# vultr

- 安装

  ``` shell
  
  wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
  chmod +x shadowsocks.sh
  ./shadowsocks.sh 2>&1 | tee shadowsocks.log  
  ```

  

- 修改配置 /etc/shadowsocks.json

  ``` json
   {
      "server":"0.0.0.0",
      "local_address":"127.0.0.1",
      "local_port":1080,
     "port_password":{
           "4455":"密码1",
           "5566":"密码2",
           "6677":"密码3"
  }, 
      "timeout":300,
      "method":"aes-256-cfb",
      "fast_open":false
  }
  tip: 是json格式的文件，注意标点符号。
  ```

  

- 重启

  ``` shell
  需要用到的命令：
  启动：service shadowsocks start
  停止：service shadowsocks stop
  重启：service shadowsocks restart
  状态：service shadowsocks status
  ```

  

- 防火墙

  ``` shell
  firewall-cmd --zone=public --add-port=80/tcp --permanent
  
  命令含义：
  
  --zone #作用域
  
  --add-port=80/tcp  #添加端口，格式为：端口/通讯协议
  
  --permanent  #永久生效，没有此参数重启后失效
  重启网络端口
  firewall-cmd --reload
  查看
  firewall-cmd --zone= public --query-port=80/tcp
  删除
  firewall-cmd --zone= public --remove-port=80/tcp --permanent
  查看已经开放的端口：
  firewall-cmd --list-ports
  ```

  

