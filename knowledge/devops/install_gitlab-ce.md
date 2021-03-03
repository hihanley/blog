# Docker-Compose安装Gitlab-CE
`UPDATE: 2021年03月02日`

> 参考：https://docs.gitlab.com/omnibus/docker/#installation

## docker-compose.yml
```
version: '3'

services:
  web:
    image: 'gitlab/gitlab-ce:latest'
    restart: 'always'
    hostname: '192.168.80.145'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://192.168.80.145:11080'
        gitlab_rails['gitlab_shell_ssh_port'] = 11022
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '11080:11080'
      - '11022:22'
    volumes:
      - './config:/etc/gitlab'
      - './logs:/var/log/gitlab'
      - './data:/var/opt/gitlab'
```