# docker和docker-compose及Docker Machine安装

centos7 

## docker

1. 在线安装

   参考网址：https://docs.docker.com/engine/install/centos/

   ``` shell
   sudo yum install -y yum-utils
   sudo yum-config-manager \
       --add-repo \
       https://download.docker.com/linux/centos/docker-ce.repo
   sudo yum-config-manager --enable docker-ce-nightly
   sudo yum install docker-ce docker-ce-cli containerd.io
   sudo yum install docker-ce-19.03.9 docker-ce-cli-19.03.9 containerd.io
   sudo systemctl start docker
   sudo docker run hello-world
   ```

   

2. 离线安装

   - 下载rpm包

   - 安装

     ``` shell
     yum install /path/to/package.rpm
     ```

     

3. 卸载

   ``` shell
   sudo yum remove docker-ce
   sudo rm -rf /var/lib/docker
   sudo rm -rf /run/docker
   sudo rm -rf /var/run/docker
   sudo rm -rf /etc/docker
   ```

   

## docker-compose

[ https://docs.docker.com/compose/install/ ]( https://docs.docker.com/compose/install/ )

1. 在线安装

   - 下载并重命名

   ``` shell 
   sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

   - 添加可执行权限

     ``` shell
     sudo chmod +x /usr/local/bin/docker-compose
     ```

     

   - 添加软链

     ``` shell
     sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
     docker-compose --version
     ```

     

2. 离线安装

   参考windows平台下面操作

3.  卸载

   ``` shell
   sudo rm /usr/local/bin/docker-compose
   ```

   如果使用pip安装 执行下面

   ``` shell
   pip uninstall docker-c
   ```


## Docker Machine

[ https://docs.docker.com/machine/install-machine/ ]( https://docs.docker.com/machine/install-machine/ )

1. 在线安装

   ``` shell
    base=https://github.com/docker/machine/releases/download/v0.16.0 &&
     curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
     sudo mv /tmp/docker-machine /usr/local/bin/docker-machine &&
     chmod +x /usr/local/bin/docker-machine
   ```

   