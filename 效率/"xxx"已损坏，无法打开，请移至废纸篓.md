解决方法：

执行以下命令

```bash
sudo xattr -d com.apple.quarantine 你的软件

eg：sudo xattr -d com.apple.quarantine /Applications/XMind\ ZEN.app
```

操作方式是，打开iterm，然后输入：sudo xattr -d com.apple.quarantine命令之后，空一格，然后打开“应用程序”，然后找到对应的软件将其拖入到iterm对话框中即可。