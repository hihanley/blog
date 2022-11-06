# SSH

## 使SSH通过HTTP代理或者SOCKS5代理

直接配置

```bash
ssh -o ProxyCommand="nc -X 5 -x 127.0.0.1:1080 %h %p" root@server
```

配置文件方式

```text
Host *
    ProxyCommand nc -X 5 -x 127.0.0.1:1080 %h %p
```

## 清除SSH登录记录等

`/var/log/wtmp` last 登录成功日志，包含用户名、IP 地址和时间记录

`/var/log/btmp` lastb 登录失败日志，包含信息同上

`/var/log/lastlog` lastlog 各用户的最近登录日志

`/var/log/secure` 用 cat查看 各类需要输入口令的登录日志

```bash
cat /dev/null > /var/log/wtmp
cat /dev/null > /var/log/btmp
cat /dev/null > /var/log/lastlog
cat /dev/null > /var/log/secure
```

清除所有历史命令记录，第二条命令表示立即更新日志文件

```bash
history -c
history -w
```
