# mysql8的安装
## 写在前面
- 与5.*的版本整体差不多，但是安装细节决定成败
## 下载
点击https://dev.mysql.com/downloads/file/?id=476233，也可以点[这里](https://dev.mysql.com/downloads/file/?id=476233),有账号可以登录，没有选最下面的跳过。
## 安装和启动
1. 把bin添加到环境变量path下面，win10注意每个变量是新起一行，不要在最后加分号
2. 添加配置文件my.ini(直接txt改名和后缀即可)，内容如下,编码格式选ANSI
```
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[mysqld]
#设置3306端口
port = 3306
# 设置mysql的安装目录
basedir=E:\mysql-5.6.42-winx64
# 设置mysql数据库的数据的存放目录 data后面的命令会生成
datadir=E:\mysql-5.6.42-winx64\data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```
3. 以管理员身份运行命令行，并切到mysql的bin目录，然后执行下面的语句,不要关闭此窗口，在里面找到初始化密码
```
mysqld --initialize --console
```
4. 安装服务
``` cmd
// 服务名可以不写，默认的名字为 mysql
mysqld --install [服务名]
``` 
5. 启动服务
```
// 注意服务名，没有写就是mysql
net start mysql
```
- 其它
```
// 停止服务
net stop mysql 
// 卸载 MySQL
sc delete MySQL/mysqld -remove
```
## 设置
- 更改密码(先用初始化密码登录进去)
```
mysql -u root -p
```
然后执行
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';  
```  
- 设置外网访问
```
// 进入mysql库
use mysql
// 更新域属性，'%'表示允许外部访问
update user set host='%' where user ='root';
// 更改生效
FLUSH PRIVILEGES;
// 再执行授权语句
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'WITH GRANT OPTION;
```
- Navicat 连接
1. Navicat12以上的版本没有区别，直接连
2. Navicat12以下的更改加密方式caching_sha2_password->mysql_native_password
```
update user set plugin='mysql_native_password' where user='root';
``` 
- 不能访问，查看端口是否通过防火墙，尽量不要直接关防火墙（排查原因可以试一下）

