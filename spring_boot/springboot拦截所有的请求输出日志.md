# springboot拦截所有的请求输出日志

### 添加依赖

``` xml
 <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>

        </dependency>
```

###  添加拦截类

- 说明

  ``` wiki
   整个表达式可以分为五个部分：
  
   1、execution(): 表达式主体。
  
   2、第一个*号：表示返回类型，*号表示所有的类型。
  
   3、包名：表示需要拦截的包名，后面的两个句点表示当前包和当前包的所有子包，com.antsdouble.air.api包、子孙包下所有类的方法。
  
   4、第二个*号：表示类名，*号表示所有的类。
  
   5、*(..):最后这个星号表示方法名，*号表示所有的方法，后面括弧里面表示方法的参数，两个句点表示任何参数。
  ```

  

- 要记得修改自己的扫描包

``` java
package com.antsdouble.air.api.gateway.aop;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import org.springframework.web.context.request.RequestContextHolder;
import org.springframework.web.context.request.ServletRequestAttributes;

import javax.servlet.http.HttpServletRequest;
import java.util.Arrays;

/**
 * @author lyy
 * @description
 * @date 2019/7/11
 */
@Aspect
@Component
public class WebControllerAop {

    private Logger logger=LoggerFactory.getLogger(WebControllerAop.class);
    ThreadLocal<Long> startTime = new ThreadLocal<>();
    /**
     * 指定切点
     * 匹配 com.antsdouble.air
     */
    @Pointcut("execution(public * com.antsdouble.air.*.*.controller.*.*(..))")
    public void webLog(){

    }
    /**
     * 功能描述 通过@Before实现，对请求内容的日志记录
     * @author lyy
     * @date 2019/7/11
     * @param [joinPoint]
     * @return void
     */
    @Before("webLog()")
    public void doBefore(JoinPoint joinPoint) throws Throwable {
        startTime.set(System.currentTimeMillis());

        // 接收到请求，记录请求内容
        ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
        HttpServletRequest request = attributes.getRequest();

        // 记录下请求内容
        logger.info("URL : " + request.getRequestURL().toString());
        logger.info("HTTP_METHOD : " + request.getMethod());
        logger.info("IP : " + request.getRemoteAddr());
        logger.info("CLASS_METHOD : " + joinPoint.getSignature().getDeclaringTypeName() + "." + joinPoint.getSignature().getName());
        logger.info("ARGS : " + Arrays.toString(joinPoint.getArgs()));

    }

    /**
     * 功能描述 最后通过@AfterReturning记录请求返回的对象。
     * @author lyy
     * @date 2019/7/11
     * @param [ret]
     * @return void
     */
    @AfterReturning(returning = "ret", pointcut = "webLog()")
    public void doAfterReturning(Object ret) throws Throwable {
        // 处理完请求，返回内容
        logger.info("RESPONSE : " + ret);
        logger.info("SPEND TIME : " + (System.currentTimeMillis() - startTime.get()));
    }
}

```

