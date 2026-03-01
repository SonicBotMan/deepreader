# DeepReader 🧠

> AI 驱动的深度网页内容阅读器，支持多平台

DeepReader 是一款专为 AI Agent 设计的智能网页内容提取工具。它能自动检测消息中的 URL，使用专用解析器获取内容，并将其转换为干净的 Markdown 格式（带 YAML 前言）。

## ✨ 功能特性

- **无需 API Key** - 开箱即用
- **多平台支持** - Twitter/X、Reddit、YouTube 及任意网页
- **自动检测** - 智能 URL 类型识别
- **清洁输出** - 带结构化元数据的 Markdown
- **批量处理** - 同时处理多个 URL

## 📦 支持的平台

| 平台 | 获取方式 | 需要 API Key？ |
|------|----------|----------------|
| Twitter / X | FxTwitter API + Nitter 备用 | ❌ 不需要 |
| Reddit | .json 后缀 API | ❌ 不需要 |
| YouTube | youtube-transcript-api | ❌ 不需要 |
| 任意网页 | Trafilatura + BeautifulSoup | ❌ 不需要 |

## 🚀 快速开始

### 安装

```bash
pip install -r requirements.txt
```

### 基础用法

```python
from deepreader_skill import run

# 自动模式 — 检测到消息中的 URL 时触发
result = run("看看这个: https://x.com/user/status/123456")

# Reddit 帖子（含评论）
result = run("https://www.reddit.com/r/python/comments/abc123/my_post/")

# YouTube 字幕
result = run("https://youtube.com/watch?v=dQw4w9WgXcQ")

# 任意网页
result = run("https://example.com/blog/interesting-article")

# 批量处理多个 URL
result = run("""
  https://x.com/user/status/123456
  https://www.reddit.com/r/MachineLearning/comments/xyz789/
  https://example.com/article
""")
```

## 📄 输出格式

内容保存为 `.md` 文件，包含结构化的 YAML 前言：

```yaml
---
title: "Tweet by @user"
source_url: "https://x.com/user/status/123456"
domain: "x.com"
parser: "twitter"
ingested_at: "2026-02-16T12:00:00Z"
content_hash: "sha256:..."
word_count: 350
---

[内容正文...]
```

## ⚙️ 配置选项

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `DEEPREEDER_MEMORY_PATH` | `../../memory/inbox/` | 保存内容的目录 |
| `DEEPREEDER_LOG_LEVEL` | `INFO` | 日志级别 |

## 🏗️ 项目架构

```
deepreader/
├── core/              # 核心功能
│   ├── router.py      # URL 路由与类型检测
│   ├── storage.py     # 文件存储与管理
│   └── utils.py       # 工具函数
├── parsers/          # 内容解析器
│   ├── twitter.py     # Twitter/X 解析器
│   ├── reddit.py      # Reddit 解析器
│   ├── youtube.py     # YouTube 解析器
│   └── generic.py     # 通用网页解析器
├── integrations/      # 第三方集成
│   └── notebooklm.py  # NotebookLM 集成
└── __init__.py        # 主入口
```

## 🔧 工作原理

```
检测到 URL → 是 Twitter/X?  → FxTwitter API → Nitter 备用
           → 是 Reddit?     → .json 后缀 API
           → 是 YouTube?    → youtube-transcript-api
           → 其他          → Trafilatura (通用)
```

当消息包含 `https://` 或 `http://` 时自动触发。

## 🤝 贡献指南

欢迎贡献代码！请随时提交 Pull Request。

## 📜 许可证

MIT 许可证

---

<p align="center">
  用 ❤️ 为 AI Agents 打造
</p>
