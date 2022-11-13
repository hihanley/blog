# Docker

## MongoDB

```yml
version: "3"

services:
  mongo:
    container_name: "mongo"
    image: "mongo"
    restart: "always"
    ports:
      - "27017:27017"
    environment:
      "MONGO_INITDB_ROOT_USERNAME": root
      "MONGO_INITDB_ROOT_PASSWORD": root

  mongo-express:
    container_name: "mongo-express"
    image: "mongo-express"
    restart: "always"
    ports:
      - "8317:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: "root"
      ME_CONFIG_MONGODB_ADMINPASSWORD: "root"
      ME_CONFIG_MONGODB_ENABLE_ADMIN: "true"
      ME_CONFIG_MONGODB_URL: "mongodb://root:root@mongo:27017/"
```

## MySQL

> Support arm64.  
> Need to create folders manually.

```text
mysql
├── lib
├── log
└── docker-compose.yml
```

```yml
version: "3"

services:
  mysql:
    container_name: "mysql"
    image: "mysql/mysql-server:8.0"
    restart: "always"
    command: "--authentication_policy=mysql_native_password"
    environment:
      "MYSQL_ROOT_PASSWORD": "root"
      "MYSQL_ROOT_HOST": "%"
      "TZ": "Asia/Shanghai"
    ports:
      - "3306:3306"
    volumes:
      - "./lib:/var/lib/mysql"
      - "./log:/var/log/mysql"

  phpmyadmin:
    container_name: "phpmyadmin"
    image: "phpmyadmin:5"
    restart: "always"
    ports:
      - "8306:80"
    environment:
      - PMA_HOSTS=mysql
      - PMA_USER=root
      - PMA_PASSWORD=root
```

## Redis

> Support arm64.  
> Need to create folders manually.

```text
redis
├── data
└── docker-compose.yml
```

```yml
version: "3"

services:
  redis:
    container_name: "redis"
    image: "redis:6"
    restart: "always"
    command: "redis-server --appendonly yes"
    ports:
      - "6379:6379"
    volumes:
      - "./data:/data"
  
  phpredisadmin:
    container_name: "phpredisadmin"
    image: "hopsoft/phpredisadmin:latest"
    restart: "always"
    ports:
      - "8379:80"
    environment:
      - REDIS_1_HOST=redis
```
