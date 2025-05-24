# Discord论坛搜索机器人

一个功能强大的Discord机器人，专为大型服务器设计，提供高级论坛帖子搜索和内容管理功能。通过高效的缓存系统和优化的搜索算法，即使在拥有大量用户和帖子的服务器中也能保持出色性能。

## 功能特点

- **高级搜索语法**：支持AND、OR、NOT等复杂逻辑操作符和精确短语匹配
- **多维度过滤**：按标签、作者、日期范围、反应数和回复数等多条件筛选
- **智能排序**：支持8种排序方式，包括反应数、回复数、发帖时间和最后活跃时间
- **实时搜索进度**：搜索过程中显示实时进度和统计信息，支持取消长时间运行的搜索
- **分页浏览结果**：直观的界面控制，轻松浏览大量搜索结果
- **自动完成建议**：输入时提供智能建议，优先显示最近使用的选项
- **搜索历史记录**：保存用户最近的搜索记录，方便重复查询
- **性能监控系统**：内置详细的性能统计和资源使用监控
- **大型服务器优化**：专为高流量大型服务器(10000+用户)设计，支持Redis缓存

## 安装说明

### 环境要求

- Python 3.11.x
- Discord.py v2.3+
- 可选：Redis服务器（用于高级缓存）
- 机器人需要的权限：
  - 读取消息
  - 发送消息
  - 嵌入链接
  - 添加反应
  - 读取消息历史
  - 查看频道

### 安装步骤

1. 克隆项目仓库：

    ```bash
    git clone https://github.com/yourusername/discord-forum-search-bot.git
    cd discord-forum-search-bot
    ```

2. 安装依赖项：

    ```bash
    pip install -r requirements.txt
    ```

3. 创建并配置环境变量文件(`.env`)：

    ```env
    DISCORD_TOKEN=your_bot_token_here
    ```

4. 运行机器人：

    ```bash
    python main.py
    ```

### Docker部署（推荐用于生产环境）

使用Docker Compose快速部署（包含Redis缓存）：

```bash
# 配置环境变量
echo "DISCORD_TOKEN=your_bot_token_here" > .env

# 启动服务
docker-compose up -d
```

## 使用指南

### 搜索命令

基本搜索：

```bash
/forum_search forum_name:[论坛名称] search_word:[搜索关键词]
```

高级搜索语法：

- AND搜索: `term1 AND term2` 或 `term1 & term2`
- OR搜索: `term1 OR term2` 或 `term1 | term2`
- NOT搜索: `NOT term` 或 `-term`
- 精确短语: `"exact phrase"`
- 组合使用: `(term1 OR term2) AND NOT term3`

多条件过滤：

```bash
/forum_search forum_name:[论坛名称] tag1:[标签1] tag2:[标签2] original_poster:[用户] min_reactions:[数量] start_date:[日期]
```

排序选项：

```bash
/forum_search forum_name:[论坛名称] order:[排序方式]
```

支持的排序方式：最高反应降序/升序、总回复数降序/升序、发帖时间由新到旧/由旧到新、最后活跃由新到旧/由旧到新

### 其他实用命令

查看搜索语法帮助：

```bash
/search_syntax
```

查看搜索历史：

```bash
/search_history
```

查看机器人性能统计：

```bash
/bot_stats
```

查看服务器统计信息：

```bash
/server_stats
```

### 分页控制

- ⏮️: 第一页
- ◀️: 上一页
- ▶️: 下一页
- ⏭️: 最后一页
- 🔢: 跳转到指定页面
- 🔄: 刷新结果
- ❌: 关闭搜索结果

## 部署和维护指南

### 系统要求

#### 最低要求
- **操作系统**: Linux (Ubuntu 20.04+), macOS 10.15+, Windows 10+
- **Python**: 3.11 或更高版本
- **内存**: 512MB RAM (小型服务器)
- **存储**: 1GB 可用空间

#### 推荐配置
- **操作系统**: Ubuntu 22.04 LTS
- **Python**: 3.11+
- **内存**: 2GB+ RAM (大型服务器)
- **存储**: 5GB+ SSD
- **CPU**: 2+ 核心

### 依赖服务配置

#### Redis服务器 (推荐)
```bash
# Ubuntu/Debian 安装
sudo apt update
sudo apt install redis-server
sudo systemctl start redis-server
sudo systemctl enable redis-server

# 验证安装
redis-cli ping  # 应返回 PONG
```

#### Docker方式安装Redis
```bash
docker run -d \
  --name discord-bot-redis \
  -p 6379:6379 \
  -v redis-data:/data \
  redis:7-alpine redis-server --appendonly yes
```

### 应用部署

