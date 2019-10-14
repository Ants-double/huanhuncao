# Docker使用
##  Docker 安装
- 使用脚本安装
```
sudo curl -sSL https://get.daocloud.io/docker | sh
```
## 卸载
```
sudo apt-get remove docker docker-engine docker-ce docker.io
```
## 配置镜像/etc/docker/daemon.json(没有则创建)
//"registry-mirrors":["https://registry.docker-cn.com"]

```
{
  "registry-mirrors": ["https://72idtxd8.mirror.aliyuncs.com"]
}
``` 
# 遇到的错误
1. Please enter passphrase for disk ants--vg-swap_1 (cryptswap1) on none! Job for docker.service failed. See "systemctl status docker.service" and "journalctl -xe" for details.
![passphrase](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_%e6%89%b9%e6%b3%a8%202019-05-21%20090607.png)
- 解决
编译/etc/fstab  文件删除下面一行
```
/dev/mapper/ubuntu--vg-swap_1 none            swap    sw              0       0
``` 
2. systemctl status docker.service
![status](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_docker%20mirror%20error.png)
- 配置镜像文件内容出错
修改/etc/docker/daemon.json 内容 ，用json校验工具校验一下

