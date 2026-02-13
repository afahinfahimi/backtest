# System Architecture Overview — V15

## Pages & Their Roles

### Dashboard (Analysis)
Primary real-time analysis interface. Enter stock symbols, run scoring engine, view SA scores + Action Signals + Tier classifications. Column order: Symbol | SA | Action | Alert | MC | VIX | Price | 1D P | 5D | 1M | 3M | Tier.

### Backtest
Historical analysis mode. Select a past date, run analysis to see what scores/signals would have been, compare against actual future performance (10D F, 1M F, 2M F). Sessions persist and can be saved/loaded.

### Matrix Pages
Historical score exploration:
- **Stock Matrix**: Single stock's SA scores + Action Signals over time
- **Market Matrix (MC)**: MC score trends, VIX, QQQ performance over time
Both support pagination with "Load More" and CSV export including Action Signal data.

### Chat
AI-powered conversational interface using Lovable AI Gateway. Enriched with Trader Profile, scoring configs, and page context for personalized trading advice.

### Optimize
Research hub with 7 tabs: Scores (win rates by score range), Data (entry counts), SA Breakdown (question correlation), MC Breakdown, Ideas (hypothesis backlog), Log (changelog), App (Pro Advisor chat).

### Tests (Formula Lab)
Sandbox for SA scoring experiments. Run proposed changes against saved backtest data without modifying production engine.

### Lists
Watchlist management + saved analyses/backtests browser. 50/50 split layout with compact multi-column display.

### Config
Engine documentation (SA, MC, MS, Rules, Alerts), Trader Profile editor, system overview. Read-only display with Discussion Chat sidebar.

### Settings
API keys (FMP), chart defaults, data management (clear cache, reset).

### Design
Live theme customization — score colors, VIX thresholds, MC thresholds. Changes apply globally via CSS variables.

## Data Flow
Market Data (FMP API) → MC Engine → MC Score → MC Zones
Stock Data (FMP API) → SA Engine → SA Score → Tier
SA + MC + VIX → Action Signal Engine → Buy/Sell/Hold Signal
Historical Data → Matrix → Backtest → Optimization Loop
