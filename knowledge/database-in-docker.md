# Database in docker

> Need to create folders manually

## MySQL

```
mysql
├── lib
├── log
└── docker-compose.yml
```

`docker-compose.yml`
``` yml
version: "3"

services:
  mysql:
    container_name: "mysql"
    image: "mysql"
    restart: "always"
    command: "--default-authentication-plugin=mysql_native_password"
    environment:
      "MYSQL_ROOT_PASSWORD": "root"
      "TZ": "Asia/Shanghai"
    ports:
      - "3306:3306"
    volumes:
      - "./lib:/var/lib/mysql"
      - "./log:/var/log/mysql"

  phpmyadmin:
    container_name: "phpmyadmin"
    image: "phpmyadmin/phpmyadmin"
    restart: "always"
    ports:
      - "13306:80"
    environment:
      - PMA_HOSTS=mysql
      - PMA_USER=root
      - PMA_PASSWORD=root

```

## Redis

```
redis
├── data
└── docker-compose.yml
```

`docker-compose.yml`
```yml
version: "3"

services:
  redis:
    container_name: "redis"
    image: "redis"
    restart: "always"
    command: "redis-server --appendonly yes"
    ports:
      - "6379:6379"
    volumes:
      - "./data:/data"
  
  phpredisadmin:
    container_name: "phpredisadmin"
    image: "erikdubbelboer/phpredisadmin"
    restart: "always"
    ports:
      - "16379:80"
    environment:
      - REDIS_1_HOST=redis
```