# 📈 AlgoTrader Bot — Intraday Algo Trading System

> **Built 100% via AI Prompt Engineering** — signal engine → paper trading → React dashboard → live order execution → GCP deployment, all delivered through structured multi-turn Claude prompt chains.

⚠️ **Research & Paper Trading System** — built for learning algorithmic trading. Not financial advice.

---

## 🎯 What It Does

AlgoTrader Bot is a fully automated **intraday trading system** that monitors the Indian stock market (NSE/BSE), identifies trade opportunities using technical indicators, and executes buy/sell orders automatically — without manual intervention.

Once configured and started each morning, the bot:
- Scans 200+ F&O symbols and builds a dynamic watchlist
- Monitors live market data via WebSocket (tick-by-tick)
- Fires buy signals when conditions are met
- Places orders automatically through Zerodha Kite Connect API
- Manages open positions and exits automatically
- Logs every trade to MongoDB for analysis

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                  React Dashboard                         │
│         Live P&L · Trade Journal · Signal Feed          │
└────────────────────┬────────────────────────────────────┘
                     │ REST API
                     ▼
┌─────────────────────────────────────────────────────────┐
│              FastAPI (Python) — Bot Engine               │
│                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Signal       │  │ Order        │  │ Position     │  │
│  │ Engine       │  │ Manager      │  │ Manager      │  │
│  │ (TA engine)  │  │ (Kite API)   │  │ (auto exit)  │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
│                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Dynamic      │  │ Paper Trade  │  │ Auth Server  │  │
│  │ Watchlist    │  │ Engine       │  │ (Kite OAuth) │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└────────────────────┬─────────────────────────┬──────────┘
                     │ Kite WebSocket           │ REST
                     ▼                          ▼
        ┌─────────────────────┐    ┌───────────────────┐
        │  Zerodha Kite       │    │     MongoDB        │
        │  Live Market Data   │    │  Trade Journal     │
        │  + Order Execution  │    │  Signal Logs       │
        └─────────────────────┘    └───────────────────┘
```

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| **Bot Engine** | Python · FastAPI · Pandas-TA |
| **Market Data** | Zerodha Kite Connect WebSocket (live tick data) |
| **Order Execution** | Zerodha Kite Connect REST API |
| **Dashboard** | React · Recharts · WebSocket |
| **Database** | MongoDB (trade journal, signal logs) |
| **Cloud** | GCP Compute Engine · Supervisord · Systemd |
| **Testing** | 703 automated tests |

---

## 🚀 Key Features

### 📡 Live Market Data
- Connects to Zerodha Kite WebSocket for real-time tick-by-tick price data
- Scans **200+ F&O symbols** per watchlist cycle
- Dynamic watchlist — best-scoring stocks selected each morning automatically

### 🤖 Fully Automated Trading
- Bot runs independently once started — no manual clicks during market hours
- Automatically places buy orders when signals trigger
- Automatically manages and exits positions
- Auto square-off before market close (14:55 IST)

### 📄 Paper Trading Mode
- Full paper trading mode (`LIVE_TRADING=false`) — simulates all trades without real money
- Identical logic runs in paper and live modes — safe to test before going live
- All virtual trades logged to MongoDB for analysis

### 📊 React Dashboard
- Live P&L display updated in real time
- Trade journal — every entry/exit with timestamps and outcome
- Signal feed — what the bot is watching and why it acted

### ☁️ GCP Cloud Deployment
- Runs 24/7 on GCP Compute Engine VM
- Supervisord process manager — auto-restarts on crash
- Systemd service — survives VM reboots
- Daily Kite OAuth token refresh via browser (phone-friendly auth page)

### 🧪 703 Automated Tests
- Unit tests covering signal engine, order manager, position manager
- Paper trade engine tested independently
- Pre-flight smoke test runs every morning before market open

---

## 📊 By the Numbers

| Metric | Value |
|---|---|
| F&O symbols scanned per cycle | 200+ |
| Automated tests | 703 |
| Deployment | GCP Cloud (24/7) |
| Market data | Zerodha Kite WebSocket |
| Trading mode | Paper (default) · Live (configurable) |
| Build method | 100% AI Prompt Engineering (Claude) |
| Phases shipped | 6 (signal → paper → dashboard → live → GCP → ML scorer) |

---

## 🗂️ Project Phases

| Phase | What Was Built |
|---|---|
| **Phase 1** | Signal engine — technical indicator scanning |
| **Phase 2** | Paper trading bot — virtual order simulation |
| **Phase 3** | React dashboard — live P&L and trade journal |
| **Phase 4** | Live order engine — Kite API integration |
| **Phase 5** | GCP deployment — 24/7 cloud operation |
| **Phase 6** | ML scorer — signal confidence scoring |

---

## ⚙️ How to Configure & Run

The bot is fully configurable via environment variables — no code changes needed:

```env
KITE_API_KEY=your_key
KITE_API_SECRET=your_secret
LIVE_TRADING=false          # true = real orders, false = paper mode
CAPITAL_PER_TRADE=20000     # ₹ allocated per trade
MAX_OPEN_POSITIONS=1        # concurrent positions limit
MONGO_URI=mongodb://...
```

**Daily startup (3 steps):**
1. Refresh Kite auth token via browser (08:00 IST)
2. Run pre-flight check — confirms all systems green
3. Start bot at market open (09:15 IST) — fully automated from here

---

## 🤖 How This Was Built

6 phases from signal engine to live cloud deployment were delivered through **structured multi-turn prompt engineering** with Claude.

Each phase followed the same pattern:
1. **Domain context given** — trading rules, Kite API constraints, architecture requirements
2. **Claude designed** — module structure, data flow, edge cases
3. **Claude coded** — full implementation with 703 automated tests
4. **Iterated** — multi-turn refinement until production-ready

This is **LLM-native development** — not autocomplete, but Claude as a product co-developer.

---

## 🗺️ Roadmap

- [ ] ML-based signal confidence scorer (in progress)
- [ ] Multi-broker support (Angel One, Upstox)
- [ ] Telegram alerts for trade events
- [ ] Web-based configuration UI (no .env editing)
- [ ] Backtesting engine with historical NSE data

---

## ⚠️ Disclaimer

This is a **personal research project** for learning algorithmic trading concepts. It is not financial advice. Use paper trading mode to evaluate performance before considering live trading. Always understand the risks involved.

---

## 👨‍💻 Built By

**Balamurugan Kandasamy (Bala)** — AI Prompt Engineer · Full Stack Dev · 18+ Years Enterprise

📧 baluclick@gmail.com | 📍 Chennai, India | ✈️ Open to Middle East / Remote

> *"I don't use AI to autocomplete lines of code. I use it as a product co-founder — providing domain context, business rules, and iterative feedback while Claude architects, codes, and deploys entire feature sets."*
