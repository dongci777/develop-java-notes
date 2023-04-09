> 问题：
>
> 报错：cd: no such file or directory: /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core

## 一、创建homebrew目录并下载

```powershell
cd /usr/local/Homebrew/Library/Taps
mkdir homebrew 
cd homebrew
git clone https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```

## 二、替换homebrew源 （更换为清华北大镜像）

```powershell
cd "$(brew --repo)"
git remote set-url origin git://mirrors.ustc.edu.cn/brew.git
```

## 三、替换homebrew-core源

```powershell
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git
```

## 四、brew更新

```powershell
brew update
```