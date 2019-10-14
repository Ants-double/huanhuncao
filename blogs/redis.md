# Redis 安装
- 就是解压运行，根据自己的爱好，放到文件夹中
```
tar -zxvf redis-5.0.4.tar.gz
yum install gcc
cd redis-5.0.4
make MALLOC=libc　　
cd src
make install
```
## 修改配置文件
```
daemonize no-> daemonize yes //后台运行
bind ：127.0.0.1->bind ：0.0.0.0 //外网过滤
 protected-mode yes->protected-mode no //保护
```
## 打开防火墙
```
firewall-cmd --reload //查看开放端口
firewall-cmd --zone=public --add-port=6379/tcp --permanent 添加端口永久的
firewall-cmd --reload //重启防火墙
```

## 启动
```
redis-server 配置文件.conf
```
## 客户端连接
```
redis-cli -h hostip -p portnumber 
可以加--raw
```
## springboot 
- springboot 2.x 使用lettuce连接池
- SpringBoot2.0之后，spring容器是自动的生成了StringRedisTemplate和RedisTemplate<Object,Object>，可以直接注入，但是在实际使用中，我们大多不会直接使用RedisTemplate<Object,Object>，而是会对key,value进行序列化，所以我们还需要新增一个配置类
``` xml
 <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <version>2.1.4.RELEASE</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.springframework.session/spring-session-data-redis -->
        <dependency>
            <groupId>org.springframework.session</groupId>
            <artifactId>spring-session-data-redis</artifactId>
            <version>2.1.4.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
        </dependency>
```  
### 添加配置文件
``` properties
server.port=8081

spring.session.store-type=redis
spring.redis.database=0
spring.redis.host=104.207.131.22

spring.redis.port=6379
spring.redis.password=
spring.redis.timeout=1000

```

## MISCONF Redis is configured to save RDB snapshots
- 开启了redis对服务器磁盘的监控，redis检测到服务器的磁盘可能不能长久化的运行而做出的提示。
- 如果你为Redis的服务和持久化设置了正常的监控，你可能会想要关闭这个特征，因此Redis服务将在即使服务器磁盘、权限、退出出现问题时依然正常工作。
但这一操作将会使数据存储变得不安全，可能在磁盘出现问题的情况下丢失Redis存储的数据，因此停用此监控操作要事先备份好数据或设定Redis缓存数据的时效，Redis是一个不错的缓存数据的服务，类似于Java中的map工具类，只是要配置一下服务器的信息。
两种方法
1. 通过命令修改
```
127.0.0.1:6379> config set stop-writes-on-bgsave-error no
```
2. 更改redis.conf配置文件
```
stop-writes-on-bgsave-error no
```