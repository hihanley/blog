# KeePass

## 使用KeePass保存SSH Keys并在Windows10中使用KeePass的KeeAgent插件作为SSH-Agent且支持Git

1. 在Windows10的服务中停止并禁用`OpenSSH Authentication Agent`服务  
2. 设置KeeAgent为Agent Mode，勾选`Enable agent for Windows OpenSSH`，勾选`Create Cygwin compatible socket file`，设置路径为`C:\Users\{UserName}\AppData\Local\Temp\cyglockfile`  
3. 设置系统环境变量`SSH_AUTH_SOCK`为刚刚设置的路径
4. 进入Git Bash中测试：`ssh -T git@github.com`
5. 如果不生效，则在第二步中同时勾选`Create msysGit compatible socket file`，设置路径为`C:\Users\{UserName}\AppData\Local\Temp\syslockfile`，然后将`SSH_AUTH_SOCK`设置为这个路径再测试
