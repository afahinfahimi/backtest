# Tests Page (Formula Lab) — V15

## Purpose
Sandbox environment for experimenting with SA scoring formula changes before implementing them. Tests run locally against saved backtest data without modifying the production scoring engine.

## Workflow
1. **Create Test** → Define type + parameters + hypothesis
2. **Select Data** → Load historical data from saved backtests
3. **Run Test** → Engine recalculates SA scores with proposed change
4. **Review Results** → Compare before/after win rates
5. **Decide** → Approve → implement in sa-scoring-engine.ts, or reject

## Test Types

### add_question
Add a new SA scoring question. Parameters:
- field: Data field to evaluate (e.g., "rsiValue", "peRatio")
- operator: >, <, >=, <=, ==
- threshold: Comparison value
- pointsIfTrue / pointsIfFalse: Score impact
- questionName: Display label

### modify_question
Change an existing question's logic. Parameters:
- questionIndex: 0-based index of the SA question
- originalLogic: Current logic (reference)
- newLogic: Updated logic

### remove_question
Remove a question. Parameters:
- removeQuestionIndex: 0-based index

### change_weight
Adjust point values. Parameters:
- targetQuestion: Question name
- oldValue / newValue: Point values

### change_threshold
Adjust tier or score thresholds. Parameters:
- targetQuestion: Target (e.g., "T1", "T2")
- oldValue / newValue: Threshold values

## Results Metrics
- **Total Stocks**: Number of stocks analyzed
- **Stocks Changed**: How many had SA score affected by the change
- **Threshold Crossers**: Stocks crossing key thresholds (80, 90)
- **Win Rate Before/After**: Primary success metric
- **Verdict**: AI-generated assessment

## Data Sources
- **formula_tests**: Test definitions, status, results (draft → tested → approved → implemented/rejected)
- **saved_backtests**: Source data for test runs
- **stock_matrix_results**: Historical raw_data for SA recalculation

## Current SA Engine Reference
- 30 questions (Q19 Trend Consistency removed in V14)
- Normalization span: 105 (Max 69, Min -36)
- Q9 uses 20D + 50D SMA (not 50/200)
- Q16 uses 3-tier country scoring (USA +2, Developed +1, China/EM -2)
- Cyclical sector cap: 4 points max on Q1–Q3
- Missing data: midpoint of min/max for each question
