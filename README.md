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

## 大型服务器优化建议

对于拥有10000+用户和大量帖子的服务器，建议以下配置：

1. 使用Docker部署并启用Redis缓存：

    ```bash
    # 在docker-compose.yml中设置
    environment:
      - CONFIG_MODE=large_server
    ```

2. 或在`config/large_server.py`中调整以下参数：
   - 设置 `MAX_MESSAGES_PER_SEARCH=1000` 限制单次搜索消息数
   - 设置 `CACHE_TTL=600` 增加缓存时间至10分钟
   - 设置 `REACTION_TIMEOUT=1800` 延长会话有效期至30分钟
   - 设置 `USE_REDIS_CACHE=True` 启用Redis缓存
   - 设置 `CONCURRENT_SEARCH_LIMIT=5` 控制并发搜索数量
   - 设置 `USER_SEARCH_COOLDOWN=60` 限制用户搜索频率

3. 在服务器管理员设置中：
   - 限制使用机器人的频道
   - 设置合理的命令冷却时间

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
- **搜索速度慢**：考虑启用Redis缓存和调整`large_server.py`配置
- **内存使用过高**：降低`MAX_MESSAGES_PER_SEARCH`和`THREAD_CACHE_SIZE`值
- **命令错误**：查看`logs`目录下的日志文件获取详细错误信息

## 许可证

MIT License

## 贡献指南

欢迎贡献代码、报告问题或提出改进建议。请提交Pull Request或开Issue讨论。