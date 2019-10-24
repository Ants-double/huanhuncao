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
    image: zookeeper:3.4.14
    restart: always
    hostname: zoo1
    ports:
      - 2187:2181
    environment:
      ZOO_MY_ID: 1
      ZOO_SERVERS: server.1=0.0.0.0:2888:3888;2181 server.2=zoo2:2888:3888;2181 server.3=zoo3:2888:3888;2181

  zoo2:
    image: zookeeper:3.4.14
    restart: always
    hostname: zoo2
    ports:
      - 2188:2181
    environment:
      ZOO_MY_ID: 2
      ZOO_SERVERS: server.1=zoo1:2888:3888;2181 server.2=0.0.0.0:2888:3888;2181 server.3=zoo3:2888:3888;2181

  zoo3:
    image: zookeeper:3.4.14
    restart: always
    hostname: zoo3
    ports:
      - 2189:2181
    environment:
      ZOO_MY_ID: 3
      ZOO_SERVERS: server.1=zoo1:2888:3888;2181 server.2=zoo2:2888:3888;2181 server.3=0.0.0.0:2888:3888;2181
```

