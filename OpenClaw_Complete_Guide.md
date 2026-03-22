# OpenClaw — Complete Setup & Usage Guide
### Your Personal Reference for Everything We Did Today

---

## 1. What is OpenClaw?

OpenClaw is a **free, open-source autonomous AI agent** that runs on your computer and lets you control it from your phone through messaging apps like Telegram or WhatsApp. Think of it as a personal AI assistant that can manage emails, calendars, web searches, and more — all just by chatting with it.

- **Installed on:** Your laptop/PC
- **Used from:** Phone (Telegram, WhatsApp, etc.) or browser dashboard
- **Dashboard URL:** `127.0.0.1:18789`
- **Current version:** v2026.3.13

---

## 2. Installation

Install OpenClaw via npm or pnpm in your terminal:

```bash
npm install -g openclaw@latest
```
Then run the setup wizard:
```bash
openclaw onboard --install-daemon
```

---

## 3. Starting & Stopping OpenClaw

| Action | Command |
|--------|---------|
| Start | `openclaw start` |
| Stop | `openclaw stop` |
| Restart | `openclaw restart` |
| Check status | `openclaw status` |
| Start daemon | `openclaw daemon start` |
| Stop daemon | `openclaw daemon stop` |
| Remove from startup | `openclaw daemon uninstall` |

> **Tip:** If OpenClaw was installed with `--install-daemon`, it auto-starts every time your laptop turns on. Just open `127.0.0.1:18789` in your browser.

---

## 4. Emergency Stop / Kill Switch

If something goes wrong, here's how to force stop everything:

```bash
# Kill the process
pkill -f openclaw          # Linux/Mac
# Windows: Open Task Manager → find node.exe → End Task

# Full removal
npm uninstall -g openclaw
rm -rf ~/.openclaw         # Linux/Mac
# Windows: Delete C:\Users\YourName\.openclaw
```

**Most important kill switch — delete your API key:**
Go to **aistudio.google.com** → Manage API Keys → Delete. This instantly stops OpenClaw from doing anything even if it's still running.

---

## 5. API Keys (Free Options)

OpenClaw needs an AI provider API key to work. Here are the best free options:

| Provider | Website | Notes |
|----------|---------|-------|
| **Google Gemini** | aistudio.google.com | Free, no credit card, but has rate limits |
| **Groq** | console.groq.com | Best free option — fast & generous |
| **OpenRouter** | openrouter.ai | Access to many free models |
| **Mistral** | console.mistral.ai | Simple free tier |
| **GitHub Models** | github.com/marketplace/models | Free with GitHub account |

> **Recommendation:** Use **Groq** as your primary — most reliable free tier. Use Gemini as backup.

### How to Replace an Expired API Key

1. Get a new key from your provider's website
2. Open `127.0.0.1:18789` → Agents → your agent → update the key field → Save
3. Run `openclaw restart` in terminal

---

## 6. Telegram Bot Setup

### Step 1 — Create a bot via BotFather
- Open Telegram → search **@BotFather** (must have ✅ blue verified tick)
- Type `/newbot`
- Give it a name (e.g., `My Assistant`)
- Give it a username ending in `bot` (e.g., `myassistant_bot`)
- Copy the token (looks like: `7483920156:AAFkdjsf83jd...`)

### Step 2 — Add bot to OpenClaw
- Go to `127.0.0.1:18789` → **Channels** → **Add Channel** → **Telegram**
- Paste the bot token → Save

### Step 3 — Approve yourself (important!)
When you first message the bot, it will say:
> *"Access not configured. Your Telegram user ID: XXXXXXXX. Pairing code: YYYYYY. Ask bot owner to approve."*

Run this in terminal to approve:
```bash
openclaw pairing approve telegram XXXXXXXX
```
Replace XXXXXXXX with your actual user ID shown in Telegram.

### Step 4 — Start chatting
- Search your bot in Telegram → tap **Start** or type `/start`
- Start sending messages!

---

## 7. Switching to WhatsApp

1. Go to `127.0.0.1:18789` → **Channels** → **Add Channel** → **WhatsApp**
2. A QR code will appear on screen
3. On your phone: **WhatsApp → Settings → Linked Devices → Link a Device**
4. Scan the QR code

> ⚠️ This links your **real WhatsApp number** (not a separate bot). Small risk of account restrictions from WhatsApp. You can run both Telegram and WhatsApp at the same time.

---

## 8. Errors We Encountered & Fixes

### Error 1 — Telegram 401 Unauthorized
```
telegram deleteWebhook failed: 401 Unauthorized
```
**Cause:** Wrong or invalid bot token.
**Fix:** Go to BotFather → `/mybots` → your bot → regenerate token → paste it again in OpenClaw Channels settings.

### Error 2 — Google Gemini Rate Limit
```
API rate limit reached. Please try again later.
```
**Cause:** Free Gemini tier allows only ~15 requests/minute.
**Fix:** Wait 1–2 minutes (OpenClaw auto-retries). Or switch to Groq API.

### Error 3 — Google Auth Permanent Failure
```
Provider google has auth_permanent issue (skipping all models)
```
**Cause:** API key is invalid, deleted, or expired.
**Fix:** Get a new API key → update it in Agents settings → run `openclaw restart`.

### Error 4 — Config Key Not Recognized
```
Config validation failed: Unrecognized key: "GOOGLE_API_KEY"
```
**Fix:** Don't use terminal config command. Instead update the key directly from the dashboard: `127.0.0.1:18789` → Agents → your agent → update key field.

---

## 9. Viewing & Exporting Command History

### View history
```bash
# Windows CMD
doskey /history

# Windows PowerShell
Get-History

# Linux/Mac
history
```

### Export history to file
```bash
# Windows CMD — save to Desktop
doskey /history > %USERPROFILE%\Desktop\commands.txt

# Windows PowerShell — save to Desktop
Get-History | Out-File $env:USERPROFILE\Desktop\commands.txt

# Linux/Mac
history > ~/Desktop/commands.txt
```

---

## 10. Quick Reference — Dashboard Sections

| Section | What it does |
|---------|-------------|
| **Chat** | Talk to your AI agent directly in browser |
| **Channels** | Add/manage Telegram, WhatsApp, Discord etc. |
| **Agents** | Configure AI model, API key, behaviour |
| **Instances** | See running agent instances |
| **Sessions** | View conversation sessions |
| **Overview** | General stats and status |
| **Cron Jobs** | Schedule automated tasks |
| **Usage** | See how much API you've used |

---

## 11. Pro Tips

- **Bookmark** `127.0.0.1:18789` in your browser for quick access
- **Keep Telegram as backup** even after setting up WhatsApp
- **Delete your API key** first if anything goes seriously wrong — it's the safest kill switch
- **Use Groq** instead of Gemini free tier — it's faster and has better limits
- OpenClaw works even when your browser is closed — it runs in the background as a daemon

---

*Summary prepared: March 2026 | OpenClaw v2026.3.13*
