# 🤖 Multi-User Telegram Auto-Forward Bot

A powerful Telegram bot that automatically forwards messages between channels and groups with **advanced filters, caption cleaning, watermarking, and multi-account support**.

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/new)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## ✨ Features

### 🚀 Core Features
- ✅ **Multiple source → destination rules** - Forward from many to many
- ✅ **Telethon (MTProto)** - Forward files up to 2GB+
- ✅ **Copy mode & Forward mode** - Choose how to send messages
- ✅ **Album handling** - Keep grouped media together
- ✅ **Duplicate prevention** - Skip already forwarded files
- ✅ **Multi-account support** - Connect multiple Telegram accounts
- ✅ **Per-user rules** - Each user has isolated rules

### 🎨 Advanced Features
- ✂️ **Caption cleaning** - Remove hashtags, links, emojis, mentions, phones, emails
- 🚫 **Message filters** - Ignore specific message types (video, photo, sticker, etc.)
- 📝 **Text watermark** - Add custom text to images and videos
- 🖼️ **Logo watermark** - Add logo/image watermark with transparency
- 💬 **Custom captions** - Replace captions with formatted text
- 🔄 **Word replacement** - Replace words/phrases in captions
- 📌 **Header/Footer** - Add custom text at beginning/end
- 🔘 **Link buttons** - Add custom inline buttons
- ⏱️ **Delay forwarding** - Schedule message forwarding
- 📜 **History forwarding** - Forward past messages when creating rule
- 🙈 **Spoiler effect** - Apply blur effect to photos/videos
- 🗑️ **Block/Whitelist words** - Filter messages by content

### 📊 Monitoring & Health
- 🏥 **Health check server** - HTTP endpoints for monitoring
- 📈 **Prometheus metrics** - Track forwards, sessions, uptime
- 🎯 **Beautiful dashboard** - Visual status page
- 🚨 **Error tracking** - Monitor and debug issues

---

## 🏗️ Tech Stack

- **Python 3.10+**
- **python-telegram-bot** - Bot UI and commands
- **Telethon** - MTProto for large file forwarding
- **SQLite** - Local database
- **FFmpeg** - Media processing (watermarks)
- **Pillow** - Image manipulation

---

## 🚀 Quick Start

### Option 1: Deploy to Railway (Recommended) ⚡

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app)

1. Click the button above
2. Connect your GitHub account
3. Fork this repository
4. Set environment variables in Railway dashboard
5. Done! Your bot is live 🎉

📖 **[Full Railway Deployment Guide →](RAILWAY_DEPLOYMENT.md)**

### Option 2: Local Development 💻

```bash
# 1. Clone repository
git clone https://github.com/YOUR-USERNAME/telegram-autoforward-bot.git
cd telegram-autoforward-bot

# 2. Install dependencies
pip install -r requirements.txt

# 3. Copy environment template
cp .env.example .env

# 4. Edit .env with your credentials
nano .env

# 5. Run the bot
python main.py
```

### Option 3: Docker 🐳

```bash
# 1. Build image
docker build -t telegram-bot .

# 2. Run container
docker run -d \
  --name telegram-bot \
  -e TELEGRAM_API_ID=your_api_id \
  -e TELEGRAM_API_HASH=your_api_hash \
  -e TELEGRAM_BOT_TOKEN=your_bot_token \
  -v $(pwd)/data:/app/data \
  -p 8080:8080 \
  telegram-bot
```

---

## ⚙️ Configuration

### Required Environment Variables

Get these credentials before starting:

```bash
# Get from https://my.telegram.org/apps
TELEGRAM_API_ID=12345678
TELEGRAM_API_HASH=abc123def456...

# Get from @BotFather on Telegram
TELEGRAM_BOT_TOKEN=1234567890:ABC-DEF...
```

### Optional Configuration

```bash
# Admin user ID (optional)
ADMIN_USER_ID=123456789

# Storage paths
SESSION_DIR=user_sessions
DATABASE_FILE=autoforward.db

# Limits
MAX_RULES_PER_USER=50
MAX_ACCOUNTS_PER_USER=10

# Health check server port
HEALTH_PORT=8080
```

📄 **See [.env.example](.env.example) for full configuration**

---

## 📖 How to Use

### 1️⃣ Start the Bot

Open Telegram and search for your bot, then send:

```
/start
```

### 2️⃣ Connect Your Account

1. Click **"🔗 Connect Account"**
2. Send your phone number: `+1234567890`
3. Enter the verification code from Telegram
4. Enter 2FA password (if enabled)
5. ✅ Account connected!

### 3️⃣ Create Forwarding Rule

1. Click **"➕ Add Rule"**
2. Select your connected account
3. **Enter sources** (where messages come FROM):
   ```
   -1001234567890, @channel1, @channel2
   ```
4. **Enter destinations** (where messages go TO):
   ```
   @mychannel, -1009876543210
   ```
5. **Choose mode**:
   - 📤 **Forward** - Keep "Forwarded from" header
   - 📋 **Copy** - Send as new message (no header)

6. **Configure filters** (optional):
   - Ignore specific message types
   - Remove hashtags, links, mentions
   - Add watermarks, buttons, custom captions

7. ✅ Done! Messages will forward automatically 24/7

### 4️⃣ Manage Rules

- 📋 **View Rules** - See all your active rules
- ⏯️ **Toggle** - Enable/disable rules
- 🔧 **Edit** - Change sources, destinations, filters
- 🗑️ **Delete** - Remove rules

