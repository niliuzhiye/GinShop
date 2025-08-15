# 🛒 小米商城微服务电商系统

<div align="center">
  <img src="https://img.shields.io/badge/Go-1.17+-00ADD8?style=for-the-badge&logo=go" alt="Go Version"/>
  <img src="https://img.shields.io/badge/Gin-Web_Framework-00ADD8?style=for-the-badge&logo=gin" alt="Gin Framework"/>
  <img src="https://img.shields.io/badge/gRPC-Microservices-326CE5?style=for-the-badge&logo=grpc" alt="gRPC"/>
  <img src="https://img.shields.io/badge/Consul-Service_Discovery-F24C53?style=for-the-badge&logo=consul" alt="Consul"/>
  <img src="https://img.shields.io/badge/MySQL-8.0+-4479A1?style=for-the-badge&logo=mysql" alt="MySQL"/>
  <img src="https://img.shields.io/badge/Redis-Cache-DC382D?style=for-the-badge&logo=redis" alt="Redis"/>
  <img src="https://img.shields.io/badge/Docker-Container-2496ED?style=for-the-badge&logo=docker" alt="Docker"/>
</div>

## 📋 项目简介

这是一个基于Go语言和微服务架构构建的现代化电商系统，以小米商城为原型，采用了完整的微服务设计模式。系统集成了商品管理、订单处理、用户系统、支付集成、权限控制等电商核心功能。

### ✨ 核心特性

- 🏗️ **微服务架构**: 基于 go-micro v4 构建的分布式微服务系统
- 🔍 **服务发现**: 使用 Consul 进行服务注册、发现和配置管理
- 🔐 **权限控制**: 基于 RBAC 的细粒度权限管理系统
- 💳 **支付集成**: 支持支付宝、微信支付等多种支付方式
- 📦 **缓存系统**: Redis 缓存提升系统性能
- 🖼️ **文件管理**: 支持本地存储和阿里云 OSS 对象存储
- 🐳 **容器化**: Docker Compose 一键部署
- 🎯 **高性能**: 合理的架构设计和性能优化

## 🏗️ 技术架构

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   用户前台界面    │    │   管理后台界面    │    │     API接口      │
│   (Frontend)   │    │   (Admin Panel) │    │   (API Layer)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
              ┌───────────────────────────────────┐
              │           API Gateway             │
              │        (Gin Web Server)          │
              └───────────────────────────────────┘
                                  │
                     ┌────────────┴────────────┐
                     │       Consul           │
                     │   (服务注册与发现)       │
                     └─────────────────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        │                        │                        │
┌───────▼────────┐    ┌─────────▼────────┐    ┌─────────▼────────┐
│  RBAC 微服务    │    │ Captcha 微服务   │    │ Captcha Client  │
│ (权限管理)      │    │  (验证码服务)     │    │   (验证码客户端)  │
└────────────────┘    └─────────────────┘    └─────────────────┘
        │                        │                        │
        └────────────────────────┼────────────────────────┘
                                  │
              ┌───────────────────────────────────┐
              │           Data Layer             │
              │   MySQL + Redis + File Storage   │
              └───────────────────────────────────┘
