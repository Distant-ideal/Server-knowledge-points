# windows服务

## 什么是windows服务

windows服务是可以在windows会话长时间运行的可执行应用程序，这些服务可以在计算机启动时自动启动，也可以暂停或者重新启动而且不需要开发任何用户控制界面。这种服务非常适合在服务器上使用，或任何时候，为了不影响在用一台计算机上工作的其他用户，需要长时间运行功能时使用。

## windows服务于游戏服务器的关系

c#代码需要可执行程序作为容器，那么我们使用windows服务来作为容器，咱们编程好的服务器可以随着windows的启动而自动启动，不需要每次开机手动执行服务器的启动

## visual studio 2019创建windows服务

AssemblyInfo.cs文件中引用的类库和功能的定义和生成的版本号

App.config文件中配置文件

Program.cs启动和执行的文件

service1.cs配置的文件

右键点击安装程序

在其中找到serviceInstaller1点击查看属性将DisplayName和ServiceName修改将其中的StartType修改为Automatic（自动）

找到serviceProcessInstaller1点击查看属性修改Account为LocalSystem（本地系统）

重新生成解决方案

在debug文件夹中新建两个批处理文件install.bot和uninstall.bot

完成文件后在控制面板服务中查看是否成功

### install.bot

```
cd /d "%~dp0"
InstallUtil KingOfGlory.Host.exe
net start KingOfGlory
cmd
```

### uninstall.bot

```
cd /d "%~dp0"
InstallUtil /u KingOfGlory.Host.exe
net start KingOfGlory
cmd
```













