# MCC//PRO — Market Command Center

A personal EOD market monitoring dashboard hosted on GitHub Pages, with data auto-fetched daily from Yahoo Finance via GitHub Actions.

## Live URL
`https://YOUR_USERNAME.github.io/market-dashboard/`

## How It Works

```
Every weekday at 22:00 UTC (06:00 HKT)
    ↓
GitHub Action runs fetch_data.py
    ↓
Python fetches 100+ tickers from Yahoo Finance (free, no API key)
    ↓
Saves data/data.json to repo
    ↓
Your dashboard at GitHub Pages reads data.json on load
    ↓
Fresh EOD data ready for your 9am HKT review ✓
```

## Repo Structure

```
market-dashboard/
├── index.html              ← Your dashboard (GitHub Pages serves this)
├── fetch_data.py           ← Data fetcher script
├── data/
│   └── data.json           ← Auto-generated daily (do not edit manually)
└── .github/
    └── workflows/
        └── fetch-data.yml  ← GitHub Actions schedule
```

## Setup (One-Time, ~10 Minutes)

### 1. Create GitHub Account
Go to [github.com](https://github.com) → Sign Up → free personal account.

### 2. Create a New Repository
- Click **+** → **New repository**
- Name it: `market-dashboard`
- Set to **Public** (required for free GitHub Pages)
- Click **Create repository**

### 3. Upload Files
Click **uploading an existing file** and upload:
- `index.html`
- `fetch_data.py`
- `.github/workflows/fetch-data.yml` *(create this folder path manually in the UI)*

Or use GitHub Desktop app (easier) — drag and drop the whole folder.

### 4. Enable GitHub Pages
- Go to repo **Settings** → **Pages**
- Source: **Deploy from a branch**
- Branch: `main` / `(root)`
- Click **Save**

Your URL will be: `https://YOUR_USERNAME.github.io/market-dashboard/`

### 5. Run the Action Manually First
- Go to **Actions** tab → **Fetch Market Data** → **Run workflow**
- This generates `data/data.json` immediately (without waiting for the schedule)
- Reload your Pages URL — live data will appear

## Schedule
The action runs **Mon–Fri at 22:00 UTC** (06:00 HKT), after US markets close at ~21:00 UTC.
Data is fresh and ready for your **9am HKT** morning review.

You can also trigger it manually anytime from the Actions tab.

## Data Sources
- **Equities, ETFs, Futures, Commodities, Crypto**: Yahoo Finance via `yfinance` (free, no key)
- **~130 tickers** fetched per run across all dashboard sections

## Troubleshooting

**Dashboard shows "Demo data"**: The `data/data.json` file hasn't been generated yet. Run the Action manually (Step 5 above).

**Some tickers show no data**: Yahoo Finance occasionally has gaps. The fetcher logs warnings — check the Actions run log.

**Action fails**: Check the Actions tab for error logs. Most common cause is a temporary Yahoo Finance outage — re-running usually fixes it.
