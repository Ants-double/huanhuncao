
#
## Computation of average could overflow
```
   NewChA[0] = (Ch[0] + Ch[1]) / 2;

```
- The code computes the average of two integers using either division or signed right shift, and then uses the result as the index of an array. If the values being averaged are very large, this can overflow (resulting in the computation of a negative average). Assuming that the result is intended to be nonnegative, you can use an unsigned right shift instead. In other words, rather that using (low+high)/2, use (low+high) >>> 1
This bug exists in many earlier implementations of binary search and merge sort. Martin Buchholz found and fixed it in the JDK libraries, and Joshua Bloch widely publicized the bug pattern.

- 大平均数可能溢出
```
 (Ch[0] + Ch[1]) >>> 1
``` 
## Dead store to local variable

```
public static void main(String[] args) {
		
		ConfigurableApplicationContext context = SpringApplication.run(O3mpFileServerStartMain.class, args);
		
		logger.info("Web接口项目启动!");
		
	}
``` 
- This instruction assigns a value to a local variable, but the value is not read or used in any subsequent instruction. Often, this indicates an error, because the value computed is never used.
Note that Sun's javac compiler often generates dead stores for final local variables. Because FindBugs is a bytecode-based tool, there is no easy way to eliminate these false positives.
- 局部变量没有使用
## Write to static field from instance method
- This instance method writes to a static field. This is tricky to get correct if multiple instances are being manipulated, and generally bad practice.
- 在实例方法中更改静态字段 ，在多线程的情况下可以导不一致的情况
- 解决：考虑单例模式或看具体需求
##  Useless object created
- Our analysis shows that this object is useless. It's created and modified, but its value never go outside of the method or produce any side-effect. Either there is a mistake and object was intended to be used or it can be removed.
This analysis rarely produces false-positives. Common false-positive cases include:
- This object used to implicitly throw some obscure exception.
- This object used as a stub to generalize the code.
- This object used to hold strong references to weak/soft-referenced objects.
- 创建了局部变量，并做了相关值的修改，但是没有再次使用，运行完作用域就没有了。
- 删除
## Code contains a hard coded reference to an absolute pathname
- This code constructs a File object using a hard coded to an absolute pathname (e.g., new File("/home/dannyc/workspace/j2ee/src/share/com/sun/enterprise/deployment");
- 文件路径使用绝对路径
- 解决：使用相对路径
## Integral division result cast to double or float
- This code casts the result of an integral division (e.g., int or long division) operation to double or float. Doing division on integers truncates the result to the integer value closest to zero. The fact that the result was cast to double suggests that this precision should have been retained. What was probably meant was to cast one or both of the operands to double before performing the division. Here is an example:
```
int x = 2;
int y = 5;
// Wrong: yields result 0.0
double value1 =  x / y;

// Right: yields result 0.4
double value2 =  x / (double) y;
```  
## Class doesn't override equals in superclass
- This class extends a class that defines an equals method and adds fields, but doesn't define an equals method itself. Thus, equality on instances of this class will ignore the identity of the subclass and the added fields. Be sure this is what is intended, and that you don't need to override the equals method. Even if you don't need to override the equals method, consider overriding it anyway to document the fact that the equals method for the subclass just return the result of invoking super.equals(o).
- 继承类修改了epuals方法，考虑在父类中操作

## Exception is caught when Exception is not thrown
- This method uses a try-catch block that catches Exception objects, but Exception is not thrown within the try block, and RuntimeException is not explicitly caught. It is a common bug pattern to say try { ... } catch (Exception e) { something } as a shorthand for catching a number of types of exception each of whose catch blocks is identical, but this construct also accidentally catches RuntimeException as well, masking potential bugs.
A better approach is to either explicitly catch the specific exceptions that are thrown, or to explicitly catch RuntimeException exception, rethrow it, and then catch all non-Runtime Exceptions, as shown below:
```
//添加运行时异常抛出
  try {
    ...
  } catch (RuntimeException e) {
    throw e;
  } catch (Exception e) {
    ... deal with all non-runtime exceptions ...
  }
```

## May expose internal representation by returning reference to mutable object
- Returning a reference to a mutable object value stored in one of the object's fields exposes the internal representation of the object.  If instances are accessed by untrusted code, and unchecked changes to the mutable object would compromise security or other important properties, you will need to do something different. Returning a new copy of the object is better approach in many situations.
- 解决：返回对象的副本，copy 或者clone
## Field should be package protected
- A mutable static field could be changed by malicious code or by accident. The field could be made package protected to avoid this vulnerability.

## Non-transient non-serializable instance field in serializable class
- This Serializable class defines a non-primitive instance field which is neither transient, Serializable, or java.lang.Object, and does not appear to implement the Externalizable interface or the readObject() and writeObject() methods.  Objects of this class will not be deserialized correctly if a non-Serializable object is stored in this field.
- 解决：其中属性类添加序列化

## Method with Boolean return type returns explicit null
- A method that returns either Boolean.TRUE, Boolean.FALSE or null is an accident waiting to happen. This method can be invoked as though it returned a value of type boolean, and the compiler will insert automatic unboxing of the Boolean value. If a null value is returned, this will result in a NullPointerException.

## Comparison of String objects using == or !=
- This code compares java.lang.String objects for reference equality using the == or != operators. Unless both strings are either constants in a source file, or have been interned using the String.intern() method, the same string value may be represented by two different String objects. Consider using the equals(Object) method instead.
## Call to static DateFormat
- As the JavaDoc states, DateFormats are inherently unsafe for multithreaded use. The detector has found a call to an instance of DateFormat that has been obtained via a static field. This looks suspicous.
## Inconsistent synchronization
- The fields of this class appear to be accessed inconsistently with respect to synchronization.  This bug report indicates that the bug pattern detector judged that
The class contains a mix of locked and unlocked accesses,
The class is not annotated as javax.annotation.concurrent.NotThreadSafe,
At least one locked access was performed by one of the class's own methods, and
The number of unsynchronized field accesses (reads and writes) was no more than one third of all accesses, with writes being weighed twice as high as reads
A typical bug matching this bug pattern is forgetting to synchronize one of the methods in a class that is intended to be thread-safe.
You can select the nodes labeled "Unsynchronized access" to show the code locations where the detector believed that a field was accessed without synchronization.
Note that there are various sources of inaccuracy in this detector; for example, the detector cannot statically detect all situations in which a lock is held.  Also, even when the detector is accurate in distinguishing locked vs. unlocked accesses, the code in question may still be correct.
- 解决：get方法添加了synchronized ，set没有添加
## Call to equals() comparing different types
- This method calls equals(Object) on two references of different class types and analysis suggests they will be to objects of different classes at runtime. Further, examination of the equals methods that would be invoked suggest that either this call will always return false, or else the equals method is not be symmetric (which is a property required by the contract for equals in class Object).
## Invocation of toString on an array
- The code invokes toString on an array, which will generate a fairly useless result such as [C@16f0472. Consider using Arrays.toString to convert the array into a readable String that gives the contents of the array. See Programming Puzzlers, chapter 3, puzzle 12.
## Bad comparison of signed byte
- Signed bytes can only have a value in the range -128 to 127. Comparing a signed byte with a value outside that range is vacuous and likely to be incorrect. To convert a signed byte b to an unsigned value in the range 0..255, use 0xff & b
## Should be a static inner class
- This class is an inner class, but does not use its embedded reference to the object which created it.  This reference makes the instances of the class larger, and may keep the reference to the creator object alive longer than necessary.  If possible, the class should be made static.
## Inefficient use of keySet iterator instead of entrySet iterator
- This method accesses the value of a Map entry, using a key that was retrieved from a keySet iterator. It is more efficient to use an iterator on the entrySet of the map, to avoid the Map.get(key) lookup.

## Method invokes inefficient Number constructor; use static valueOf instead
- Using new Integer(int) is guaranteed to always result in a new object whereas Integer.valueOf(int) allows caching of values to be done by the compiler, class library, or JVM. Using of cached values avoids object allocation and the code will be faster.
Values between -128 and 127 are guaranteed to have corresponding cached instances and using valueOf is approximately 3.5 times faster than using constructor. For values outside the constant range the performance of both styles is the same.
Unless the class must be compatible with JVMs predating Java 1.5, use either autoboxing or the valueOf() method when creating instances of Long, Integer, Short, Character, and Byte.
## Method concatenates strings using + in a loop
- The method seems to be building a String using concatenation in a loop. In each iteration, the String is converted to a StringBuffer/StringBuilder, appended to, and converted back to a String. This can lead to a cost quadratic in the number of iterations, as the growing string is recopied in each iteration.
Better performance can be obtained by using a StringBuffer (or StringBuilder in Java 1.5) explicitly.
```
// This is bad
  String s = "";
  for (int i = 0; i < field.length; ++i) {
    s = s + field[i];
  }

  // This is better
  StringBuffer buf = new StringBuffer();
  for (int i = 0; i < field.length; ++i) {
    buf.append(field[i]);
  }
  String s = buf.toString();
```