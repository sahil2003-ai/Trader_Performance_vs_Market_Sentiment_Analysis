# Trader Performance vs. Market Sentiment Analysis

A data-science analysis exploring how daily trader performance metrics vary across Fear & Greed sentiment categories.

## Repository contents

| File | Purpose |
|---|---|
| `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb` | Data preparation, aggregation, and modeling experiments |
| `Output table.csv` | Summary statistics by sentiment category |
| `A short write-up` | Methodology and descriptive interpretation |
| `LICENSE` | Repository license |

## Data processing described in the project

The methodology document describes merging daily market Fear & Greed sentiment with aggregated trade outcomes. It calculates daily PnL, number of trades, win rate, average trade size, an average-leverage proxy based on `Size USD`, and long ratio by sentiment category.

Saved notebook output reports 2,644 sentiment records × 4 fields and 211,224 trade records × 16 fields at initial loading. The notebook's cleaning log is inconsistent: it reports 65,149 rows before cleaning and later 211,224 after `dropna()`. Reconcile this discrepancy and the join logic before treating the analysis as fully validated.

## Descriptive results from the saved CSV summary

| Sentiment | Mean daily PnL | Median daily PnL | Mean PnL/trade | Days | Mean trades/day | Long ratio |
|---|---:|---:|---:|---:|---:|---:|
| Extreme Fear | 52,793.59 | 22,561.74 | 38.43 | 14 | 1,528.57 | 0.49 |
| Extreme Greed | 23,817.29 | 3,127.54 | 56.74 | 114 | 350.81 | 0.46 |
| Fear | 36,891.82 | 1,412.31 | 31.28 | 91 | 679.53 | 0.51 |
| Greed | 11,140.57 | 678.48 | 39.41 | 193 | 260.64 | 0.49 |
| Neutral | 19,297.32 | 1,818.57 | 63.82 | 67 | 562.48 | 0.50 |

PnL units/currency are not specified in the available outputs. The table reports associations across the merged sample; it does not mean sentiment caused the differences or that a sentiment-based trading strategy will be profitable.

## Saved model output

The previous README records a Random Forest result of **80.77% accuracy** and **0.8515 F1-score** on a report containing 468 test examples. These are saved notebook results, not independently reproduced in this review. Before presenting them as validated performance, verify the exact prediction target, class balance, split strategy, date alignment, and that predictors are available before the outcome.

The saved feature-importance output lists `long_ratio` (0.4237), `n_trades` (0.2073), `avg_leverage` (0.1654), and `avg_trade_size` (0.1557). Importance indicates model reliance, not causal impact.

## Reproduce and validate

1. Confirm paths and provenance for the underlying sentiment and trade datasets.
2. Parse timestamps and time zones consistently.
3. Validate merge coverage and resolve the cleaning-log discrepancy.
4. Check missing values and duplicate keys at the intended data grain.
5. Recreate sentiment-level summaries and compare with the saved CSV.
6. If modeling, define the target, use time-aware validation, compare a baseline, and report per-class metrics.

## Limitations

- Data cleaning and row-count notes are inconsistent and need reconciliation.
- The reported model metrics were not independently reproduced.
- Account addresses and transaction hashes can identify accounts; avoid exposing them in screenshots or reports.
- Correlation and grouped PnL differences do not establish causality or a reliable trading strategy.

## Skills demonstrated

Python, pandas, time-series alignment, groupby aggregation, exploratory analysis, model evaluation, and responsible interpretation of financial data.

## Author

Sahil Gaikwad · [GitHub](https://github.com/sahil2003-ai) · [LinkedIn](https://www.linkedin.com/in/sahil-gaikwad-a76b7224a/)
