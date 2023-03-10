# 一、安装 zsh

为什么选择zsh？

答：zsh支持一系列的自定义插件和主题

传统的shell就是“黑窗户”下的命令行，程序员可以通过shell命令来控制系统的行为，比如进入某个目录，创建、删除某个文件等.

bash是shell的一个改进版本，也是现在非常流行的.一般默认安装在系统内，可以通过bash --version来查看版本信息，除了bash，还有很多其他的一些魔改版本，比如今天要安装的zsh

注：zsh一般是mac默认安装的，可以通过zsh --version来查看响应的信息

## 1、使用brew安装zsh

```shell
brew install zsh

# 安装完的路径
/usr/local/Cellar/zsh/5.9
```

## 2、切换zsh shell

```powershell
echo $SHELL

/bin/zshc
```

查看已经安装的shell

```powershell
cat /etc/shells

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

切换zsh

```powershell
chsh -s /bin/zsh
```

然后重启终端即可使用zsh.接下来就是安装oh-my-zsh了

# 二、安装终端iTerm2

一般终端有以下几种：

1、mac自带的terminal（丑、功能单一）

2、windows terminal

3、iTerm2（mac推荐）

4、xshell，putty

5、跨平台的Hyper等

官网：https://iterm2.com/

# 三、安装 oh-my-zsh

## 1、使用脚本一键安装

```powershell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# 国内源
sh -c "$(curl -fsSL https://gitee.com/Devkings/oh_my_zsh_install/raw/master/install.sh)"
```

![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/oh-my-zsh-00.png)

安装完成之后，在我们的用户目录下面有一个.oh-my-zsh目录

```powershell
cd ~/.oh-my-zsh
```

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/%E5%AE%89%E8%A3%85oh-my-zsh-01.png)

- plugins：插件目录
- themes：主题目录

## 2、配置文件 .zshrc

在根目录下，有一个隐藏文件.zshrc，这里面就是一系列的配置，后面我们会配置对应的内容

## 3、卸载

如果之前安装了oh-my-zsh，可以通过以下操作来卸载

```powershell
# 进入根目录
cd ~

# 进入tools目录
cd .oh-my-zsh/tools

# 卸载
sh uninstall.sh
```

# 四、配置主题颜色

配置主题颜色主要分为两个部分，第一个部分是命令iterm2本身的背景、文件夹等颜色。第二个部分就是命令行的显示展示配置，这个属于zsh的配置，这两个部分一起构成了终端的主题

## 1、配置iTerm2

### 1.1、颜色配置

打开iterm，然后按住command+.打开首选项，然后选择Profiles-> Colors ，选中右下方的Color Presets，可以选择默认的配色方案或者在线下载其他配色主题方案，我这里安装的是Ayu Mirage.

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/Iterm2%E9%85%8D%E8%89%B2%E9%85%8D%E7%BD%AE-01.png)

### 1.2、字体设置

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/Iterm2%E5%AD%97%E4%BD%93%E9%85%8D%E7%BD%AE-01.png)



## 2、安装powerlevel10k主题插件

### 2.1、下载主题

```powershell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### 2.2、配置.zshrc文件

```powershell
ZSH_THEME="powerlevel10k/powerlevel10k"
```

第一次配置完这个插件之后，会默认安装一个字体MesloLGS NF，这个字体来自一个特殊的字体家族：https://www.nerdfonts.com。可以展示非常多的图标

![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/powerlevel10k%E9%85%8D%E7%BD%AE.png)

### 2.3、自定义配置命令行样式

我们输入以下命令自定义配置我们的命令行样式了

```powershell
p10k configure
```

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/powerlevel10k%E9%85%8D%E7%BD%AE-01.png)

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/powerlevel10k%E9%85%8D%E7%BD%AE-02.png)

# 五、安装插件

## 1、zsh-autosuggestions

```powershell
git clone https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

## 2、zsh-syntax-highlighting

```powershell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

安装完插件之后，只需要配置.zshrc文件的plugins属性即可

```powershell
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

# 六、IDEA 设置

## 1、设置Terminal终端

 

## 2、设置代码字体

Preference -> Editor -> Font

- Font：JetBrains Mono
- Size：14
- Line height：1.2

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/IDEA%20Terminal%E8%AE%BE%E7%BD%AE.png)



## 3、设置console字体

Preference -> Editor -> Color Scheme -> Console Font

- Scheme：Dark purple
- Font：MesloLGS NF
- Size：14
- Line height：1.2

 ![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/IDEA%E8%AE%BE%E7%BD%AE%E5%AD%97%E4%BD%93.png)

# 七、VsCode设置

![img](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/VsCode%20Terminal%E9%85%8D%E7%BD%AE.png)

# 八、安装Fig

```powershell
brew install fig
```

![image-20230124003328225](https://cdn.jsdelivr.net/gh/dongci777/cloudimg/data/%E5%AE%89%E8%A3%85Fig.png)

安装完之后，运行，就可以在各种开发IDE的终端下面进行一个命令提示，也有其他一些比如Script、CLI等功能



# 九、问题

1、Fix Oh My Zsh “Insecure completion-dependent directories detected”

```
ZSH_DISABLE_COMPFIX=true
```

