# SA App – Backend Master Plan

## 1. Tech & Integration Overview

- **Backend stack**
  - Supabase Postgres + Edge Functions (Deno).
  - TypeScript models mirrored between `src/` and `supabase/functions/_shared/`.

- **External data: Financial Modeling Prep (FMP)**  
  Use FMP for:
  - Fundamentals: income, balance sheet, cash flow, key metrics, TTM ratios.[web:2][web:17][web:20][web:27]
  - Screener: `search-company-screener` for broad universe filters.[web:79][web:80]
  - Market data: historical EOD prices for stocks and indexes (QQQ, VIX).[web:25][web:51][web:50][web:62][web:56]

- **Configuration**
  - Read `FMP_API_KEY` from environment/config.
  - Never hard‑code API keys.

- **Principles**
  - Prefer FMP **bulk endpoints** (TTM ratios, key metrics, bulk historical prices) over per‑symbol calls.[web:27][web:18][web:25]
  - Store versioned JSONB payloads plus indexed scalar columns.
  - All scoring rules live in **scoring config JSON**, not in code.

---

## 2. Data Models & Database Tables

### 2.1 Fundamentals – `financial_reports_v1` (existing)

**Purpose:** Canonical per‑period fundamental reports.

**Table:** `financial_reports_v1`

- Columns:
  - `id` (PK)
  - `version` (text, e.g. `"1.0"`)
  - `symbol` (text, indexed)
  - `currency` (text)
  - `period_start_date` (date, indexed with `symbol`)
  - `period_end_date` (date)
  - `period_type` (text, e.g. `"annual"`, `"quarterly"`)
  - `payload` (JSONB) – full `FinancialReportV1`
  - `created_at`, `updated_at`
- Constraints:
  - Unique: `(symbol, period_start_date, period_type, version)`

**Model:** `FinancialReportV1` (TypeScript + Deno mirror)

- Shape:
  - `version`, `symbol`, `currency`
  - `period`: `startDate`, `endDate`, `type`
  - `incomeStatement`: `revenue`, `operatingIncome`, `netIncome`, etc.
  - `balanceSheet`: `totalAssets`, `totalLiabilities`, `totalEquity`, optional splits
  - `cashFlowStatement`: `operatingCashFlow`, `endingCashBalance`, optional flows
  - `metrics`: margins, ROA, ROE, etc.
  - `extensions`: free‑form namespace

---

### 2.2 Metrics snapshots – `metrics_snapshots_v1`

**Purpose:** Per‑symbol/per‑date feature vector for scoring, filters, and backtests.

**Table:** `metrics_snapshots_v1`

- Columns:
  - `id` (PK)
  - `version` (text, e.g. `"1.0"`)
  - `symbol` (text, indexed)
  - `as_of_date` (date, indexed)
  - `payload` (JSONB) – `MetricsSnapshotV1`
  - `created_at`, `updated_at`
- Constraints:
  - Unique: `(symbol, as_of_date, version)`

**Model:** `MetricsSnapshotV1`

- Core fields:
  - `version: string`
  - `symbol: string`
  - `asOfDate: string`
  - `metrics: { ... }`
    - **Profitability**
      - `fcfMarginTTM?: number`
      - `operatingMarginTTM?: number`
      - `netMarginTTM?: number`
      - `roeTTM?: number`
      - `roicTTM?: number`
      - `netMarginPrevYear?: number`
      - `operatingMarginPrevYear?: number`
    - **Growth**
      - `revenueGrowthTTM?: number`
      - `epsGrowthTTM?: number`
      - `revenueGrowthHistory3Y?: number[]` (e.g. array of last 3 annual growth rates)
    - **Balance sheet / health**
      - `debtToEquityTTM?: number`
      - `interestCoverageTTM?: number`
      - `currentRatioTTM?: number`
      - `netDebtToEquityTTM?: number`
      - `deltaDebtToEquity1Y?: number`
      - `deltaCurrentRatio1Y?: number`
    - **Valuation**
      - `peTTM?: number`
      - `psTTM?: number`
      - `evToEbitdaTTM?: number`
      - `fcfYieldTTM?: number`
      - `peToSectorMedian?: number` (stock PE / sector median PE)
    - **Size & liquidity**
      - `marketCap?: number`
      - `sharesOutstanding?: number`
      - `avgDollarVolume20D?: number`
    - **Technical / returns**
      - `atr20DPercent?: number`
      - `realizedVol20D?: number`
      - `ma50?: number`
      - `ma200?: number`
      - `return1D?: number`
      - `return10D?: number`
      - `return1M?: number`
      - `return3M?: number`
  - `extensions?: Record<string, unknown>`

