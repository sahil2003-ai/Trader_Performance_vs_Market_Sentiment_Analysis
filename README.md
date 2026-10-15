# Trader Performance vs. Market Sentiment Analysis

A data-science project exploring how daily trader performance metrics vary across Fear & Greed market-sentiment categories.

![Python](https://img.shields.io/badge/Python-Data%20Science-blue) ![Analysis](https://img.shields.io/badge/Focus-Sentiment%20Analysis-orange)

## Contents
- [Overview](#overview)
- [Research Questions](#research-questions)
- [Dataset and Output](#dataset-and-output)
- [Workflow](#workflow)
- [Results and Metrics](#results-and-metrics)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Reproduce the Analysis](#reproduce-the-analysis)
- [Limitations and Next Steps](#limitations-and-next-steps)

## Overview
The analysis joins trader-performance records with daily market-sentiment categories to explore differences in profit and loss (PnL), trade activity, and long-position ratios. It is descriptive analysis, not a trading strategy or a claim that sentiment causes performance.

## Research Questions
- How do mean and median daily PnL differ across sentiment categories?
- How does mean PnL per trade vary?
- Does trading activity or long-position ratio differ by sentiment?
- Are date alignment, time zones, and join coverage handled consistently?

## Dataset and Output
The repository includes `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb` and `Output table.csv`. The original source URLs and currency/units for PnL should be documented before the results are reused.

## Workflow
1. Confirm the provenance of both the sentiment and trader datasets.
2. Parse dates and time zones consistently.
3. Validate merge coverage and duplicate keys.
4. Calculate daily and sentiment-level aggregates.
5. Compare the notebook summaries with `Output table.csv`.
6. Interpret group differences without making causal claims.

## Results and Metrics
The saved output table reports the following sentiment-group summaries:

| Sentiment | Mean daily PnL | Median daily PnL | Mean PnL/trade | Days | Mean trades/day | Long ratio |
|---|---:|---:|---:|---:|---:|---:|
| Extreme Fear | 52,793.59 | 22,561.74 | 38.43 | 14 | 1,528.57 | 0.49 |
| Extreme Greed | 23,817.29 | 3,127.54 | 56.74 | 114 | 350.81 | 0.46 |
| Fear | 36,891.82 | 1,412.31 | 31.28 | 91 | 679.53 | 0.51 |
| Greed | 11,140.57 | 678.48 | 39.41 | 193 | 260.64 | 0.49 |
| Neutral | 19,297.32 | 1,818.57 | 63.82 | 67 | 562.48 | 0.50 |

PnL units/currency are not specified in the saved output. The groups also have different numbers of days and mean trades/day, so compare metrics with sample size and exposure in mind. These associations do not show that sentiment caused the results or that a sentiment-based strategy would be profitable.

## Technology Stack
- Python and pandas
- Jupyter Notebook
- CSV output for sentiment-level summaries
- Statistical aggregation and visualization libraries used in the notebook

## Repository Structure
```text
Trader_Performance_vs_Market_Sentiment_Analysis/
├── Trader_Performance_vs_Market_Sentiment_Analysis.ipynb
├── Output table.csv
└── README.md
```

## Reproduce the Analysis
1. Confirm the original source paths and permissions for the input datasets.
2. Install the libraries imported by the notebook.
3. Run the notebook in order.
4. Validate date alignment, merge coverage, missing values, and duplicate keys.
5. Compare fresh summaries with `Output table.csv`.

## Limitations and Next Steps
- Document dataset sources, licenses, PnL units, and time zones.
- Resolve any mismatch between notebook cleaning logs and final merged row counts.
- Report sample sizes and uncertainty alongside group means.
- Avoid interpreting correlations as causation or financial advice.
- Add genuine charts/screenshots if present in the repository.

## Skills Demonstrated
Data joining, time-based aggregation, market-sentiment analysis, descriptive statistics, data-quality validation, and responsible interpretation.

## Author
**Sahil Gaikwad** · [GitHub](https://github.com/sahil2003-ai) · [LinkedIn](https://www.linkedin.com/in/sahil-gaikwad-a76b7224a/)
