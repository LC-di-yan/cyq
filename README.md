# 云聚伙伴平台 (CYQ)

基于 Spring Boot 2.7.x 的伙伴社交平台后端服务，支持用户管理、内容发布、互动社交等核心功能。

## 技术栈

| 类别 | 技术 |
|------|------|
| 后端框架 | Spring Boot 2.7.x, Spring MVC |
| 数据访问 | MyBatis Plus (分页), MySQL |
| 缓存 | Redis, Spring Session |
| 搜索引擎 | Elasticsearch |
| 对象存储 | 腾讯云 COS |
| 接口文档 | Swagger + Knife4j |
| 工具库 | Hutool, Easy Excel, Apache Commons Lang3, Lombok |
| 容器化 | Docker |

## 项目结构

```
src/main/java/com/yupi/springbootinit/
├── annotation/     # 自定义注解（权限校验）
├── aop/            # AOP 切面（鉴权、日志）
├── common/         # 通用响应、错误码
├── config/         # 配置类（跨域、COS、MyBatis、JSON）
├── constant/       # 常量定义
├── controller/     # REST 接口
├── model/          # 实体类、VO、DTO
├── mapper/         # MyBatis Mapper
├── service/        # 业务逻辑层
├── job/            # 定时任务（ES 同步）
├── generate/       # 代码生成器
└── utils/          # 工具类
```

## 核心功能

- **用户系统** — 注册、登录、注销、权限管理（user/admin/ban）
- **内容管理** — 帖子 CRUD、标签、数据库检索 + ES 灵活检索
- **社交互动** — 点赞/取消点赞、收藏/取消收藏
- **数据同步** — 帖子全量/增量同步到 Elasticsearch
- **第三方集成** — 微信开放平台登录、微信公众号消息
- **文件上传** — 分业务文件上传（腾讯云 COS）

## 快速开始

### 环境要求

- JDK 1.8+
- Maven 3.6+
- MySQL 5.7+
- Redis（可选，用于分布式 Session）
- Elasticsearch（可选，用于全文检索）

### 1. 数据库初始化

```bash
mysql -u root -p < sql/create_table.sql
```

### 2. 修改配置

编辑 `src/main/resources/application.yml`，配置数据库连接：

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/my_db
    username: root
    password: your_password
```

### 3. 启动服务

```bash
mvn spring-boot:run

# 或打包后运行
mvn package -DskipTests
java -jar target/springboot-init-0.0.1-SNAPSHOT.jar
```

### 4. 访问接口文档

启动后访问：`http://localhost:8101/api/doc.html`

### Docker 部署

```bash
docker build -t cyq .
docker run -p 8101:8101 cyq
```

## API 概览

| 接口 | 方法 | 说明 |
|------|------|------|
| `/api/user/register` | POST | 用户注册 |
| `/api/user/login` | POST | 用户登录 |
| `/api/user/logout` | POST | 用户注销 |
| `/api/user/update` | PUT | 更新用户信息 |
| `/api/user/search` | GET | 搜索用户（管理员） |
| `/api/post/add` | POST | 发布帖子 |
| `/api/post/delete` | POST | 删除帖子 |
| `/api/post/update` | PUT | 编辑帖子 |
| `/api/post/get` | GET | 获取帖子详情 |
| `/api/post/list/page` | GET | 分页查询帖子 |
| `/api/post/search/page` | GET | ES 搜索帖子 |
| `/api/post_thumb/` | POST | 点赞/取消点赞 |
| `/api/post_favour/` | POST | 收藏/取消收藏 |

## 致谢

项目基于 [程序员鱼皮](https://github.com/liyupi) 的 [springboot-init](https://github.com/liyupi/springboot-init) 模板开发。