**Helpers:**

- `isMetricsSnapshotV1(obj: unknown): obj is MetricsSnapshotV1`
- `assertMetricsSnapshotV1(obj: unknown): MetricsSnapshotV1`

---

### 2.3 Scoring configs – `scoring_configs`

**Purpose:** Store scoring rules & questions as versioned configs.

**Table:** `scoring_configs`

- Columns:
  - `id` (PK)
  - `version` (text, e.g. `"1.0"`)
  - `name` (text, e.g. `"QualityHoldability_v1"`)
  - `is_active` (boolean)
  - `payload` (JSONB) – full `ScoringConfigV1`
  - `created_at`, `updated_at`

**Model:** `ScoringConfigV1`

- `version: string`
- `name: string`
- `description?: string`
- `blocks: ScoringBlockV1[]`

Where:

- `ScoringBlockV1`:
  - `id: string` (e.g. `"profitability"`, `"balance_sheet"`)
  - `label: string`
  - `maxPoints: number`
  - `questions: ScoringQuestionV1[]`

- `ScoringQuestionV1`:
  - `id: string`
  - `label: string`
  - `metricPath: string` (path into `MetricsSnapshotV1.metrics`, e.g. `"metrics.fcfMarginTTM"`)
  - `type: "numeric_band"`
  - `bands: { min?: number; max?: number; points: number }[]`

> All scoring logic (band thresholds, points, patterns) resides in these configs.

---

### 2.4 Watchlists – `watchlists`, `watchlist_symbols`

**Purpose:** Store universes used by Filters, Scores, and History runs.

**Table:** `watchlists`

- `id` (PK)
- `name` (text)
- `description` (text)
- `created_by` (user id or null)
- `created_at` (timestamp)

**Table:** `watchlist_symbols`

- `id` (PK)
- `watchlist_id` (FK → `watchlists.id`)
- `symbol` (text)
- `created_at` (timestamp)

---

### 2.5 History & backtests – `history_runs`, `score_history_v1`

**Purpose:** Store per‑run metadata and per‑day scoring results.

**Table:** `history_runs`

- `id` (PK)
- `name` (text)
- `config_version` (text)
- `start_date` (date)
- `end_date` (date)
- `universe_type` (text: `"manual"` | `"watchlist"`)
- `universe_value` (text, e.g. JSON string or watchlist id)
- `note` (text)
- `created_at` (timestamp)

**Table:** `score_history_v1`

- `id` (PK)
- `run_id` (FK → `history_runs.id`, indexed)
- `symbol` (text)
- `date` (date) – analysis date
- `total_score` (numeric)
- `block_scores` (JSONB) – `{ profitability, growth, balance_sheet, valuation, technical }`
- `bonus_penalty` (numeric)
- `price` (numeric)
- `past_returns` (JSONB) – `{ d1, d10, m1, m3 }`
- `forward_m1_return` (numeric)
- `alpha_vs_qqq_m1` (numeric)
- `buckets` (JSONB) – `{ marketCap, liquidity, volatility }`
- `alerts` (JSONB) – `string[]`
- `note` (text)
- `created_at` (timestamp)

**Indexes:**

- Composite index: `(run_id, symbol, date)`

---

## 3. Edge Functions / Services

### 3.1 Fundamentals (existing)

**Function:** `financial-reports-fetch`

- Input:
  - Bulk request: list of `{ symbol, period }` items.
- Behavior:
  - Calls FMP income statement, balance sheet, cash flow APIs in bulk.
  - Uses `_shared/fmpMapper.ts` to map each symbol/period into `FinancialReportV1`.
  - Upserts rows into `financial_reports_v1`.
- Output:
  - Bulk response of stored reports or errors.

**Function:** `financial-reports-query`

- Input:
  - Bulk request: list of `{ symbol, period }`.
- Behavior:
  - Returns stored `FinancialReportV1` objects (or errors if missing).

---

### 3.2 Metrics snapshots fetch – `metrics-snapshots-fetch`

**Purpose:** Build `MetricsSnapshotV1` in bulk for a list of symbols on a given date.

**Input:**

```ts
{
  asOfDate: string;
  symbols: string[];
  version?: string; // default "1.0"
}
