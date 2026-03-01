# DeepReader 🧠

> AI-powered deep web content reader with multi-platform support

DeepReader is an intelligent web content extraction tool designed for AI agents. It automatically detects URLs in messages, fetches content using specialized parsers, and converts them into clean Markdown format with YAML frontmatter.

## ✨ Features

- **Zero API Keys Required** - Works out of the box
- **Multi-platform Support** - Twitter/X, Reddit, YouTube, and any webpage
- **Automatic Detection** - Smart URL type detection
- **Clean Output** - Markdown with structured metadata
- **Batch Processing** - Handle multiple URLs at once

## 📦 Supported Sources

| Source | Method | API Key? |
|--------|--------|----------|
| Twitter / X | FxTwitter API + Nitter fallback | ❌ None |
| Reddit | .json suffix API | ❌ None |
| YouTube | youtube-transcript-api | ❌ None |
| Any URL | Trafilatura + BeautifulSoup | ❌ None |

## 🚀 Quick Start

### Installation

```bash
pip install -r requirements.txt
```

### Basic Usage

```python
from deepreader_skill import run

# Automatic — triggered when message contains URLs
result = run("Check this out: https://x.com/user/status/123456")

# Reddit post with comments
result = run("https://www.reddit.com/r/python/comments/abc123/my_post/")

# YouTube transcript
result = run("https://youtube.com/watch?v=dQw4w9WgXcQ")

# Any webpage
result = run("https://example.com/blog/interesting-article")

# Multiple URLs at once
result = run("""
  https://x.com/user/status/123456
  https://www.reddit.com/r/MachineLearning/comments/xyz789/
  https://example.com/article
""")
```

## 📄 Output Format

Content is saved as `.md` files with structured YAML frontmatter:

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

[Content body here...]
```

## ⚙️ Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `DEEPREEDER_MEMORY_PATH` | `../../memory/inbox/` | Where to save ingested content |
| `DEEPREEDER_LOG_LEVEL` | `INFO` | Logging verbosity |

## 🏗️ Architecture

```
deepreader/
├── core/              # Core functionality
│   ├── router.py      # URL routing & type detection
│   ├── storage.py     # File storage & management
│   └── utils.py       # Utility functions
├── parsers/           # Content parsers
│   ├── twitter.py     # Twitter/X parser
│   ├── reddit.py      # Reddit parser
│   ├── youtube.py     # YouTube parser
│   └── generic.py     # Generic webpage parser
├── integrations/       # Third-party integrations
│   └── notebooklm.py  # NotebookLM integration
└── __init__.py        # Main entry point
```

## 🔧 How It Works

```
URL detected → is Twitter/X?  → FxTwitter API → Nitter fallback
             → is Reddit?     → .json suffix API
             → is YouTube?    → youtube-transcript-api
             → otherwise      → Trafilatura (generic)
```

Triggers automatically when any message contains `https://` or `http://`.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📜 License

MIT License

---

<p align="center">
  Made with ❤️ for AI Agents
</p>
