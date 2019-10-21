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

    

-  发送邮件

  ``` wiki
  
  ```

  1. 添加maven依赖
    ``` xml
      <dependency>
                 <groupId>org.springframework.boot</groupId>
                 <artifactId>spring-boot-starter-mail</artifactId>
     
             </dependency>
    ```
  2.  添加配置信息

     ``` properties
     spring.application.name=spring-boot-mail
     
     # 邮箱主机
     spring.mail.host=smtp.qq.com
     # userName
     spring.mail.username=896478104@qq.com
     # password
     spring.mail.password=u******
     spring.mail.default-encoding=utf-8
     #解决530的错误
     spring.mail.properties.mail.smtp.auth=true
     spring.mail.properties.mail.smtp.starttls.enable=true
     spring.mail.properties.mail.smtp.starttls.required=true
     
     mail.from=${spring.mail.username}
     mail.to=ants_double@yeah.net
     ```
  
     
  
  3. 添加server
  
     ``` java 
     package com.antsdouble.service;
     
     import com.antsdouble.beans.MailProperties;
     import org.springframework.beans.factory.annotation.Autowired;
     import org.springframework.core.io.FileSystemResource;
     import org.springframework.mail.SimpleMailMessage;
     import org.springframework.mail.javamail.JavaMailSender;
     import org.springframework.mail.javamail.MimeMessageHelper;
     import org.springframework.stereotype.Service;
     
     import javax.mail.MessagingException;
     import javax.mail.internet.MimeMessage;
     import java.io.File;
     
     @Service("mailService")
     public class MailService {
     
         @Autowired
         private JavaMailSender mailSender;
     
         @Autowired
         private MailProperties mailProperties;
     
         //简单的发送文字
         public void sendMail() {
     
             SimpleMailMessage message = new SimpleMailMessage();
     
             message.setFrom(mailProperties.getFrom());
     
             message.setTo(mailProperties.getTo());
     
             message.setSubject("it is a test for spring boot");
     
             message.setText("你好，我是ly，我正在测试发送邮件。");
     
     
             try {
                 mailSender.send(message);
             } catch (Exception e) {
                 System.out.println(e);
             }
     
         }
     
         //带附件的
         public void sendMailAttachFile() throws MessagingException {
             MimeMessage mimeMessage = mailSender.createMimeMessage();
             MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
             helper.setFrom(mailProperties.getFrom());
     
             helper.setTo(mailProperties.getTo());
     
             helper.setSubject("主题：发送有附件的邮件");
     
             helper.setText("你好，我是ly，我正在测试发送一封有附件的邮件。");
             FileSystemResource file1 = new FileSystemResource(new File("E:\\01.gif"));
     
             FileSystemResource file2 = new FileSystemResource(new File("E:\\02.png"));
     
             helper.addAttachment("附件-1.jpg", file1);
     
             helper.addAttachment("附件-2.jpg", file2);
             try {
                 mailSender.send(mimeMessage);
             } catch (Exception e) {
                 System.out.println(e);
             }
         }
     
         //嵌入附件的
         public void sendMailAddContent() throws MessagingException {
             MimeMessage mimeMessage = mailSender.createMimeMessage();
     
             MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
     
     
             helper.setFrom(mailProperties.getFrom());
     
             helper.setTo(mailProperties.getTo());
     
     
             helper.setSubject("主题：嵌入静态资源");
     
             helper.setText("<html><body><img src=\"cid:hello\" ></body></html>", true);
     
     
             // 注意addInline()中资源名称 hello 必须与 text正文中cid:hello对应起来
     
             FileSystemResource file1 = new FileSystemResource(new File("d:\\cat.jpg"));
     
             helper.addInline("hello", file1);
     
             try {
                 mailSender.send(mimeMessage);
     
             } catch (Exception e) {
     
     
             }
         }
     
     
     }
     
     ```
  
     
  
  4. 添加controller
  
     ``` java 
     package com.antsdouble.beans;
     
     import org.springframework.boot.context.properties.ConfigurationProperties;
     import org.springframework.stereotype.Component;
     
     @Component
     @ConfigurationProperties(prefix = "mail")
     public class MailProperties {
         private String from;
         private String to;
     
         public MailProperties() {
         }
     
         public MailProperties(String from, String to) {
             this.from = from;
             this.to = to;
         }
     
         public String getFrom() {
             return from;
         }
     
         public void setFrom(String from) {
             this.from = from;
         }
     
         public String getTo() {
             return to;
         }
     
         public void setTo(String to) {
             this.to = to;
         }
     
         @Override
         public String toString() {
             return "MailProperties{" +
                     "from='" + from + '\'' +
                     ", to='" + to + '\'' +
                     '}';
         }
     }
     
     ```
  
     
  
  5. 添加beans
  
     ``` java
     package com.antsdouble.beans;
     
     import org.springframework.boot.context.properties.ConfigurationProperties;
     import org.springframework.stereotype.Component;
     
     @Component
     @ConfigurationProperties(prefix = "mail")
     public class MailProperties {
         private String from;
         private String to;
     
         public MailProperties() {
         }
     
         public MailProperties(String from, String to) {
             this.from = from;
             this.to = to;
         }
     
         public String getFrom() {
             return from;
         }
     
         public void setFrom(String from) {
             this.from = from;
         }
     
         public String getTo() {
             return to;
         }
     
         public void setTo(String to) {
             this.to = to;
         }
     
         @Override
         public String toString() {
             return "MailProperties{" +
                     "from='" + from + '\'' +
                     ", to='" + to + '\'' +
                     '}';
         }
     }
     
     ```
  
     
  
  6. 
  
  



​     

- 