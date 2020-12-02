# PyCharm修改Terminal为PowerShell后未激活正确Conda环境的问题

`2020年12月2日`

**问题**：PyCharm修改Terminal为PowerShell后，打开Terminal一直激活base环境，而不是项目设置的虚拟环境。  

**原因**：MiniConda安装完后，如果执行了`conda init`，会在PowerShell启动时自动激活base环境，而PyCharm打开Terminal时也会自动激活当前项目的虚拟环境，只是PyCharm的激活动作在前，PowerShell启动时激活动作在后，所以激活的实际上是base环境。

**解决方法**：执行`conda config --set auto_activate_base false`关闭PowerShell启动时自动激活base环境。