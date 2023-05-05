## Mac OS使用launchctl命令添加定时任务

> 参考文章：
>
> https://jishuin.proginn.com/p/763bfbd58025
>
> https://chendoing.github.io/mac/macos/tools/2020/11/25/macos-launchctl/



`launchctl`是通过 `.plist` 来得知系统中有哪些东西需要被管理的。*所以简单的来说，想要新增被管理项，本质上就是新增一个*.plist放入苹果的管理文件夹下，然后使其被加载后执行。

### 1. 文件存放位置

```shell
~/Library/LaunchAgents          # 当前用户定义的任务
/Library/LaunchAgents           # 系统管理员定义的任务
/Library/LaunchDaemons          # 管理员定义的系统守护进程任务
/System/Library/LaunchAgents    # 苹果定义的任务
/System/Library/LaunchDaemons   # 苹果定义的系统守护进程任务
```

注意：最好不要使用下面两个位置的（苹果定义的），我这里使用~/Library/LaunchAgents目录

### 2. 编写.plist文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict> 
  <key>Label</key>
  <string>com.zhaixiaobin.icc-project.plist</string>
  <key>ProgramArguments</key>
  <array>
    <string>/Users/shell/git_batch.sh</string>
  </array>
  <!-- 指定要运行的时间 -->
  <key>StartCalendarInterval</key>
  <dict>
        <key>Minute</key>
        <integer>0</integer>
        <key>Hour</key>
        <integer>20</integer>
  </dict>
  <!-- 标准输出文件 -->
  <key>StandardOutPath</key>
  <string>/Users/shell/out.log</string>
  <!-- 标准错误输出文件，错误日志 -->
  <key>StandardErrorPath</key>
  <string>/Users/shell/out.err</string>
</dict>
</plist>
```

plist参数说明：

- Label：对应的需要保证全局唯一性；
- Program：要运行的程序；
- ProgramArguments：命令语句
- StartCalendarInterval：运行的时间，单个时间点使用dict，多个时间点使用 array <dict>
- StartInterval：时间间隔，与StartCalendarInterval使用其一，单位为秒
- StandardInPath、StandardOutPath、StandardErrorPath：标准的输入输出错误文件，这里建议不要使用 .log 作为后缀，会打不开里面的信息。
- 定时启动任务时，如果涉及到网络，但是电脑处于睡眠状态，是执行不了的，这个时候，可以定时的启动屏幕就好了。

### 3. 将任务添加到调度列表中

```shell
launchctl load com.zhaixiaobin.icc-project.plist # 加载
launchctl start com.zhaixiaobin.icc-project.plist # 开始任务
```

其他命令：

```shell
launchctl stop com.zhaixiaobin.icc-project.plist # 结束任务
launchctl list | grep 'icc-project' # 查看任务列表, 使用 grep '任务部分名字' 过滤
```

执行流程：

![image-20230505212935165](https://cdn.jsdelivr.net/gh/dongci777/cloudimg@main/data/image-20230505212935165.png)

注意：

> - 如果任务被修改了，那么必须先unload，然后重新load
> - start可以测试任务，这个是立即执行，不管时间到了没有
> - 执行start和unload前，任务必须先load过，否则报错
> - stop可以停止任务



遇到的问题：

> 在执行launchctl list | grep icc-project的时候发现状态列为78（如果不是0的话就说明执行出错了），这个时候可以通过launchctl error 78 命令来查看，输出的是：78: Function not implemented，可以安装以下工具来排查问题

```shell
brew install launchcontrol
```

然后打开软件

![image-20230505221604751](https://cdn.jsdelivr.net/gh/dongci777/cloudimg@main/data/image-20230505221604751.png)

意思就是没有权限执行该脚本文件，执行：`chmod 744 xxx.sh`，然后重新加载，重新运行。再次打开软件，就是running中了

![image-20230505221930230](https://cdn.jsdelivr.net/gh/dongci777/cloudimg@main/data/image-20230505221930230.png)