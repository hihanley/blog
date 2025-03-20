# Docker

## MongoDB

```yml
services:
  mongo:
    container_name: "mongo"
    image: "mongo"
    restart: "always"
    ports:
      - "27017:27017"
    environment:
      "MONGO_INITDB_ROOT_USERNAME": root
      "MONGO_INITDB_ROOT_PASSWORD": password

  mongo-express:
    container_name: "mongo-express"
    image: "mongo-express"
    restart: "always"
    ports:
      - "8081:8081"
    environment:
      # Basic Auth
      ME_CONFIG_BASICAUTH: "true" 
      ME_CONFIG_BASICAUTH_USERNAME: "root"
      ME_CONFIG_BASICAUTH_PASSWORD: "password"
      ME_CONFIG_MONGODB_URL: "mongodb://root:password@mongo:27017/"
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
services:
  mysql:
    container_name: "mysql"
    image: "mysql/mysql-server:8.0"
    restart: "always"
    command: "--authentication_policy=mysql_native_password"
    environment:
      "MYSQL_ROOT_PASSWORD": "password"
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
      - "80:80"
    environment:
      - PMA_HOSTS=mysql
      # 如果需要手动登录 则注释以下两行
      - PMA_USER=root
      - PMA_PASSWORD=password
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
services:
  redis:
    container_name: "redis"
    image: "redis:6"
    restart: "always"
    command: "redis-server --appendonly yes --requirepass password"
    ports:
      - "6379:6379"
    volumes:
      - "./data:/data"
  
  phpredisadmin:
    container_name: "phpredisadmin"
    image: "erikdubbelboer/phpredisadmin"
    restart: "always"
    ports:
      - "80:80"
    environment:
      - REDIS_1_HOST=redis
      - REDIS_1_AUTH=password
      # Basic Auth
      - ADMIN_USER=root
      - ADMIN_PASS=password
```

## Kafka

> Need to create folders manually.

```text
kafka
├── data
├── zoo_data
└── docker-compose.yml
```

```yml
services:
  zoo:
    container_name: "zoo"
    image: "bitnami/zookeeper"
    restart: "always"
    volumes:
      - "./zoo_data:/bitnami"
    environment:
      - ALLOW_ANONYMOUS_LOGIN=yes

  kafka:
    container_name: "kafka"
    image: "bitnami/kafka"
    restart: "always"
    ports:
      - "9092:9092"
    volumes:
      - "./data:/bitnami"
    environment:
      - KAFKA_CFG_ZOOKEEPER_CONNECT=zoo:2181
      - ALLOW_PLAINTEXT_LISTENER=yes
      - KAFKA_CLIENT_USERS=user
      - KAFKA_CLIENT_PASSWORDS=password
    depends_on:
      - zoo
```
