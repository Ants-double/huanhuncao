## Error response from daemon: Cannot start container … no such file or directory

系统版本和docker版本不对应,不要在没有经过验证的情况下在生产环境中使用

``` shell
yum -y update kernel
reboot
uname -r
```

