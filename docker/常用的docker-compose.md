# 常用的docker-compose

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

