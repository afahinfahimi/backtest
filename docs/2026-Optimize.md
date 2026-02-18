# Module-5: Optimize

The Optimize module provides an AI-assisted sandbox for iteratively refining the SA scoring engine by testing config changes against historical data across multiple dates and segments.

## Core Components

### Optimize Engine
- **File:** `src/lib/optimize-engine.ts`
- **Purpose:** Re-scores `stock_matrix_results.raw_data` using draft SA configs. Computes per-question Pearson correlations, win rates, and average returns per segment.
- **Key Functions:** `runDraftComparison()`, `createDraft()`, `saveDraftRun()`, `fetchAvailableDates()`
- **Isolation:** Uses its own tables and engine file — never modifies production scoring.

### Optimize Page
- **File:** `src/pages/OptimizePage.tsx`
- **Route:** `/optimize`
- **Layout:** Draft selector + test controls + two-panel (Chat + Runs)

### Chat Panel
- **File:** `src/components/optimize/OptimizeChatPanel.tsx`
- **Edge Function:** `supabase/functions/optimize-chat/index.ts`
- **Purpose:** AI-assisted analysis of correlation data. Suggests config changes (threshold tweaks, new questions, penalties, question removal).
- **Context:** Sends current draft config and latest run correlations to AI.

### Runs Panel
- **File:** `src/components/optimize/OptimizeRunsPanel.tsx`
- **Purpose:** Displays saved test runs with per-question correlation comparison (Draft vs Production).

### Correlation (r) Table (Legacy)
- **File:** `src/components/optimize/CorrelationTable.tsx`
- **Purpose:** Production correlation display on Home page (unchanged).

### Points Table (Legacy)
- **File:** `src/components/optimize/SAPointsTable.tsx`
- **Purpose:** Collapsible raw points grid on Home page (unchanged).

## Database Tables

### optimize_drafts
- **Purpose:** Stores draft SA config snapshots for testing.
- **Columns:** `id`, `name`, `base_version`, `config_snapshot` (JSONB — full ScoringEngineConfig), `status`, `notes`, `created_at`, `updated_at`.

### optimize_draft_runs
- **Purpose:** Individual test execution results per date/segment.
- **Columns:** `id`, `draft_id` (FK → optimize_drafts), `analysis_date`, `segment`, `symbols[]`, `sector_filter`, `correlations` (JSONB), `win_rate`, `avg_return`, `sample_size`, `production_correlations` (JSONB), `production_win_rate`, `details` (JSONB), `created_at`.

### optimize_ideas
- **Purpose:** User-generated optimization notes (legacy).

## Workflow
1. Create a draft (clones production SA config).
2. AI Chat suggests modifications (add/remove questions, change thresholds, add penalties).
3. Manually edit draft config or apply AI suggestions.
4. Run tests on multiple dates and segments (≥80, ≥70, all, sector filter).
5. Compare Draft vs Production correlations and win rates.
6. When satisfied, manually update the Vault with the new config.

## Segmentation
- **SA ≥ 80:** Focus on reducing false positives in highest-scoring stocks.
- **SA ≥ 70:** Broader validation after ≥80 improvements.
- **All:** Full universe baseline.
- **Sector filter:** Test impact on specific industries (e.g., exclude Biotech).

## Key Dependencies
- `src/lib/engine/rule-processor.ts` — Core scoring engine.
- `src/lib/engine/configs/sa-config.ts` — Production SA config (DEFAULT_SA_CONFIG).
- `src/lib/engine/types.ts` — ScoringEngineConfig, QuestionConfig types.
- `stock_matrix_results` table — Source of historical raw_data for re-scoring.

## End of Optimize