```

## 🛠️ 技术栈

| 分类 | 技术 | 版本 | 说明 |
|------|------|------|------|
| **语言** | Go | 1.17+ | 主要开发语言 |
| **Web框架** | Gin | v1.7.7 | HTTP服务器和路由 |
| **微服务** | go-micro | v4.9.0 | 微服务框架 |
| **服务发现** | Consul | latest | 服务注册发现 |
| **通信协议** | gRPC/Protobuf | - | 微服务间通信 |
| **数据库** | MySQL | 8.0+ | 主数据库 |
| **缓存** | Redis | 6.0+ | 缓存系统 |
| **ORM** | GORM | v1.22.4 | 数据库ORM |
| **容器化** | Docker/Docker Compose | - | 容器化部署 |
| **支付** | 支付宝/微信支付 | - | 第三方支付 |

## 📁 项目结构

```
xiaomishop/
├── client/                          # 客户端应用
│   ├── captcha-client/              # 验证码客户端微服务
│   │   ├── Dockerfile
│   │   ├── go.mod
│   │   ├── main.go
│   │   └── Makefile
│   ├── ginshop/                     # 主电商应用
│   │   ├── conf/                    # 配置文件
│   │   │   └── app.ini
│   │   ├── controllers/             # 控制器层
│   │   │   ├── admin/              # 后台管理控制器
│   │   │   ├── api/                # API控制器
│   │   │   └── itying/             # 前台业务控制器
│   │   ├── middlewares/            # 中间件
│   │   │   ├── adminAuth.go        # 管理员权限中间件
│   │   │   └── userAuth.go         # 用户权限中间件
│   │   ├── models/                 # 数据模型
│   │   ├── proto/                  # gRPC协议定义
│   │   ├── routers/                # 路由配置
│   │   ├── static/                 # 静态资源
│   │   ├── templates/              # 模板文件
│   │   └── main.go                 # 主程序入口
│   └── ginWebApi/                   # Web API服务
│       ├── controllers/
│       ├── models/
│       ├── routers/
│       └── main.go
├── server/                          # 服务端微服务
│   ├── captcha/                     # 验证码微服务
│   │   ├── Dockerfile
│   │   ├── go.mod
│   │   ├── handler/
│   │   ├── proto/
│   │   └── main.go
│   └── rbac/                        # 权限管理微服务
│       ├── conf/                    # 配置文件
│       │   └── app.ini
│       ├── handler/                 # 服务处理器
│       │   ├── rbac.go
│       │   ├── rbacLogin.go
│       │   ├── rbacManager.go
│       │   └── rbacRole.go
│       ├── models/                  # 数据模型
│       ├── proto/                   # gRPC协议定义
│       └── main.go                  # 微服务启动文件
└── docker-compose.yml               # Docker编排文件
```

## 🚀 快速开始

### 环境要求

- Go 1.17+
- MySQL 8.0+
- Redis 6.0+
- Docker & Docker Compose

### 安装步骤

1. **克隆项目**
```bash
git clone https://github.com/your-username/xiaomishop.git
cd xiaomishop
```

2. **配置环境**
```bash
# 修改配置文件
cp client/ginshop/conf/app.ini.example client/ginshop/conf/app.ini
cp server/rbac/conf/app.ini.example server/rbac/conf/app.ini

# 编辑配置文件，修改数据库连接等信息
```

3. **使用 Docker Compose 启动**
```bash
# 启动所有服务
docker-compose up -d

# 查看服务状态
docker-compose ps
```

4. **手动编译启动（可选）**
```bash
# 启动 RBAC 微服务
cd server/rbac
go mod tidy
go run main.go

# 启动验证码微服务
cd server/captcha
go mod tidy
go run main.go

# 启动主应用
cd client/ginshop
go mod tidy
go run main.go
```

### 访问地址

- **前台商城**: http://localhost:8080
- **后台管理**: http://localhost:8080/admin
- **API接口**: http://localhost:3000
- **Consul控制台**: http://localhost:8500

### 默认账号

- **管理员账号**: admin / 123456

## 🔧 配置说明

### 主应用配置 (`client/ginshop/conf/app.ini`)

```ini
app_name = 小米商城
log_level = DEBUG
admin_path = /admin
excludeAuthPath = "/,/welcome,/loginOut"

[mysql]
ip = 127.0.0.1
port = 3306
user = root
password = 123456
database = ginxiaomi

[redis]
ip = localhost
port = 6379
redisEnable = true

[oss]
status = 0  # 0: 本地存储, 1: 阿里云OSS
```

### RBAC微服务配置 (`server/rbac/conf/app.ini`)

```ini
app_name = rbac

[mysql]
ip = 127.0.0.1
port = 3306
user = root
password = 123456
database = ginxiaomirbac

