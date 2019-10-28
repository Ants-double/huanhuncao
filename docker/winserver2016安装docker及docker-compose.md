# winserver2016安装docker及docker-compose

## docker 安装

- 更新系统到最新版

  - 可以通过设置来更新，也可以通过命令行来更新命令如下

    1. 启动powershell

    2. 输入sconfig 之后选择6 输入A更新所有更新

       

    

- 安装docker 

  参考[微软官网 点击跳转]( https://docs.microsoft.com/zh-cn/virtualization/windowscontainers/quick-start/set-up-environment?tabs=Windows-Server )

  - 注册提供商

    ``` powershell
    Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
    ```

    

  - 安装docker 

     ``` powershell
    Install-Package -Name docker -ProviderName DockerMsftProvider
     ```

    -  PowerShell 询问是否信任包源“DockerDefault”时，键入 `A` 以继续进行安装。

  - 安装完成，重启

    ``` powershell
    Restart-Computer -Force
    ```

    

## docker-compose 安装

1. 手动安装

- 下载软件包,选择window平台[ https://github.com/docker/compose/releases/ ]( https://github.com/docker/compose/releases/ )

- 找到系统Docker安装目录，把软件重命名为docker-compose.exe并放在docker的安装目录中

- 把docker添加到环境变量

  

2. 自动安装，我自动安装失败，看着自动安装流程就是下载注册的流程，所以手动安装如上。

   参考： https://docs.docker.com/compose/install/ 

   ``` 
   1. 管理员运行powershell
   2. 请求TLS1.2 
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
   3. 下载安装（1.21.1为例）
   Invoke-WebRequest "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\Docker\docker-compose.exe
   ```