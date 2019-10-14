
# 运行数据区域
## 程序计数器
- 是一块较小的空间，可以看作是当前线程所执行的字节码的行号的指示器，为了线程切换后能恢复到正确的位置，每条线程都有一个独立的程序计数器，各条线程之间的计数器互不影响，独立存储。这类内存称为线程私有的内存
## Java虚拟机栈
- 也就是传说中的栈区，也是线程私用的，它的生命周期和线程相同，主要描述方法执行的内存模型，每执行一个方法就会创建一个栈帧用于存储方法信息并入栈，方法执行完出栈。
- 当进入一个方法时，分配多大的局部变量大小是完全确定的，运行期间也不会改变局部变量的大小。其中long和double类型会占用两个局部变量的空间，其字基本类型占用一个
- 此处会有两个异常
 1. StackOverflowError ：请求的栈的深度大于虚拟机所允许的最大值 
 2. OOM:如果栈是在扩展的情况下，扩展时无法申请到足够的内存
## 本地方法栈
- 在HotSpot中与虚拟机栈合二为一，同样异样也是一样的两种
- 主要是虚拟机使用到的Native服务时使用，规范中没有指定本地方法栈中使用的语言，方式和数据结构
## Java 堆
- 不是线程私用的，是被所有线程共享的一块内存区域，此处主要存放对象的实例（因为JIT发展导致并不是所有的对象都分配在堆上）
- 堆可以是物理上不连续的空间，只要逻辑上连续即可，现在的堆都是可以扩展的
- Xmx:分配堆的最大值
- Xms:初始化堆的大小
- 如果没有内存分配并且无法扩展将会产生OOM异常。
- 新生代
 1. Eden
 2. From Survivor
 3. To Survivor
- 老年代
TLAB：线程共享区是否划出多个线程私有分配缓冲区
## 方法区
- 线程共区域，用于存储加载的类信息，常量和静态变量，即时编译后的代码等数据，在HotSpot也就是所谓的永久代（原因是此处也是按照GC分代回收，统一回收的策略）jdk1.7中把字符串常量池移出并正逐步改为采用Native Memory来实现方法区的规划了
- -XX:MaxPermSize 用来标记此区域的最大值
- 此处的垃圾回收效果不太满意，但是回收却是必要的
## 运行时常量池
- 主要用来存编译期生成的各种字面量和符号引用，这部分内容将在类加载后进行方法区运行时常量池存放
- 不仅是编译时产生，而且运行时可能将新的常量存入池中如String的intern()方法
- 同产如果无法申请到内存也会报OOM
## 直接内存
- 使用Navative函数库直接分配堆外的内存，然后通过Java堆中的DirectByteBuffer对象作为这块内存的引用进行操作
- 内存受物理内存和操作系统内存管理的影响，如果操作大于真实可用的内存也会报OOM
# 对象创建

## 分配有两种方式
 1. 指针碰撞： Serial ParNew 等带Compact的收集器（考虑多线程情况下失败重试，和原子性）
 2. 空闲列表：CMS 基于Mark-SWeep的收集器
 - -XX:+/-UseTLAB参数设定是否启动本地线程分配缓冲，如果使用不赋初始值就能直接使用，否则要进行初始化为0值

## 对象的内存布局
- 对象头
 1. 对象自身运行时数据
 2. 类型指针
- 实例数据
- 对齐填充
## 对象的访问
- 句柄访问：划分句柄池存放实例和类型数据和具体地址信息
 1. 就是在对象移动时不用改变reference
- 直接指针访问
 2. 快，速度快，HotSpot是基于这一种的
## 常见的OOM异常
1. 堆溢出
``` java
//-Xms20m -Xmx20m -XX:+HeapDumpOnOutOfMemoryError
public class HeapOOM {
    static class OOMObject {
    }

    public static void main(String[] args) {
        List<OOMObject> list = new ArrayList<OOMObject>();
        while (true) {
            list.add(new OOMObject());
        }
    }
}
/*
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at java.util.Arrays.copyOf(Arrays.java:3210)
	at java.util.Arrays.copyOf(Arrays.java:3181)
	at java.util.ArrayList.grow(ArrayList.java:265)
	at java.util.ArrayList.ensureExplicitCapacity(ArrayList.java:239)
	at java.util.ArrayList.ensureCapacityInternal(ArrayList.java:231)
	at java.util.ArrayList.add(ArrayList.java:462)
	at com.antsdouble.HeapOOM.main(HeapOOM.java:13)
*/

``` 
- 分析dump文件确认是内存泄漏还是内存溢出 判断原因针对性的解决
## 栈溢出
``` java
//-Xss128k 设置栈的大小
public class JavaVMStackOOM {
    private int stackLength=1;
    public void stackLeak(){
        stackLength++;
        stackLeak();
    }

    public static void main(String[] args) throws Throwable {
        JavaVMStackOOM oom=new JavaVMStackOOM();
        try {
            oom.stackLeak();
        }
        catch (Throwable e){
            System.out.println(oom.stackLength);
            throw e;
        }
    }
}
/*
19987
Exception in thread "main" java.lang.StackOverflowError
	at com.antsdouble.JavaVMStackOOM.stackLeak(JavaVMStackOOM.java:7)
	at com.antsdouble.JavaVMStackOOM.stackLeak(JavaVMStackOOM.java:7)
*/
```  
多线程的时候可能是OOM,此时可以减少堆的内存来换取更多的线程来解决这个问题

## 方法区和运行时常量溢出
- String.intern()是一个Native方法：作用如果字符串常量池中有就返回，否则就添加到常量池中并返回 
- -XX:PermSize 常量区的大小
- -XX:MaxPermSize 最大值
OOM PerGen space
- CGLib这类字节码技术，增强的类越多，就需要越大的方法区来保证动态生成的Class加入内存，以及大量JSP或OSGi应用 
## 本机直接内存溢出
- DirectMemory可以通过-XX:MaxDirectMemorySize来指定，如不指定默认和-Xmx一样，
- 一般Heap Dump看不到明显的异常也就是dump文件很小而且程序使用NIO这类技术就应该检查一下这个原因
