# PanCheck 部署完成指南

## 部署状态

✅ PanCheck 网盘链接检测系统已成功部署并运行！

## 服务信息

- **服务地址**: http://localhost:6080
- **管理后台**: http://localhost:6080/admin/login
- **后台密码**: admin123
- **API 健康检查**: http://localhost:6080/api/v1/health

## 数据库信息

- **数据库类型**: MySQL
- **数据库地址**: db.fanjianhui.com:13306
- **数据库名称**: pancheck
- **字符集**: utf8mb4

## 数据库表结构

已创建以下5个数据库表：

1. **submission_records** - 提交记录表
   - 存储用户提交的链接检测记录

2. **invalid_links** - 失效链接表
   - 存储检测到的失效链接

3. **settings** - 设置表
   - 存储系统配置信息

4. **scheduled_tasks** - 定时任务表
   - 存储定时检测任务配置

5. **task_executions** - 任务执行记录表
   - 存储定时任务的执行记录

## 服务管理

### 启动服务

```bash
cd /workspace/projects/pancheck
export PATH=/usr/local/go/bin:$PATH
./bin/main
```

### 后台运行

```bash
cd /workspace/projects/pancheck
export PATH=/usr/local/go/bin:$PATH
nohup ./bin/main > /tmp/pancheck.log 2>&1 &
```

### 停止服务

```bash
pkill -f "bin/main"
```

### 查看日志

```bash
tail -f /tmp/pancheck.log
```

## 配置文件

环境变量配置文件位于: `/workspace/projects/pancheck/.env`

主要配置项：

```env
# 服务器配置
SERVER_PORT=6080
SERVER_MODE=release
SERVER_CORS_ORIGINS=*

# 数据库配置
DATABASE_TYPE=mysql
DATABASE_HOST=db.fanjianhui.com
DATABASE_PORT=13306
DATABASE_USER=root
DATABASE_PASSWORD=Mysql506699
DATABASE_DATABASE=pancheck
DATABASE_CHARSET=utf8mb4

# 检测器配置
CHECKER_DEFAULT_CONCURRENCY=5
CHECKER_TIMEOUT=30

# 管理员密码配置
ADMIN_PASSWORD=admin123
```

## 支持的网盘平台

PanCheck 支持 9 种主流网盘平台的链接检测：

- 夸克网盘
- UC网盘
- 百度网盘
- 天翼云盘
- 123网盘
- 115网盘
- 阿里云盘
- 迅雷云盘
- 中国移动云盘

## API 使用示例

### 检测网盘链接

```bash
curl -X POST http://localhost:6080/api/v1/links/check \
  -H "Content-Type: application/json" \
  -d '{
    "links": [
      "https://pan.baidu.com/s/1example",
      "https://www.aliyundrive.com/s/2example"
    ]
  }'
```

### 登录管理后台

```bash
curl -X POST http://localhost:6080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"password":"admin123"}'
```

## 功能特性

1. **多平台支持** - 支持 9 种主流网盘平台的链接检测
2. **高性能检测** - 支持并发检测，可配置检测频率和超时时间
3. **数据统计** - 提供详细的检测统计和数据分析
4. **定时任务** - 支持创建定时检测任务，自动检测链接有效性
5. **数据持久化** - 使用 MySQL 存储检测记录
6. **现代化界面** - 基于 React + TypeScript 的管理后台

## 故障排查

### 服务无法启动

检查日志查看错误信息：
```bash
cat /tmp/pancheck.log
```

### 数据库连接失败

确认数据库配置是否正确，检查 `.env` 文件中的数据库连接信息。

### 端口被占用

检查 6080 端口是否被其他程序占用：
```bash
netstat -tlnp | grep 6080
```

## 技术栈

- **后端**: Go 1.23 + Gin + GORM
- **前端**: React + TypeScript + Vite
- **数据库**: MySQL 8.0
- **部署**: 二进制文件部署

## 项目文件位置

- **项目目录**: `/workspace/projects/pancheck`
- **后端二进制**: `/workspace/projects/pancheck/bin/main`
- **前端静态文件**: `/workspace/projects/pancheck/static/`
- **配置文件**: `/workspace/projects/pancheck/.env`

---

**部署完成！现在可以访问 http://localhost:6080 开始使用 PanCheck 网盘链接检测系统。**
