# 修改dns

找到打开 修改/etc/resolv.conf 

``` shell
vim /etc/resolv.conf 
```

在最后添加	

``` conf
nameserver 8.8.8.8
```

保存并重启网卡

``` shell
systemctl restart network-manager.service
```

