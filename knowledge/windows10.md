# Windows10

## Windows10调整网络优先级

**问题**：Windows10既连接Wifi又插网线时，电脑会优先使用有线网络，我想优先使用无线网络。  

**解决方法**：修改`接口跃点数`，可以达到想要的效果。执行`Get-NetIPInterface`查询当前所有的网络连接，`InterfaceMetric`列就是接口跃点数。  
执行`Set-NetIPInterface -InterfaceIndex {ifIndex} -InterfaceMetric 10`将你想要使用网络的接口跃点数设置为10即可。  

**参考**: [修改接口跃点数，让Win10优先使用无线网络连接](https://windows10.pro/set-netipinterface-interfaceindex-interfacemetric/)
