# mvn本地服务nexus3的搭建 
## 下载
- [下载nexus](https://www.sonatype.com/oss-thank-you-win64.zip)
- 官网速度极慢，下面是我下好上传的大家可以下载使用链接：https://pan.baidu.com/s/1Ji5Orv3moXc60HRQ39y65Q 
提取码：jiwx 
## 安装
- 以管理员身份运行cmd 并切换到bin目录下面执行下面的命令安装服务
```
nexus.exe /install <optional-service-name>　　//安装nexus服务
```
- 启动服务
```
nexus.exe /start <optional-service-name>   //启动nexus服务

nexus.exe /stop <optional-service-name>    //停止nexus服务
```
### 其它
- 如果要更改配置信息到etc\nexus-default.properties文件中更改
```
application-host : Nexus服务监听的主机 ;

application-port: Nexus服务监听的端口;

nexus-context-path : Nexus服务的上下文路径;
```
- 默认的用户名为admin 密码为admin123
# 配置本地代理
- 我们要在pom.xml文件中配置，因为pom文件的依赖性主要还是maven的依赖性所以我们只要在最顶层配置即可
``` xml
<distributionManagement>
        <repository>
            <id>nexus-releases</id>
            <name>Nexus Release Repository</name>
            <url>http://192.168.15.13:6689/repository/maven-releases/</url>
        </repository>

        <snapshotRepository>
            <id>nexus-snapshots</id>
            <name>Nexus Snapshot Repository</name>
            <url>http://192.168.15.13:6689/repository/maven-snapshots/</url>
        </snapshotRepository>

    </distributionManagement>

    <repositories>
        <repository>
            <id>nexus</id>
            <name>Nexus Repository</name>
            <url>http://192.168.15.13:6689/repository/maven-public/</url>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
            <releases>
                <enabled>true</enabled>
            </releases>
        </repository>
        <repository>
            <id>3rdParty</id>
            <name>3rdParty</name>
            <url>http://192.168.15.13:6689/repository/3rdParty/</url>
        </repository>
        <repository>
            <id>aliyun-repos</id>
            <name>Aliyun Repository</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>

        <repository>
            <id>sonatype-repos</id>
            <name>Sonatype Repository</name>
            <url>https://oss.sonatype.org/content/groups/public</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
        <repository>
            <id>sonatype-repos-s</id>
            <name>Sonatype Repository</name>
            <url>https://oss.sonatype.org/content/repositories/snapshots</url>
            <releases>
                <enabled>false</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>

    <pluginRepositories>
        <pluginRepository>
            <id>nexus</id>
            <name>Nexus Plugin Repository</name>
            <url>http://192.168.15.13:6689/repository/maven-public/</url>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
            <releases>
                <enabled>true</enabled>
            </releases>
        </pluginRepository>

        <pluginRepository>
            <id>aliyun-repos</id>
            <name>Aliyun Repository</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </pluginRepository>
    </pluginRepositories>
```
# mvn发布到第三方库
- 我们执行发布命令
  ```
  mvn clean deploy 
  ```
## 错误类别及处理
- 错误400 就是仓库的权限问题如下图设置为allow redeploy
- ![400](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_081301.png)
- 错误401 就是setting.xml用户名密码或者仓库坐标不匹配，一一对应上即可
- ![401](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_081302.png)
- 错误405 就是pom文件中的代理配置和发布配置路径不正确 参考上面的pom文件内容
- No goals have been specified for this build  
  ``` xml
    <defaultGoal>compile</defaultGoal>
  pom.xml文件<build>标签后面加上<defaultGoal>compile</defaultGoal>即可  
  ```
# mvn新建第三方库并上传本地jar文件
## 新建第三方仓库
- 登录nexus点击仓库，右上角新增加或者是加号
- ![newnexus](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_081303.png)
- 命令并设置权限
- ![access](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_081304.png)
- 在本地Setting.xml文件中配置server同上
- 在本地jar文件夹执行下面的命令
``` cmd
mvn deploy:deploy-file -DgroupId=xxx.xxx -DartifactId=xxx -Dversion=0.0.2 -Dpackaging=jar -Dfile=D:\xxx.jar -Durl=http://xxx.xxx.xxx.xxx:8081/repository/3rdParty/ -DrepositoryId=3rdParty
其中-DgroupId 为上传的jar的groupId
-DartifactId 为上传的jar的artifactId
-Dversion 为上传的jar的需要被依赖的时候的版本号
然后是-Dpackaging为jar，-Dfile为jar包路径 
-Durl 为要上传的路径，可以通过以下方式获取到
  mvn deploy:deploy-file -DgroupId=edu.ucar -DartifactId=grib -Dversion=4.3.19 -Dpackaging=jar -Dfile=F:\my3djar\grib-4.3.19.jar -Durl=http://192.168.15.13:6689/repository/3rdParty/ -DrepositoryId=3rdParty
```
![result](https://www.cnblogs.com/images/cnblogs_com/ants_double/1413361/o_081305.png)
- 最后在pom文件是配置这个第三库的代理
# mvn依赖报红线不影响正常使用解决办法
## 本地仓库有这个jar文件，但是还是报错，操作如下
- 把pom.xml文件是报错的依赖删除，更新maven并clean一下
- 再把报错的依赖还原，更新maven (俗称手动更新依赖)