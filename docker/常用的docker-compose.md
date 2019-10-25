# 常用的docker-compose

## 常用命令

``` wiki
docker-compose up -d
docker-compose down 

docker-compose stop
docker-compose start
 <-- 重新编译dockerfile生成镜像-->
docker-compose up -d --build
```



## mysql

``` yml
version: '3.1'
services: 
    db:
      # images 8.x
      image: mysql
      restart: always
      environment: 
        MYSQL_ROOT_PASSWORD: 456123
      command: 
        --default-authentication-plugin=mysql_native_password
        --character-set-server=utf8mb4
        --collation-server=utf8mb4_general_ci
        --explicit_defaults_for_timestamp=true
        --lower_case_table_names=1
      ports: 
        - 3309:3306
      volumes: 
        - ./data:/var/lib/mysql
    
```

## zookeeper

``` yml
version: '3.1'

services:
  zoo1:
    image: zookeeper
    restart: always
    container_name: zook1
    hostname: zook1
    ports:
      - 2187:2181
    environment:
      ZOO_MY_ID: 1
      ZOO_SERVERS: server.1=0.0.0.0:2888:3888;2181 server.2=zook2:2888:3888;2181 server.3=zook3:2888:3888;2181
    volumes: 
      - ./zook1:/conf

  zoo2:
    image: zookeeper
    restart: always
    container_name: zook2
    hostname: zook2
    ports:
      - 2188:2181
    environment:
      ZOO_MY_ID: 2
      ZOO_SERVERS: server.1=zook1:2888:3888;2181 server.2=0.0.0.0:2888:3888;2181 server.3=zook3:2888:3888;2181
    volumes: 
      - ./zook1:/conf

  zoo3:
    image: zookeeper
    restart: always
    container_name: zook3
    hostname: zook3
    ports:
      - 2189:2181
    environment:
      ZOO_MY_ID: 3
      ZOO_SERVERS: server.1=zook1:2888:3888;2181 server.2=zook2:2888:3888;2181 server.3=0.0.0.0:2888:3888;2181
    volumes: 
      - ./zook1:/conf
```

## 启动自定义的dockerfile

``` yaml
version: '3.1'
services: 
    consumer:
       build: 
         context: .
         dockerfile: dockerfile
       image: consumer
       container_name: luzhouconsumer
       restart: always
       networks: 
         - nets
       volumes: 
         - ./contentconsumer.log:/usr/src/myapp/contentconsumer.log
       ports: 
         - 7779:7779
       environment: 
         - JAVA_OPTS=-Xmx256M -Dspring.profiles.active=test -Duser.timezone=GMT+08
networks: 
    nets:   
      external: false    


```



## 同时启动多个jar

``` yml
version: '3.1'
services: 
    provider:
       build: 
         context: .
         dockerfile: providerdockerfile
       image: provider
       container_name: luzhouprovider
       restart: always
       networks: 
         - nets
       volumes: 
         - ./contentprovider.log:/usr/src/myapp/contentprovider.log
       ports: 
         - 6669:6669
       environment: 
         - JAVA_OPTS=-Xmx256M -Dspring.profiles.active=test -Duser.timezone=GMT+08
    consumer:
       build: 
         context: .
         dockerfile: consumerdockerfile
       image: consumer
       container_name: luzhouconsumer
       restart: always
       networks: 
         - nets
       volumes: 
         - ./contentconsumer.log:/usr/src/myapp/contentconsumer.log
       ports: 
         - 7779:7779
       environment: 
         - JAVA_OPTS=-Xmx256M -Dspring.profiles.active=test -Duser.timezone=GMT+08
networks: 
    nets:   
      external: false    


```

## nginx

```shell
docker run  --name mynginx -d -p 80:80 -v E:/docker/luzhou/nginx/nginx.conf:/etc/nginx/nginx.conf -v E:/docker/luzhou/nginx/conf.d:/etc/nginx/conf.d  -v E:/docker/luzhou/nginx/logs:/var/log/nginx nginx
```



``` yaml
version: '3.1'
services:
  nginx:
    # build: 
    #   context: .
    #   dockerfile: nginxdockerfile    
    restart: always
    image: nginx
    container_name: luzhounginx
    networks: 
      - nets
    ports:
      - 80:80
    volumes:
      - ./conf:/etc/nginx     #映射nginx的配置文件到容器里
      # - ./conf/nginx.conf:/etc/nginx/nginx.conf
      - ./logs:/var/log/nginx
    # command: [nginx-debug, '-g', 'daemon off;']
networks: 
    nets:   
      external: false   
```

