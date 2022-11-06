# Ubuntu

## Ubuntu 20.04设置静态IP

Ubuntu从`17.10` 开始，配置写在`/etc/netplan/01-netcfg.yaml` 或者类似名称的`yaml` 文件里。

1. 查看网卡设备号：`ip a`
2. 修改`yaml`文件：`sudo nano /etc/netplan/xxx.yaml`

```yaml
network:
  ethernets:
    ens32:
      addresses: [192.168.11.3/24]
      gateway4: 192.168.11.2
      nameservers:
        addresses: [1.1.1.1, 114.114.114.114]
  version: 2
```

最后执行：`sudo netplan apply`
