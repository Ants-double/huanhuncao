# springboot配置集成vue前端并打包发布

## 操作步骤

1. 新建一个springboot工程orchid

2. 新建一个vue项目并成功打包，可以参考[https://www.cnblogs.com/ants_double/p/13391211.html](https://www.cnblogs.com/ants_double/p/13391211.html)

3. 添加必要的依赖

   ``` xml
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-thymeleaf</artifactId>
           </dependency>
   ```

   

4. 添加controller入口

   ``` java
   @Controller()
   @RequestMapping("/")
   public class IndexController {
       @GetMapping("home")
       public ModelAndView index(){
           ModelAndView mv =  new ModelAndView("index");
           return mv;
       }
   }
   ```

   

5. 配置资源文件

   ``` yaml
   spring:
     thymeleaf:
       prefix: classpath:/templates/
       suffix: .html
       servlet:
         content-type: text/html
       mode: HTML
       cache: false
       encoding: utf-8
   
   ```

   

   

6. 放入vue生成的包文件（使用默认路径）

   - static 文件夹放入 resources/static文件夹下
   - index.html放入resources/templates文件夹下

7. 打包发布

   ``` shell
   mvn package
   nohup java -jar ****.jar
   ```

   

## 源码

- [https://github.com/Ants-double/orchid 中的init_orchid分支](https://github.com/Ants-double/orchid)

