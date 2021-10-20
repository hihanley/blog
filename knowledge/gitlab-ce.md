# GitLab-CE

## Docker-Compose安装Gitlab-CE

> 参考：https://docs.gitlab.com/omnibus/docker/#installation

`docker-compose.yml`
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


## Docker安装Gitlab-Runner

> 安装参考：https://docs.gitlab.com/runner/install/docker.html

> 配置参考：https://docs.gitlab.com/runner/register/index.html#docker

1. 先运行`docker run --rm -it -v {配置目录}/config:/etc/gitlab-runner gitlab/gitlab-runner register`创建配置文件

2. 创建`docker-compose.yml`：

```
version: "3"

services:
  gitlab-runner:
    image: "gitlab/gitlab-runner:latest"
    restart: "always"
    volumes:
      - "{配置目录}/config:/etc/gitlab-runner"
      - "/var/run/docker.sock:/var/run/docker.sock"
```