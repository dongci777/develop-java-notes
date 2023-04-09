## 一、编辑 .bashrc文件

```powershell
vim ~/.bashrc
```

## 二、在文件的结尾加入以下脚本

```powershell
function git_branch {
   branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
   if [ "${branch}" != "" ];then
       if [ "${branch}" = "(no branch)" ];then
           branch="(`git rev-parse --short HEAD`...)"
       fi
       echo " ($branch)"
   fi
}
export PS1='\u@\h \[\033[01;36m\]\W\[\033[01;32m\]$(git_branch)\[\033[00m\] \$ '
```

## 三、保存退出 

```powershell
:wq
```

## 四、执行以下命令

```powershell
source ./.bashrc
```

## 五、为了每次开机有效，需要高速mac开机后需要先执行该配置

```powershell
echo "[ -r ~/.bashrc ] && source ~/.bashrc" >> .bash_profile
```