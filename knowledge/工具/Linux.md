# Linux

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

## 配置最大打开文件数

1. 修改 `/etc/sysctl.conf` 添加以下内容

    ```text
    fs.file-max = 2000000
    fs.inotify.max_user_watches=524288
    ```

2. 修改 `/etc/security/limits.conf` 添加以下内容

    ```text
    * soft     nproc          65535
    * hard     nproc          65535
    * soft     nofile         65535
    * hard     nofile         65535
    root soft     nproc          65535
    root hard     nproc          65535
    root soft     nofile         65535
    root hard     nofile         65535
    ```

3. 修改 `/etc/systemd/system.conf` 和 `/etc/systemd/user.conf`，找到 `DefaultLimitNOFILE` 这一行，删除前面的注释，修改为 `DefaultLimitNOFILE=65535`

4. 修改 `/etc/pam.d/common-session` 添加 `session required        pam_limits.so`

5. 配置完成之后，重启系统即可
