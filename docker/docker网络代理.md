# docker 网络代理

centos 7 系统环境

##  DNS设置
设置DNS为包含公网DNS

## 解决方案

1. 手动启动命令行监听

   ``` shell
   systemctl stop docker.service
   nohup docker daemon -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock
   ```

   

2. 修改系统配置来修改daemon

   在/etc/sysconfig/docker添加代理信息

   ``` conf
   HTTP_PROXY=http://10.200.200.253:808
   http_proxy=$HTTP_PROXY
   HTTPS_PROXY=$HTTP_PROXY
   https_proxy=$HTTP_PROXY
   export HTTP_PROXY HTTPS_PROXY http_proxy https_proxy
   ```

   

3. 持久化修改会覆盖docker.service文件

   - 创建systemd内嵌目录

     ``` shell
     mkdir -p /etc/systemd/system/docker.service.d
     ```

     

   - 创建代理文件,具体ip和端口要做相应的修改

     ``` shell
     vim http-proxy.conf
     放下面内容
     [Service]
      Environment=HTTP_PROXY=http://10.200.200.253:808/”
     vim https-proxy.conf
     [Service]
     Environment=HTTPS_PROXY=http://10.200.200.253:808/”
     ```

     

   - 刷新配置并重启docker

     ``` shell
     systemctl daemon-reload
     systemctl restart docker
     ```

     

4. 通过daemon.json来修改

   ``` json
   {
       "bip":"ip+端口"
     "registry-mirrors": ["https://registry.docker-cn.com","http://hub-mirror.c.163.com"]
   }
   ```

   