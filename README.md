# Compose - Docker Compose 配置集合

这个项目提供了一系列Docker Compose配置文件，用于在不同场景下部署禅道项目管理系统。

## 项目结构

```
├── baisc/
│   ├── docker-compose.yml              # 基础配置
│   ├── docker-compose-cache.yml        # 带Redis缓存的配置
│   ├── docker-compose-cache-web.yml    # 带Redis缓存和Traefik的配置
│   └── docker-compose-replication.yml  # 数据库主从复制配置
└── README.md                            # 文档
```

## 配置文件说明

> 所用配置都可以根据自己的实际情况进行灵活修改。

### 基础配置 (docker-compose.yml)

提供基本的禅道应用和MariaDB数据库服务：
- **zentao-db**: 使用bitnami/mariadb:10.6镜像的数据库服务
- **zentao**: 使用easysoft/zentao镜像的禅道应用服务

### 缓存配置 (docker-compose-cache.yml)

在基础配置上增加了Redis缓存服务：
- **zentao-db**: MariaDB数据库服务
- **zentao**: 禅道应用服务
- **zentao-redis**: Redis缓存服务

### 缓存+Web界面配置 (docker-compose-cache-web.yml)

在缓存配置的基础上增加了Traefik作为反向代理：
- **zentao-db**: MariaDB数据库服务
- **zentao**: 禅道应用服务
- **zentao-redis**: Redis缓存服务
- **traefik**: Traefik反向代理，提供Web访问界面

### 主从复制配置 (docker-compose-replication.yml)

配置了MariaDB的主从复制，提高数据库可用性：
- **zentao-db-primary**: 主数据库服务
- **zentao-db-secondary**: 从数据库服务
- **zentao**: 禅道应用服务

## 使用说明

### 基础配置

```bash
cd baisc
docker-compose up -d
```

### 带缓存的配置

```bash
cd baisc
docker-compose -f docker-compose-cache.yml up -d
```

### 带缓存和Web界面的配置

```bash
cd baisc
docker-compose -f docker-compose-cache-web.yml up -d
```

### 数据库主从复制配置

```bash
cd baisc
docker-compose -f docker-compose-replication.yml up -d
```

## 许可证

本项目采用 [Apache License 2.0](LICENSE) 许可证。
