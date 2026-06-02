# 📈 StockPulse

> A full-stack stock trading simulator built as a university project. Browse stocks, place buy/sell orders, track your portfolio, set price alerts, and watch prices move in real time — all with fake money, zero real risk.

---

## What is this?

StockPulse is a paper-trading dashboard — think of it like a flight simulator, but for the stock market. You get **$100,000 of virtual cash** when you sign up, and you can:

- Browse 15 real-world stocks (AAPL, TSLA, NVDA, etc.)
- Buy and sell shares at simulated live prices
- Track your portfolio's value and total return
- Set price alerts so you never miss a move
- View reports and analytics on your trading activity

Prices update **every 3 seconds** via a live feed — so it actually feels like a real trading platform.

---

## Screenshots

> Login → Dashboard → Stocks → Portfolio → Orders → Alerts → Reports

The app has a clean sidebar layout with 6 main sections, all accessible once you create an account.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React + Vite + TypeScript |
| Styling | Tailwind CSS + shadcn/ui |
| Charts | Recharts |
| Backend | Node.js + Express 5 |
| Database | PostgreSQL + Drizzle ORM |
| Auth | Session-based (express-session) |
| API Contract | OpenAPI + Orval codegen |
| Monorepo | pnpm workspaces |
| Live Prices | Server-Sent Events (SSE) |

---

## Getting Started Locally

### 1. Prerequisites

Make sure you have these installed:

- [Node.js](https://nodejs.org) v18 or higher
- [pnpm](https://pnpm.io) — install with `npm install -g pnpm`
- [PostgreSQL](https://www.postgresql.org/download/) — running locally with a database created

### 2. Clone / Extract

If you downloaded the ZIP:
```bash
unzip stockpulse.zip
cd stockpulse
```

If you're cloning from GitHub:
```bash
git clone https://github.com/YOUR_USERNAME/stockpulse.git
cd stockpulse
```

### 3. Install dependencies

```bash
pnpm install
```

### 4. Set up environment variables

Create a `.env` file in the project root:

```env
DATABASE_URL=postgresql://your_user:your_password@localhost:5432/stockpulse
SESSION_SECRET=pick-any-long-random-string-here
```

### 5. Set up the database

This creates all the tables automatically:

```bash
pnpm --filter @workspace/db run push
```

### 6. Run the app

You'll need **two terminals** running at the same time:

**Terminal 1 — API Server:**
```bash
pnpm --filter @workspace/api-server run dev
```

**Terminal 2 — Frontend:**
```bash
pnpm --filter @workspace/stock-app run dev
```

Then open your browser at **http://localhost:24351** and create an account. That's it!

---

## Project Structure

```
stockpulse/
├── artifacts/
│   ├── api-server/        # Express backend (port 8080)
│   │   └── src/
│   │       ├── routes/    # auth, stocks, portfolio, orders, alerts, reports
│   │       └── lib/       # logger, priceSimulator (SSE)
│   └── stock-app/         # React frontend (port 24351)
│       └── src/
│           ├── pages/     # Auth, Dashboard, Stocks, Portfolio, Orders, Alerts, Reports
│           ├── components/ # Sidebar, AppLayout, UI primitives
│           └── hooks/     # useLivePrices (SSE consumer)
├── lib/
│   ├── db/                # Drizzle ORM schema + migrations
│   ├── api-spec/          # OpenAPI YAML spec (source of truth)
│   └── api-client-react/  # Auto-generated React Query hooks
└── scripts/               # Utility scripts
```

---

## Features Walkthrough

### 🔐 Auth
Register with your name, email, and password. You start with **$100,000** virtual cash.

### 📊 Dashboard
At-a-glance overview: portfolio value, total return, market sentiment, top gainers, top losers, and recent activity.

### 🔍 Stocks
Browse all 15 stocks in a live-updating table. Prices flash **green** when they go up and **red** when they go down (every 3 seconds). Search by symbol or company name.

### 💼 Portfolio
See every stock you hold, your average buy price, current value, and unrealized gain/loss.

### 📋 Orders
Place market buy/sell orders. Full order history with status tracking.

### 🔔 Alerts
Set a price target for any stock. The system checks it against live prices and marks it triggered automatically.

### 📈 Reports
Analytics on your trading activity — order volume, P&L breakdown, and more.

---

## Seeded Data

The database comes with **15 pre-loaded stocks**:

`AAPL` `MSFT` `GOOGL` `AMZN` `TSLA` `NVDA` `META` `BRK` `JPM` `JNJ` `V` `WMT` `XOM` `DIS` `NFLX`

Each stock has **30 days of historical price data** for chart rendering.

---

## Deploying Online

Want to share it with others? The easiest free options:

- **[Railway](https://railway.app)** — supports Node.js + PostgreSQL out of the box
- **[Render](https://render.com)** — similar, free tier available
- **Replit** — just hit the **Deploy** button if you're working here

For any cloud deploy, set your `DATABASE_URL` and `SESSION_SECRET` as environment variables in the platform's dashboard.

---

## Notes

- Prices are **simulated** — they use a random walk algorithm and are not real market data
- Passwords are hashed with SHA-256 (suitable for a university project; use bcrypt for production)
- Sessions are stored in-memory — they reset when the server restarts
- This is a learning/demo project, not a real trading platform

---

## License

MIT — do whatever you want with it. If it helps you learn, that's the whole point. 🎓
