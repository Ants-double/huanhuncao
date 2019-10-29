# docker问题

##  docker: Error response from daemon: Get https://registry-1.docker.io/v2/: dial tcp: lookup registry-1.docker.io on 10.194.67.199:53: server misbehaving.


-   解决方法（确保公网dns 如8.8.8.8 | 114.114.114.114)

  ``` wiki 进入/etc/docker
  查看有没有 daemon.json。这是docker默认的配置文件。
  
  如果没有新建，如果有，则修改。
  
  
  [root@antdouble docker]# vim daemon.json
  {
    "registry-mirrors": ["https://registry.docker-cn.com","http://hub-mirror.c.163.com","https://pee6w651.mirror.aliyuncs.com"]
  }
  
  保存退出。
  
  
  重启docker服务
  
   systemctl daemon-reload
   systemctl restart docker
  ```
## Job for docker.service failed because start of the service was attempted too often. See "systemctl status docker.service" and "journalctl -xe" for details.To force a start use "systemctl reset-failed docker.service" followed by "systemctl start docker.service" again.

  



- 执行如下命令

  ``` shell
   mv daemon.json daemon.conf
   systemctl restart docker
  ```




## Error response from daemon: Get https://index.docker.io/v1/search?q=mysql&n=25: dial tcp: i/o timeout

- 添加代理设置（网上有三种方法，介绍一种持久化的）

  1. 创建一个内嵌的systemd目录

     ``` shell
     mkdir -p /etc/systemd/system/docker.service.d
     ```
```

​     

  2. 分别创建http和https代理文件

     - http

     ``` shell
     vim http-proxy.conf
```

     添加如下内容
    
     ``` conf


​     
​     [Service]
​      Environment=HTTP_PROXY=http://10.200.200.253:808/”
​     ```
​    
     - https
    
       ``` shell
       vim https-proxy.conf
       ```
    
       添加如下内容
    
       ``` conf
       [Service]
       Environment=HTTPS_PROXY=http://10.200.200.253:808/”
       ```


​       

  3. 更新配置并重启docker

     ``` shell
     systemctl daemon-reload
     systemctl restart docker
     ```

     

## Error response from daemon: Get https://registry-1.docker.io/v2/: net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)

- 找到可用的ip

  ``` shell
  dig @114.114.114.114 registry-1.docker.io
  ```

  

- 修改hosts文件 位置/etc/hosts 

  ``` shell
  54.164.230.151 registry-1.docker.io
  ```


## Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

- docker 没有启用

  ``` shell
  systemctl daemon-reload
  
  systemctl restart docker.service
  ```

  