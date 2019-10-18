# SpringBoot 常识

## 框架相关

- 打印springboot提供的Beans

  ``` java
  @Bean
      public CommandLineRunner commandLineRunner(ApplicationContext ctx){
          return args -> {
              System.out.println("Let's inspect the beans provided by spring boot");
              String[] beanDefinitionNames = ctx.getBeanDefinitionNames();
              Arrays.sort(beanDefinitionNames);
              for (String beanName:beanDefinitionNames){
                  System.out.println(beanName);
              }
          };
      }
  ```

  

- 引用C++ dll

  [C++工程 https://github.com/Ants-double/yumi/tree/master/testDll ]( https://github.com/Ants-double/yumi/tree/master/testDll )

  - 添加依赖

  ``` xml
   <!-- https://mvnrepository.com/artifact/net.java.dev.jna/jna -->
          <dependency>
              <groupId>net.java.dev.jna</groupId>
              <artifactId>jna</artifactId>
              <version>5.4.0</version>
          </dependency>
  ```

  - 调用代码

    ``` java
    package com.antsdouble;
    
    import com.sun.jna.Library;
    import com.sun.jna.Native;
    
    /**
     * @author lyy
     * @description
     * @date 2019/9/17
     */
    public class Application {
        public interface Dll extends Library {
            // 调用自定义 DLL
            Dll instance = (Dll) Native.load("testDll", Dll.class);
            int add(int a,int b);
        }
    
        //做一次转换
    
        public static void main(String[] args) {
            System.out.println("test jna");
            System.out.println(Dll.instance.add(41,6));
        }
    }
    
    ```

    