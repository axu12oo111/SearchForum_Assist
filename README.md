# Discord Forum Search Assistant

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)
![Discord.py](https://img.shields.io/badge/Discord.py-2.3+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Maintenance](https://img.shields.io/badge/Maintained-Yes-green.svg)

**A powerful Discord bot designed for large servers, providing advanced forum post search and content management capabilities.**

[Features](#-features) • [Quick Start](#-quick-start) • [Deployment](#-deployment) • [Documentation](#-documentation) • [Support](#-support)

</div>

---

## 🚀 Features

### 🔍 **Advanced Search Engine**
- **Complex Query Syntax**: Support for AND, OR, NOT operators and exact phrase matching
- **Multi-dimensional Filtering**: Filter by tags, authors, date ranges, reactions, and reply counts
- **Smart Sorting**: 8 sorting options including reactions, replies, post time, and last activity
- **Real-time Progress**: Live search progress with cancellation support for long-running queries

### 🎯 **User Experience**
- **Paginated Results**: Intuitive interface controls for browsing large result sets
- **Auto-completion**: Smart suggestions with recently used options prioritized
- **Search History**: Save and recall recent searches for quick access
- **Interactive Controls**: Rich embed interfaces with reaction-based navigation

### ⚡ **Performance & Scalability**
- **Enterprise-grade Caching**: Redis integration for high-traffic servers (10,000+ users)
- **Intelligent Memory Management**: Optimized for large-scale Discord communities
- **Performance Monitoring**: Built-in metrics and resource usage tracking
- **Multi-environment Support**: Configurations for development, testing, and production

## 🚀 Quick Start

### Prerequisites

- **Python**: 3.11+ (Required)
- **Discord.py**: v2.3+ (Auto-installed)
- **Redis**: Optional but recommended for production
- **Bot Permissions**:
  - Send Messages
  - Use Slash Commands
  - Embed Links
  - Add Reactions
  - Read Message History
  - View Channels

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/discord-forum-search-assistant.git
   cd discord-forum-search-assistant
   ```

2. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment**

   ```bash
   cp .env.example .env
   # Edit .env with your Discord bot token
   ```

4. **Run the bot**

   ```bash
   python main.py
   ```

### 🐳 Docker Deployment (Recommended)

Quick deployment with Docker Compose (includes Redis):

```bash
# Configure environment
echo "DISCORD_TOKEN=your_bot_token_here" > .env

# Start services
docker-compose up -d
```

## 📖 Usage Guide

### Basic Search

```bash
/forum_search forum_name:[forum-name] search_word:[keywords]
```

### Advanced Search Syntax

| Operator | Syntax | Example |
|----------|--------|---------|
| **AND** | `term1 AND term2` or `term1 & term2` | `python AND discord` |
| **OR** | `term1 OR term2` or `term1 \| term2` | `bot OR automation` |
| **NOT** | `NOT term` or `-term` | `NOT deprecated` |
| **Exact Phrase** | `"exact phrase"` | `"error handling"` |
| **Complex** | `(term1 OR term2) AND NOT term3` | `(python OR js) AND NOT beginner` |

### Multi-dimensional Filtering

```bash
/forum_search forum_name:[forum] tag1:[tag1] tag2:[tag2]
              original_poster:[user] min_reactions:[count]
              start_date:[date] order:[sort-method]
```

### Available Commands

| Command | Description |
|---------|-------------|
| `/forum_search` | Main search command with advanced filtering |
| `/search_syntax` | Display search syntax help |
| `/search_history` | View your recent searches |
| `/bot_stats` | Bot performance and system statistics |
| `/server_stats` | Current server statistics |

### Navigation Controls

| Button | Action |
|--------|--------|
| ⏮️ | First page |
| ◀️ | Previous page |
| ▶️ | Next page |
| ⏭️ | Last page |
| 🔢 | Jump to specific page |
| 🔄 | Refresh results |
| ❌ | Close search results |

### Sorting Options

- **Reactions**: Highest/Lowest reaction count
- **Replies**: Most/Least replies
- **Date**: Newest/Oldest posts
- **Activity**: Most/Least recently active

## 🚀 Deployment

### System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **OS** | Ubuntu 20.04+, macOS 10.15+, Windows 10+ | Ubuntu 22.04 LTS |
| **Python** | 3.11+ | 3.11+ |
| **Memory** | 512MB RAM | 2GB+ RAM |
| **Storage** | 1GB | 5GB+ SSD |
| **CPU** | 1 core | 2+ cores |

### Environment Configuration

The bot supports multiple deployment environments through a unified configuration system:

```bash
# Set environment (default, large_server, development, production)
export BOT_ENVIRONMENT=production

# Or use the configuration manager
python scripts/config_manager.py set production
```

### Cloud Deployment Options

| Platform | Cost/Month | Best For | Setup Difficulty |
|----------|------------|----------|------------------|
| **Railway** ⭐⭐⭐⭐⭐ | $5-8 | Production | Easy |
| **Render** ⭐⭐⭐⭐ | $0-7 | Testing/Small prod | Easy |
| **DigitalOcean** ⭐⭐⭐⭐ | $5-17 | Enterprise | Medium |

#### Railway Deployment (Recommended)

```bash
# Install Railway CLI
npm install -g @railway/cli

# Deploy
railway login
railway init
railway variables set DISCORD_TOKEN=your_token_here
railway up
```

#### Render Deployment

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

### Local Development Setup

1. **Clone and setup**

   ```bash
   git clone https://github.com/yourusername/discord-forum-search-assistant.git
   cd discord-forum-search-assistant
   python -m venv venv
   source venv/bin/activate  # Linux/macOS
   pip install -r requirements.txt
   ```

2. **Configure environment**

   ```bash
   cp .env.example .env
   # Edit .env with your settings
   ```

3. **Set up Discord Bot**
   - Visit [Discord Developer Portal](https://discord.com/developers/applications)
   - Create application and generate Bot Token
   - Enable required permissions:
     - Send Messages
     - Use Slash Commands
     - Embed Links
     - Read Message History
     - View Channels

4. **Run the bot**

   ```bash
   python main.py
   ```

### Performance Optimization

For large servers (10,000+ users), use the `large_server` environment:

```bash
# Set large server configuration
python scripts/config_manager.py set large_server

# Or set environment variable
export BOT_ENVIRONMENT=large_server
```

**Large Server Optimizations:**

- **Redis Caching**: Enabled by default
- **Database Indexing**: Automatic for faster searches
- **Incremental Loading**: Reduces memory usage
- **Extended Timeouts**: Better for high-traffic servers

## 📊 Monitoring & Performance

### Built-in Monitoring

```bash
/bot_stats    # System performance and statistics
/server_stats # Current server metrics
```

**Monitoring Features:**

- **System Resources**: CPU, memory, thread usage
- **Search Analytics**: Success rates, response times, concurrent searches
- **Cache Efficiency**: Hit rates, cache size, Redis status
- **Command Usage**: Most used commands and active servers
- **Network Status**: Connection health and latency

### Health Checks

```bash
# Check bot status
python scripts/config_manager.py validate

# View current configuration
python scripts/config_manager.py current

# Compare environments
python scripts/config_manager.py compare default large_server
```

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [Architecture](docs/architecture.md) | System design and components |
| [Deployment Guide](docs/deployment.md) | Detailed deployment instructions |
| [Cloud Comparison](docs/cloud_deployment_comparison.md) | Platform comparison and costs |
| [Maintenance](docs/maintenance.md) | Operations and maintenance guide |
| [Troubleshooting](docs/troubleshooting.md) | Common issues and solutions |
| [Performance](docs/performance_optimization.md) | Optimization strategies |

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| **Bot not responding** | Check `DISCORD_TOKEN` and network connectivity |
| **Empty search results** | Verify bot permissions in target channels |
| **Slow performance** | Enable Redis cache, adjust pagination settings |
| **Command errors** | Check logs: `tail -f logs/discord_bot.log` |
| **Memory issues** | Use `large_server` environment configuration |

## 🤝 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/discord-forum-search-assistant/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/discord-forum-search-assistant/discussions)
- **Documentation**: [Wiki](https://github.com/yourusername/discord-forum-search-assistant/wiki)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🚀 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details on:

- Code style and standards
- Pull request process
- Issue reporting
- Development setup

---

Made with ❤️ for the Discord community

[⭐ Star this repo](https://github.com/yourusername/discord-forum-search-assistant) • [🐛 Report Bug](https://github.com/yourusername/discord-forum-search-assistant/issues) • [💡 Request Feature](https://github.com/yourusername/discord-forum-search-assistant/issues)