[consul]
addr = 127.0.0.1:8500
```

## 📚 核心功能

### 🛍️ 电商功能
- **商品管理**: 商品增删改查、分类管理、库存管理
- **订单系统**: 订单创建、状态跟踪、订单查询
- **购物车**: 添加商品、数量调整、批量操作
- **用户系统**: 用户注册登录、个人信息、收货地址
- **支付集成**: 支付宝支付、微信支付、支付回调

### 🔐 权限管理
- **RBAC模型**: 用户-角色-权限三层模型
- **细粒度控制**: URL级别的权限控制
- **动态菜单**: 基于权限的菜单动态生成
- **权限中间件**: 自动权限检查和拦截

### 📊 系统功能
- **缓存系统**: Redis缓存热点数据
- **文件上传**: 支持图片上传和缩略图生成
- **验证码**: 图形验证码防止机器人
- **模板渲染**: 支持模板函数和数据绑定

## 🔌 API 文档

### 微服务接口

#### RBAC 权限服务

```protobuf
// 用户登录
service RbacLogin {
    rpc Login(LoginRequest) returns (LoginResponse)
}

// 角色管理
service RbacRole {
    rpc RoleGet(RoleGetRequest) returns (RoleGetResponse)
    rpc RoleAdd(RoleAddRequest) returns (RoleAddResponse)
    rpc RoleAuth(RoleAuthRequest) returns (RoleAuthResponse)
    rpc MiddlewaresAuth(MiddlewaresAuthRequest) returns (MiddlewaresAuthResponse)
}

// 管理员管理
service RbacManager {
    rpc ManagerGet(ManagerGetRequest) returns (ManagerGetResponse)
    rpc ManagerAdd(ManagerAddRequest) returns (ManagerAddResponse)
}
```

#### 验证码服务

```protobuf
service Captcha {
    rpc GenerateCaptcha(GenerateRequest) returns (GenerateResponse)
    rpc VerifyCaptcha(VerifyRequest) returns (VerifyResponse)
}
```

### REST API 接口

#### 商品相关
- `GET /` - 首页商品展示
- `GET /category:id` - 商品分类页面
- `GET /detail` - 商品详情页面
- `GET /product/getImgList` - 获取商品图片列表

#### 购物车相关
- `GET /cart` - 购物车页面
- `GET /cart/addCart` - 添加商品到购物车
- `GET /cart/incCart` - 增加商品数量
- `GET /cart/decCart` - 减少商品数量
- `GET /cart/delCart` - 删除购物车商品

#### 订单相关
- `GET /buy/checkout` - 订单结算页面
- `POST /buy/doCheckout` - 提交订单
- `GET /buy/pay` - 支付页面
- `GET /buy/orderPayStatus` - 查询支付状态

#### 支付相关
- `GET /alipay` - 支付宝支付
- `POST /alipayNotify` - 支付宝回调
- `GET /wxpay` - 微信支付
- `POST /wxpay/notify` - 微信支付回调

## 🧪 测试

```bash
# 运行测试
go test ./...

# 测试覆盖率
go test -cover ./...

# 基准测试
go test -bench=. ./...
```

## 📦 部署

### Docker 部署

```bash
# 构建镜像
docker-compose build

# 启动服务
docker-compose up -d

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down
```

### 生产环境部署

1. **环境配置**
```bash
# 设置环境变量
export GO_ENV=production
export MYSQL_HOST=your-mysql-host
export REDIS_HOST=your-redis-host
export CONSUL_HOST=your-consul-host
```

2. **数据库初始化**
```sql
-- 创建数据库
CREATE DATABASE ginxiaomi CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE DATABASE ginxiaomirbac CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- 导入数据表结构
mysql -u root -p ginxiaomi < database/ginxiaomi.sql
mysql -u root -p ginxiaomirbac < database/ginxiaomirbac.sql
```

3. **编译和部署**
```bash
# 编译各个服务
cd server/rbac && go build -o rbac main.go
cd server/captcha && go build -o captcha main.go
cd client/ginshop && go build -o ginshop main.go

# 使用进程管理器启动
pm2 start ecosystem.config.js
```

## 🔍 监控

### 健康检查

- Consul: http://localhost:8500/ui
- 应用健康检查: http://localhost:8080/health
- 微服务状态: 通过 Consul 服务注册状态查看

### 日志管理

```bash
# 查看应用日志
docker-compose logs -f ginshop

# 查看微服务日志
docker-compose logs -f rbac
docker-compose logs -f captcha
```
