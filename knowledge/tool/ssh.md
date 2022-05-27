# SSH

## SSH config template

```text
Host *
  ServerAliveInterval 60
  ServerAliveCountMax 3
  AddKeysToAgent yes
  ForwardAgent no

Host host
  HostName hostname
  User user
  Port port
  IdentityFile ~/.ssh/file
```

## Multi ssh key for same host

```text
Host github
  HostName github.com
  User git
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/file_a

Host github-other.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/file_b

# eg：github:user/project.git
# eg：git@github-other.com:user/project.git
```

## Windows unable to start ssh-agent service, error :1058

win+R打开services查看 “OpenSSH Authentication Agent” 服务是否开启，如果是 “disabled”（可能是win10自动更新给仅用了） 则将服务设为"Automatic"然后开启服务即可

## KeepassXC Agent protocol error when adding ssh key

only occur when you require user confirmation（取消勾选请求用户确认）