---

## 🎯 Use Cases

### 📢 Content Aggregation
Forward from multiple news channels → your single news channel

### 🔄 Content Redistribution
Copy competitor content → your channel (with watermark & cleaned captions)

### 🎨 Brand Protection
Add watermark to all forwarded media automatically

### 📊 Multi-Channel Management
Manage multiple Telegram accounts from one bot

### 🚫 Content Filtering
Forward only specific message types (photos only, videos only, etc.)

### 🔗 Cross-Promotion
Add custom buttons to all forwarded messages

---

## 📊 Health Monitoring

The bot includes a built-in health check server for monitoring:

### Endpoints

```bash
# Dashboard (HTML)
http://localhost:8080/

# Liveness check (always returns 200 if running)
http://localhost:8080/health

# Readiness check (200 if ready, 503 if not)
http://localhost:8080/ready

# Prometheus metrics
http://localhost:8080/metrics
```

### Metrics Tracked

- ⏱️ **Uptime** - How long bot has been running
- 📱 **Active Sessions** - Number of connected accounts
- 📨 **Total Forwards** - Cumulative message count
- 💾 **Database Health** - SQLite connection status
- 📡 **Telegram Health** - API connection status
- 🐛 **Last Error** - Most recent error with timestamp

### Dashboard Preview

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🤖 Telegram Bot Status
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Status: HEALTHY ✅

Uptime: 2d 14h 32m
Active Sessions: 3
Total Forwards: 15,234

Database: ✅
Telegram: ✅
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 🗂️ Project Structure

```
telegram-autoforward-bot/
├── main.py                 # Main bot application
├── health_server.py        # HTTP health check server
├── requirements.txt        # Python dependencies
├── Dockerfile              # Container configuration
├── railway.toml            # Railway platform config
├── .env.example            # Environment template
├── .gitignore              # Git ignore rules
├── README.md               # This file
├── RAILWAY_DEPLOYMENT.md   # Deployment guide
├── LICENSE                 # MIT License
└── user_sessions/          # Telegram session files (gitignored)
```

---

## 🔒 Security

### Best Practices

✅ **Never commit `.env`** - Always in `.gitignore`  
✅ **Use environment variables** - For all secrets  
✅ **Rotate credentials** - Change tokens every 3-6 months  
✅ **Monitor access** - Check logs regularly  
✅ **Enable 2FA** - On your Telegram account  
✅ **Use Railway's secrets** - Encrypted at rest  

### What Gets Stored

- ✅ **Session files** - Encrypted Telegram sessions
- ✅ **Database** - Forward rules and user data
- ✅ **Temporary files** - Downloaded media (auto-cleaned)
- ❌ **Passwords** - Never stored
- ❌ **Bot token** - Only in environment variables

---

## 🐛 Troubleshooting

### Bot Not Starting

```bash
# Check logs
python main.py

# Verify environment variables
cat .env

# Test health endpoint
curl http://localhost:8080/health
```

### Sessions Lost on Deploy

Use persistent storage (Railway Volumes):
```bash
# Railway Dashboard → Settings → Volumes
Mount Path: /app/user_sessions
```

### Database Resets

Enable persistent storage:
```bash
# Railway Dashboard → Settings → Volumes
Mount Path: /app/data

# Update environment
DATABASE_FILE=data/autoforward.db
```

### FFmpeg Not Found

Install FFmpeg for watermarking:
```bash
# Ubuntu/Debian
apt-get install ffmpeg

# macOS
brew install ffmpeg

# Docker (already included in Dockerfile)
```

---

## 📚 Documentation

- 📖 [Railway Deployment Guide](RAILWAY_DEPLOYMENT.md)
- 🤖 [Telegram Bot API](https://core.telegram.org/bots/api)
- 📡 [Telethon Docs](https://docs.telethon.dev)
- 🐍 [python-telegram-bot](https://docs.python-telegram-bot.org)

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Development Setup

```bash
# 1. Fork and clone
git clone https://github.com/YOUR-USERNAME/telegram-autoforward-bot.git

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment
cp .env.example .env
nano .env

# 5. Run locally
python main.py
```

### Contribution Guidelines

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [Telegram](https://telegram.org) - Messaging platform
- [Telethon](https://github.com/LonamiWebs/Telethon) - Telegram MTProto library
- [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) - Bot framework
- [Railway](https://railway.app) - Deployment platform

---

## 💬 Support

- 🐛 **Bug reports** - Open an issue
- 💡 **Feature requests** - Open an issue
- 📧 **Questions** - Open a discussion
- ⭐ **Star this repo** - If you find it useful!

---

## ⚡ Quick Links

- 🚀 [Deploy to Railway](https://railway.app/new)
- 📖 [Deployment Guide](RAILWAY_DEPLOYMENT.md)
- 🔧 [Configuration](.env.example)
- 📊 [Health Dashboard](http://localhost:8080)
- 🤖 [Create Bot](https://t.me/BotFather)
- 🔑 [Get API Credentials](https://my.telegram.org/apps)

---

## 🎯 Roadmap

- [ ] Web dashboard for rule management
- [ ] Multi-language support
- [ ] Advanced scheduling (cron-like)
- [ ] Media conversion (video → GIF, etc.)
- [ ] Statistics and analytics
- [ ] Webhook support
- [ ] Message templates
- [ ] Auto-reply functionality

---

Made with ❤️ for the Telegram community

**Star ⭐ this repo if you find it useful!**