#### 1. 获取源代码
```bash
git clone https://github.com/your-username/discord-forum-search-assistant.git
cd discord-forum-search-assistant
```

#### 2. 环境准备
```bash
# 创建虚拟环境
python3.11 -m venv venv
source venv/bin/activate  # Linux/macOS

# 安装依赖
pip install -r requirements.txt
```

#### 3. 配置设置
```bash
# 复制环境变量模板
cp .env.example .env

# 编辑配置文件
nano .env
```

#### 必需的环境变量
```env
# Discord Bot Token (必需)
DISCORD_TOKEN=your_discord_bot_token_here

# Redis配置 (可选但推荐)
USE_REDIS_CACHE=true
REDIS_URL=redis://localhost:6379/0

# 缓存设置
CACHE_TTL=600
THREAD_CACHE_SIZE=1000

# 搜索限制
MAX_MESSAGES_PER_SEARCH=1000
CONCURRENT_SEARCH_LIMIT=5
```

#### 4. Discord Bot设置
1. 访问 [Discord Developer Portal](https://discord.com/developers/applications)
2. 创建新应用并生成Bot Token
3. 设置必需权限：
   - Send Messages (发送消息)
   - Use Slash Commands (使用斜杠命令)
   - Embed Links (嵌入链接)
   - Read Message History (读取消息历史)
   - View Channels (查看频道)

#### 5. 启动应用

**开发环境**
```bash
python main.py
```

**生产环境 (systemd)**
```bash
# 创建服务文件
sudo nano /etc/systemd/system/discord-bot.service

# 启用服务
sudo systemctl enable discord-bot
sudo systemctl start discord-bot
```

**Docker部署**
```bash
# 构建镜像
docker build -t discord-forum-search-assistant .

# 运行容器
docker run -d \
  --name discord-bot \
  --restart unless-stopped \
  -v $(pwd)/data:/app/data \
  --env-file .env \
  discord-forum-search-assistant
```

**Docker Compose部署**
```bash
# 使用提供的 docker-compose.yml
docker-compose up -d

# 查看日志
docker-compose logs -f discord-bot
```

### 大型服务器优化建议

对于拥有10000+用户和大量帖子的服务器，建议以下配置：

1. 在`config/config.py`中调整以下参数：
   - 降低 `MAX_MESSAGES_PER_SEARCH` 至合理值(如500-1000)
   - 增加 `CACHE_TTL` 至5-10分钟
   - 增加 `REACTION_TIMEOUT` 以延长会话有效期

2. 启用高级缓存设置：
   - 设置 `USE_REDIS_CACHE=True` (需要额外安装Redis)
   - 配置 `THREAD_CACHE_SIZE` 以适应服务器规模

3. 在服务器管理员设置中：
   - 限制使用机器人的频道
   - 设置合理的命令冷却时间
   - 定期监控资源使用情况

## 性能监控

启用内置的性能监控：
```
/bot_stats
```
查看机器人运行状态、响应时间和资源使用情况。

### 监控和维护

#### 健康检查
```bash
# 检查服务状态
sudo systemctl status discord-bot

# 查看缓存统计
# 在Discord中使用: /bot_stats

# 检查Redis状态
redis-cli info memory
```

#### 日志管理
```bash
# 查看实时日志
tail -f logs/discord_bot.log

# 查看错误日志
grep ERROR logs/discord_bot.log | tail -20
```

#### 备份策略
```bash
# 每日数据备份
tar -czf backup/data_$(date +%Y%m%d).tar.gz data/

# Redis数据备份
redis-cli BGSAVE
cp /var/lib/redis/dump.rdb backup/redis_$(date +%Y%m%d).rdb
```

### 详细文档

- [系统架构说明](docs/architecture.md)
- [详细部署指南](docs/deployment.md)
- [运维手册](docs/maintenance.md)
- [故障排除指南](docs/troubleshooting.md)

## 性能监控

机器人内置了详细的性能监控系统：

```bash
/bot_stats
```

监控内容包括：

- 系统资源使用情况（CPU、内存、线程数）
- 搜索统计（总次数、成功率、平均时间、峰值并发）
- 缓存效率（命中率、缓存大小）
- 最常用命令统计
- 最活跃服务器数据
- 网络和连接状态

还可以查看当前服务器的详细统计信息：

```bash
/server_stats
```

## 故障排除

常见问题：

- **机器人无响应**：检查TOKEN配置和网络连接
- **搜索结果为空**：确认机器人有适当的频道访问权限
- **加载缓慢**：考虑调整缓存和分页设置
- **命令错误**：查看日志获取详细错误信息

## 许可证

MIT License

## 贡献指南

欢迎贡献代码、报告问题或提出改进建议。请提交Pull Request或开Issue讨论。