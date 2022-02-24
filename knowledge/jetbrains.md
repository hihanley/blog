# JetBrains

## projector on linux-arm64

1. install jdk. 
2. install projector: https://github.com/JetBrains/projector-installer#Installation. 
3. use projector to install ide: https://github.com/JetBrains/projector-installer/blob/master/COMMANDS.md#ide-commands.  
  example: `projector ide autoinstall --config-name idea --ide-name "IntelliJ IDEA Ultimate 2021.3" --port 8080`
4. secure the ide connection: https://github.com/JetBrains/projector-installer/blob/master/COMMANDS.md#install-https-certificate
5. support arm64: https://youtrack.jetbrains.com/articles/IDEA-A-48/JetBrains-IDEs-on-AArch64#linux
6. option - crack: https://springboot.io/t/topic/4592
7. option - create systemd service: https://youtrack.jetbrains.com/issue/PRJ-298

## PyCharm修改Terminal为PowerShell后未激活正确Conda环境的问题

**问题**：PyCharm修改Terminal为PowerShell后，打开Terminal一直激活base环境，而不是项目设置的虚拟环境。  

**原因**：MiniConda安装完后，如果执行了`conda init`，会在PowerShell启动时自动激活base环境，而PyCharm打开Terminal时也会自动激活当前项目的虚拟环境，只是PyCharm的激活动作在前，PowerShell启动时激活动作在后，所以激活的实际上是base环境。

**解决方法**：执行`conda config --set auto_activate_base false`关闭PowerShell启动时自动激活base环境。