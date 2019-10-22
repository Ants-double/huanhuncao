# springboot拦截所有的请求输出日志

### 添加依赖

``` xml
 <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>

        </dependency>
```

###  添加拦截类

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

