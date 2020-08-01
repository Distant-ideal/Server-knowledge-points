# Topshelf服务

## 什么是Topshelf

Topshelf是创建windows服务的另一种方法，Topshelf是一个开源的跨平台的宿主服务框架，支持windows和mono，值需要引用Topshelf组件库，再加上几行代码就可以构件一个很方便使用的服务宿主

## Topshelf的好处

普通windows服务项目，在断点测试时比较麻烦，必须使用vs的附加进程功能，而topshelf项目在开发阶段很方便，无需先注册成windows服务，直接在vs中启动项目，便可实现游戏服务的启动，也可非常方便的进行断点测试。

```
HostFactory.Run(x =>
{
    x.Service<StartService>(s =>
    {
        s.ConstructUsing(name => new StartService());
        s.WhenStarted(tc => tc.Start());
        s.WhenStopped(tc => tc.Stop());
    });
    x.RunAsLocalSystem();//本地服务

    x.SetDescription("KingOfGlory");
    x.SetDisplayName("KingOfGlory");
    x.SetServiceName("KingOfGlory");
});
```

## visual studio 2019创建Topshelf服务

创建c#控制台应用（。NET Framework）项目

在目录中创建一个引用文件夹为了有利于合作开发

在网络上下载topshelf并将.dll文件放入引用文件夹中

### 脚本

```
using System;
using Topshelf;

namespace KingOfGlory.Host
{
    class Program
    {
        static void Main(string[] args)
        {
            HostFactory.Run(x =>
            {
                x.Service<StartService>(s =>
                {
                    s.ConstructUsing(name => new StartService());
                    s.WhenStarted(tc => tc.Start());
                    s.WhenStopped(tc => tc.Stop());
                });
                x.RunAsLocalSystem();//本地服务

                x.SetDescription("KingOfGlory");
                x.SetDisplayName("KingOfGlory");
                x.SetServiceName("KingOfGlory");
            });
        }
    }

    public class StartService
    {
        public void Start()
        {
            Console.WriteLine("starting...");
        }
        public void Stop()
        {
            Console.WriteLine("stoping...");
        }
    }
}
```

### install.bat

```
cd /d "%~dp0"
KingOfGlory.Host.exe install
net start KingOfGlory
cmd
```

### uninstall.bat

```
cd /d "%~dp0"
KingOfGlory.Host.exe uninstall
cmd
```



