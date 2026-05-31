# 🌫️ Nepal Air Quality Predictor
### Kathmandu AQI Forecasting Dashboard

Real-time air quality monitoring, Prophet-powered forecasting, and Telegram alerts for Kathmandu, Nepal.

**Live demo:** `https://your-app-name.streamlit.app` ← update after deployment

---

## Features

- 📈 **AQI Forecast** — Facebook Prophet 7–14 day predictions with confidence intervals
- 🗺️ **Station Map** — All 4 Kathmandu monitoring stations on an interactive map
- ⏰ **Hourly Heatmap** — Rush hour pollution patterns by day and hour
- 🌤️ **Weather Integration** — 7-day forecast from Open-Meteo with rain/AQI correlation
- 🎯 **Accuracy Tracker** — Back-tested MAE, RMSE, and prediction error charts
- 📲 **Telegram Alerts** — Instant notifications when AQI crosses your threshold

---

## Quick Start (Local)

```bash
git clone https://github.com/YOUR_USERNAME/kathmandu-aqi.git
cd kathmandu-aqi
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # Mac/Linux
pip install -r requirements.txt
streamlit run kathmandu_aqi_dashboard.py
```

---

## Setting Up Secrets (Local)

Create `.streamlit/secrets.toml` (already in `.gitignore` — safe):

```toml
AQICN_TOKEN    = "your_token"      # https://aqicn.org/data-platform/token/
TELEGRAM_TOKEN = "your_bot_token"  # from @BotFather
TELEGRAM_CHAT  = "your_chat_id"    # numeric ID — see guide below
```

---

## 🚀 Deploy to Streamlit Cloud (Free)

### Step 1 — Push to GitHub

```bash
cd C:\Projects\kathmandu-aqi

git init
git add kathmandu_aqi_dashboard.py requirements.txt .gitignore .streamlit/config.toml
git commit -m "Initial commit — Kathmandu AQI Dashboard v3"

# Create a new repo on github.com first, then:
git remote add origin https://github.com/YOUR_USERNAME/kathmandu-aqi.git
git branch -M main
git push -u origin main
```

> ⚠️ Never `git add .streamlit/secrets.toml` — it's in `.gitignore` for a reason.

### Step 2 — Connect to Streamlit Cloud

1. Go to **[share.streamlit.io](https://share.streamlit.io)**
2. Sign in with your GitHub account
3. Click **"New app"**
4. Select:
   - Repository: `YOUR_USERNAME/kathmandu-aqi`
   - Branch: `main`
   - Main file: `kathmandu_aqi_dashboard.py`
5. Click **"Deploy"** — takes ~3 minutes

### Step 3 — Add Secrets on Streamlit Cloud

1. In your deployed app, click **⋮ menu → Settings → Secrets**
2. Paste this (with your real values):

```toml
AQICN_TOKEN    = "your_real_aqicn_token"
TELEGRAM_TOKEN = "your_real_bot_token"
TELEGRAM_CHAT  = "your_real_chat_id"
```

3. Click **Save** — app restarts automatically

Your app is now live at `https://your-app-name.streamlit.app` 🎉

---

## 📲 Telegram Alert Setup

### Step 1 — Create your bot

1. Open Telegram and search for **@BotFather**
2. Send `/newbot`
3. Choose a name: e.g. `Kathmandu AQI Alerts`
4. Choose a username: e.g. `ktm_aqi_bot` (must end in `bot`)
5. BotFather gives you a token like:
   ```
   6123456789:AAHdqTcvCHhvGVKMkYPGPM4gWb5aZBcd123
   ```
   Copy it — this is your `TELEGRAM_TOKEN`

### Step 2 — Get your Chat ID

1. Search for your new bot on Telegram and send it any message (e.g. "hello")
2. Open this URL in your browser (replace with your token):
   ```
   https://api.telegram.org/bot6123456789:AAHd.../getUpdates
   ```
3. Look for `"chat":{"id":` — the number after it is your `TELEGRAM_CHAT`
   ```json
   "chat": { "id": 987654321, ... }
   ```
   Copy `987654321` — this is your `TELEGRAM_CHAT`

### Step 3 — Test it

Add both values to `.streamlit/secrets.toml`, restart the app, and click
**"📨 Send Test Alert"** in the sidebar. You should receive a message instantly.

### What the alert looks like

```
🔴 AQI Alert — Kathmandu
━━━━━━━━━━━━━━━━━━━━
📍 Station: Ratna Park
💨 AQI: 168 (Unhealthy)
🔔 Your threshold: 150

Health advice:
• Avoid prolonged outdoor exercise
• Wear N95 or KN95 mask outside
• Keep windows closed; use air purifier
• Sensitive groups stay indoors

Stay safe — Nepal AQI Predictor
```

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| UI & hosting | Streamlit + Streamlit Cloud |
| AQI data | AQICN API |
| Weather | Open-Meteo API (free, no key) |
| Forecasting | Facebook Prophet |
| Charts | Plotly |
| Alerts | Telegram Bot API |
| Language | Python 3.12 |

---

## Project Structure

```
kathmandu-aqi/
├── kathmandu_aqi_dashboard.py   # Main app
├── requirements.txt             # Dependencies
├── .gitignore                   # Keeps secrets safe
├── .streamlit/
│   ├── config.toml              # Theme & server config
│   └── secrets.toml             # Local secrets (NOT committed)
└── README.md                    # This file
```

---

## Roadmap

- [ ] Real historical data pipeline (SQLite)
- [ ] Weather regressors in Prophet model
- [ ] Festival/event calendar (Dashain, Tihar)
- [ ] WhatsApp alerts via Twilio
- [ ] Weekly PDF report export

---

Built for Kathmandu 🇳🇵 — contributions welcome.
