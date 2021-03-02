# Docker安装Gitlab-Runner
`UPDATE: 2021年03月02日`

> 安装参考：https://docs.gitlab.com/runner/install/docker.html

> 配置参考：https://docs.gitlab.com/runner/register/index.html#docker

## 简单步骤
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