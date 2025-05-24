# Discord 论坛搜索助手

![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)
![Discord.py](https://img.shields.io/badge/Discord.py-2.3+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Maintenance](https://img.shields.io/badge/Maintained-Yes-green.svg)

**Language / 语言:** [🇺🇸 English](README.md) • [🇨🇳 **中文**](README_zh.md)

**专为大型服务器设计的强大Discord机器人，提供高级论坛帖子搜索和内容管理功能。**

[功能特点](#-功能特点) • [快速开始](#-快速开始) • [部署指南](#-部署指南) • [文档](#-文档) • [支持](#-支持)

---

## 🚀 功能特点

### 🔍 **高级搜索引擎**

- **复杂查询语法**: 支持 AND、OR、NOT 操作符和精确短语匹配
- **多维度过滤**: 按标签、作者、日期范围、反应数和回复数筛选
- **智能排序**: 8种排序方式，包括反应数、回复数、发帖时间和最后活跃时间
- **实时进度**: 长时间搜索的实时进度显示和取消支持

### 🎯 **用户体验**

- **分页结果**: 直观的界面控制，轻松浏览大量搜索结果
- **自动完成**: 智能建议，优先显示最近使用的选项
- **搜索历史**: 保存和快速访问最近的搜索记录
- **交互控制**: 基于反应的丰富嵌入界面导航

### ⚡ **性能与可扩展性**

- **企业级缓存**: Redis集成，支持高流量服务器（10,000+用户）
- **智能内存管理**: 针对大型Discord社区优化
- **性能监控**: 内置指标和资源使用跟踪
- **多环境支持**: 开发、测试和生产环境配置

## 🚀 快速开始

### 前置要求

- **Python**: 3.11+ (必需)
- **Discord.py**: v2.3+ (自动安装)
- **Redis**: 可选，但推荐用于生产环境
- **机器人权限**:
  - 发送消息
  - 使用斜杠命令
  - 嵌入链接
  - 添加反应
  - 读取消息历史
  - 查看频道

### 安装步骤

1. **克隆仓库**

   ```bash
   git clone https://github.com/yourusername/discord-forum-search-assistant.git
   cd discord-forum-search-assistant
   ```

2. **安装依赖**

   ```bash
   pip install -r requirements.txt
   ```

3. **配置环境**

   ```bash
   cp .env.example .env
   # 编辑 .env 文件，添加你的Discord机器人令牌
   ```

4. **运行机器人**

   ```bash
   python main.py
   ```

### 🐳 Docker部署（推荐）

使用Docker Compose快速部署（包含Redis）：

```bash
# 配置环境变量
echo "DISCORD_TOKEN=your_bot_token_here" > .env

# 启动服务
docker-compose up -d
```

## 📖 使用指南

### 基本搜索

```bash
/forum_search forum_name:[论坛名称] search_word:[关键词]
```

### 高级搜索语法

| 操作符 | 语法 | 示例 |
|--------|------|------|
| **AND** | `term1 AND term2` 或 `term1 & term2` | `python AND discord` |
| **OR** | `term1 OR term2` 或 `term1 \| term2` | `bot OR automation` |
| **NOT** | `NOT term` 或 `-term` | `NOT deprecated` |
| **精确短语** | `"exact phrase"` | `"错误处理"` |
| **复合查询** | `(term1 OR term2) AND NOT term3` | `(python OR js) AND NOT beginner` |

### 多维度过滤

```bash
/forum_search forum_name:[论坛] tag1:[标签1] tag2:[标签2]
              original_poster:[用户] min_reactions:[数量]
              start_date:[日期] order:[排序方式]
```

### 可用命令

| 命令 | 描述 |
|------|------|
| `/forum_search` | 主搜索命令，支持高级过滤 |
| `/search_syntax` | 显示搜索语法帮助 |
| `/search_history` | 查看最近的搜索记录 |
| `/bot_stats` | 机器人性能和系统统计 |
| `/server_stats` | 当前服务器统计信息 |

### 导航控制

| 按钮 | 操作 |
|------|------|
| ⏮️ | 第一页 |
| ◀️ | 上一页 |
| ▶️ | 下一页 |
| ⏭️ | 最后一页 |
| 🔢 | 跳转到指定页面 |
| 🔄 | 刷新结果 |
| ❌ | 关闭搜索结果 |

### 排序选项

- **反应数**: 最高/最低反应数
- **回复数**: 最多/最少回复
- **日期**: 最新/最旧帖子
- **活跃度**: 最近/最久活跃

## 🚀 部署指南

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| **操作系统** | Ubuntu 20.04+, macOS 10.15+, Windows 10+ | Ubuntu 22.04 LTS |
| **Python** | 3.11+ | 3.11+ |
| **内存** | 512MB RAM | 2GB+ RAM |
| **存储** | 1GB | 5GB+ SSD |
| **CPU** | 1核心 | 2+核心 |

### 环境配置

机器人通过统一配置系统支持多种部署环境：

```bash
# 设置环境 (default, large_server, development, production)
export BOT_ENVIRONMENT=production

# 或使用配置管理器
python scripts/config_manager.py set production
```

### 云平台部署选项

| 平台 | 月费用 | 适用场景 | 设置难度 |
|------|--------|----------|----------|
| **Railway** ⭐⭐⭐⭐⭐ | $5-8 | 生产环境 | 简单 |
| **Render** ⭐⭐⭐⭐ | $0-7 | 测试/小型生产 | 简单 |
| **DigitalOcean** ⭐⭐⭐⭐ | $5-17 | 企业级 | 中等 |

#### Railway部署（推荐）

```bash
# 安装Railway CLI
npm install -g @railway/cli

# 部署
railway login
railway init
railway variables set DISCORD_TOKEN=your_token_here
railway up
```

#### Render部署

```yaml
# render.yaml
services:
  - type: web
    name: discord-forum-search-bot
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: python main.py
    envVars:
      - key: DISCORD_TOKEN
        sync: false
```

### 本地开发设置

1. **克隆和设置**

   ```bash
   git clone https://github.com/yourusername/discord-forum-search-assistant.git
   cd discord-forum-search-assistant
   python -m venv venv
   source venv/bin/activate  # Linux/macOS
   pip install -r requirements.txt
   ```

2. **配置环境**

   ```bash
   cp .env.example .env
   # 编辑 .env 文件配置你的设置
   ```

3. **设置Discord机器人**
   - 访问 [Discord开发者门户](https://discord.com/developers/applications)
   - 创建应用程序并生成机器人令牌
   - 启用必需权限：
     - 发送消息
     - 使用斜杠命令
     - 嵌入链接
     - 读取消息历史
     - 查看频道

4. **运行机器人**

   ```bash
   python main.py
   ```

### 性能优化

对于大型服务器（10,000+用户），使用 `large_server` 环境：

```bash
# 设置大型服务器配置
python scripts/config_manager.py set large_server

# 或设置环境变量
export BOT_ENVIRONMENT=large_server
```

**大型服务器优化：**

- **Redis缓存**: 默认启用
- **数据库索引**: 自动建立，加快搜索速度
- **增量加载**: 减少内存使用
- **扩展超时**: 更适合高流量服务器

## 📊 监控与性能

### 内置监控

```bash
/bot_stats    # 系统性能和统计信息
/server_stats # 当前服务器指标
```

**监控功能：**

- **系统资源**: CPU、内存、线程使用情况
- **搜索分析**: 成功率、响应时间、并发搜索
- **缓存效率**: 命中率、缓存大小、Redis状态
- **命令使用**: 最常用命令和活跃服务器
- **网络状态**: 连接健康状况和延迟

### 健康检查

```bash
# 检查机器人状态
python scripts/config_manager.py validate

# 查看当前配置
python scripts/config_manager.py current

# 比较环境配置
python scripts/config_manager.py compare default large_server
```

## 📚 文档

| 文档 | 描述 |
|------|------|
| [系统架构](docs/architecture.md) | 系统设计和组件说明 |
| [部署指南](docs/deployment.md) | 详细部署说明 |
| [云平台对比](docs/cloud_deployment_comparison.md) | 平台对比和费用分析 |
| [运维手册](docs/maintenance.md) | 运维和维护指南 |
| [故障排除](docs/troubleshooting.md) | 常见问题和解决方案 |
| [性能优化](docs/performance_optimization.md) | 优化策略和技巧 |

## 🐛 故障排除

| 问题 | 解决方案 |
|------|----------|
| **机器人无响应** | 检查 `DISCORD_TOKEN` 和网络连接 |
| **搜索结果为空** | 验证机器人在目标频道的权限 |
| **性能缓慢** | 启用Redis缓存，调整分页设置 |
| **命令错误** | 检查日志: `tail -f logs/discord_bot.log` |
| **内存问题** | 使用 `large_server` 环境配置 |

## 🤝 支持

- **问题反馈**: [GitHub Issues](https://github.com/yourusername/discord-forum-search-assistant/issues)
- **讨论交流**: [GitHub Discussions](https://github.com/yourusername/discord-forum-search-assistant/discussions)
- **文档wiki**: [项目Wiki](https://github.com/yourusername/discord-forum-search-assistant/wiki)

## 📄 许可证

本项目采用MIT许可证 - 详见 [LICENSE](LICENSE) 文件。

## 🚀 贡献指南

我们欢迎贡献！请查看我们的 [贡献指南](CONTRIBUTING.md) 了解详情：

- 代码风格和标准
- Pull Request流程
- 问题报告
- 开发环境设置

---

用 ❤️ 为Discord社区制作

[⭐ 给项目加星](https://github.com/yourusername/discord-forum-search-assistant) • [🐛 报告Bug](https://github.com/yourusername/discord-forum-search-assistant/issues) • [💡 功能建议](https://github.com/yourusername/discord-forum-search-assistant/issues)
