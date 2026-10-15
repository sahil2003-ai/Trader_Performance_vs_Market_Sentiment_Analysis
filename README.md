# Trader Performance vs. Market Sentiment Analysis

A data-science project exploring relationships between market-sentiment indicators and trader-performance measures.

## Step-by-step workflow

1. Open `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb` and read the data-loading cells.
2. Review `Output table.csv` and the short write-up; identify source data, units, date ranges, and target variables.
3. Check missing values, duplicates, time zones, and date alignment across sentiment and performance records.
4. Define the analysis question and make sure features would have been available at the time of prediction.
5. Perform EDA and visualize sentiment alongside performance measures.
6. If modelling, use chronological splits and compare against simple baselines.
7. Evaluate on a held-out time period and check for leakage or survivorship bias.
8. Interpret results as associations unless the design supports stronger causal conclusions.
9. Update the write-up with verified results and caveats.

## Tools
Python, pandas, Jupyter Notebook, scikit-learn/XGBoost and visualization libraries where used.

## Screenshots
No image files were found in the repository root. Add charts under `images/` and embed them here.

## Limitations
Market data is noisy; timing mismatches can create misleading results. This is educational research, not investment advice.

## Next improvements
Document data provenance, time alignment, target definitions, baseline metrics, and reproducible setup.