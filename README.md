# Trader Performance vs. Market Sentiment Analysis

A data-science project exploring how cryptocurrency trader activity and profitability vary across daily **Fear & Greed Index** regimes. The notebook combines trade-level records with daily sentiment, engineers trader-day features, compares profitability-classification models, and segments trading behavior with K-Means clustering.

<p align="left">
  <img src="https://img.shields.io/badge/Python-Data%20Analysis-3776AB?logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Analytics-Market%20Sentiment-6A5ACD" alt="Market sentiment" />
  <img src="https://img.shields.io/badge/ML-Classification%20%7C%20Clustering-F7931E" alt="Classification and clustering" />
  <img src="https://img.shields.io/badge/Notebook-Jupyter-F37626?logo=jupyter&logoColor=white" alt="Jupyter" />
</p>

## Project overview

This project investigates relationships between daily market sentiment and trading outcomes, including profit and loss (PnL), trade frequency, win rate, trade size and long-position ratio. It combines descriptive analysis with a supervised model that predicts whether a trader-day is profitable and an unsupervised model that groups trader-days into behavioral segments.

**This is an exploratory analysis, not a validated trading strategy.** Observed associations do not establish that sentiment causes performance or that following the patterns would produce profits.

## Research questions

- How do mean and median daily PnL vary across Extreme Fear, Fear, Neutral, Greed and Extreme Greed?
- Does mean PnL per trade differ from total daily PnL patterns?
- How do trade frequency, position direction and trade-size proxies vary by sentiment?
- Can trader-day activity features classify whether a trader-day is profitable?
- What behavioral profiles emerge from clustering trader-day metrics?
- Are the source dates, time zones, merge coverage and row counts consistent?

## Data sources and availability

The notebook expects two source files that are **not currently included in the repository tree**:

| Expected file | Purpose | Saved notebook profile |
|---|---|---:|
| `fear_greed_index.csv` | Daily market Fear & Greed classification | 2,644 rows × 4 columns |
| `historical_data.csv` | Individual trader executions and PnL | 211,224 rows × 16 columns |

The repository currently contains the analysis notebook, the exported sentiment summary table and a methodology write-up. To reproduce the analysis from raw data, obtain the original files from their authorized sources, document those sources and licenses, and place the files where the notebook expects them.

### Trading data fields

The notebook references fields including `Account`, `Coin`, `Execution Price`, `Size Tokens`, `Size USD`, `Side`, `Timestamp IST`, `Start Position`, `Direction`, `Closed PnL`, `Transaction Hash`, `Order ID`, `Crossed`, `Fee`, `Trade ID` and `Timestamp`.

The sentiment data includes a timestamp, a numeric index value, a classification and a date. The exported output does not specify the currency/unit for PnL. This README therefore reports PnL values without adding a currency symbol.

## Data preparation and feature engineering

The notebook follows this workflow:

1. Load the sentiment and trade files with pandas.
2. Inspect schemas, missing values and duplicate rows.
3. Parse the sentiment date and trade timestamp; derive a calendar date from `Timestamp IST`.
4. Create trade-level flags for positive closed PnL and long/buy side.
5. Aggregate individual executions into daily trader-level and market-level summaries.
6. Join those summaries to the sentiment classification by calendar date.
7. Compare performance and behavior across sentiment categories.
8. Train and evaluate classification models on trader-day records.
9. Scale numerical features and use K-Means to identify three behavioral clusters.

### Engineered metrics

| Metric | Definition in notebook |
|---|---|
| Daily PnL | Sum of `Closed PnL` for each trader and date |
| Trade count | Number of trade rows in the group |
| Win rate | Share of rows where `Closed PnL > 0` |
| Average trade size | Mean `Size Tokens` |
| Trade-value proxy | Mean `Size USD` |
| Long ratio | Share of rows whose `Side` is Buy/Long |
| Profitable target | 1 when daily PnL is greater than 0; otherwise 0 |

**Metric caveat:** the notebook names mean `Size USD` a leverage proxy in places, but notional trade value is not the same as leverage. This README calls it a **trade-value proxy** where possible. Actual leverage would require position exposure and collateral/equity information.

## Results: performance by sentiment

The repository's `Output table.csv` contains the following saved summaries. PnL units/currency are not specified.

| Sentiment | Mean daily PnL | Median daily PnL | Mean PnL per trade | Days | Mean trades/day | Mean Size USD proxy | Long ratio |
|---|---:|---:|---:|---:|---:|---:|---:|
| Extreme Fear | 52,793.59 | 22,561.74 | 38.43 | 14 | 1,528.57 | 4,091.80 | 0.49 |
| Extreme Greed | 23,817.29 | 3,127.54 | 56.74 | 114 | 350.81 | 4,410.52 | 0.46 |
| Fear | 36,891.82 | 1,412.31 | 31.28 | 91 | 679.53 | 6,524.29 | 0.51 |
| Greed | 11,140.57 | 678.48 | 39.41 | 193 | 260.64 | 6,735.30 | 0.49 |
| Neutral | 19,297.32 | 1,818.57 | 63.82 | 67 | 562.48 | 7,157.53 | 0.50 |

### Descriptive observations

- **Extreme Fear** has the highest mean and median daily PnL in the saved summary, but only 14 days are represented.
- **Greed** has the lowest mean daily PnL and the lowest median daily PnL among the listed sentiment groups.
- **Neutral** has the highest mean PnL per trade in this output.
- The long ratio stays close to 0.5 across all categories, so the sentiment grouping alone does not show a large directional imbalance.
- Mean trades per day varies considerably across sentiment groups; comparisons should account for activity and sample size.

These are descriptive summaries. Unequal group sizes, market conditions, outliers and aggregation choices can affect the averages. They are not evidence that a sentiment-based trading rule would be profitable.

## Supervised learning: predicting profitable trader-days

The notebook creates a binary target:

- **Profitable (1):** daily PnL > 0
- **Not profitable (0):** daily PnL ≤ 0

Features include trade count, average trade size, mean `Size USD` trade-value proxy, long ratio and sentiment category. The notebook uses a stratified 80/20 train/test split with `random_state=42`, a preprocessing pipeline with numerical scaling and one-hot encoding, and GridSearchCV with three-fold cross-validation to tune model hyperparameters.

### Model comparison

The saved notebook output reports these held-out split results:

| Model | Accuracy | F1-score |
|---|---:|---:|
| **Random Forest** | **80.77%** | **85.15%** |
| XGBoost | 80.34% | 85.02% |
| Gradient Boosting | 79.27% | 83.64% |
| Decision Tree | 77.99% | 83.20% |
| MLP Classifier | 77.14% | 82.08% |
| SVC | 76.71% | 80.84% |
| K-Nearest Neighbors | 75.43% | 80.93% |
| Logistic Regression | 62.61% | 76.82% |

Random Forest was the best model by accuracy in the recorded run. Its test-set classification report shows:

| Class | Precision | Recall | F1-score | Support |
|---|---:|---:|---:|---:|
| Not profitable (0) | 0.77 | 0.69 | 0.73 | 175 |
| Profitable (1) | 0.82 | 0.88 | 0.85 | 293 |
| **Overall accuracy** |  |  | **0.81** | **468** |
| Macro average | 0.80 | 0.78 | 0.79 | 468 |
| Weighted average | 0.81 | 0.81 | 0.81 | 468 |

The test split contains 468 trader-day records. The positive class is more common than the negative class, so accuracy should be read alongside class-wise precision, recall and F1.

### Random Forest feature importance

The notebook's saved feature-importance output ranks the model inputs as follows:

| Feature | Importance |
|---|---:|
| Long ratio | 0.4237 |
| Trade count | 0.2073 |
| Trade-value proxy (`Size USD`) | 0.1654 |
| Average trade size | 0.1557 |
| Sentiment: Extreme Greed | 0.0123 |
| Sentiment: Fear | 0.0116 |
| Sentiment: Greed | 0.0105 |
| Sentiment: Neutral | 0.0085 |
| Sentiment: Extreme Fear | 0.0050 |

Feature importance measures the model's use of features, not causality. In this model, the engineered trading-behavior variables contribute more importance than the one-hot sentiment categories.

### Evaluation caveat

The model predicts profitability from trader-day behavior features and sentiment. These are observational records, and the saved workflow does not establish out-of-time generalization. For a stronger assessment, split by date or use forward-chaining validation, check for account overlap across splits, compare with a majority-class baseline, and verify that features would truly be available at the intended prediction time.

## Unsupervised learning: trader behavior clusters

The notebook scales six trader-day features and applies K-Means with **three clusters**. The saved output gives the following average profiles:

| Cluster | Trader-days | Mean daily PnL | Mean trades | Mean win rate | Mean trade size | Mean Size USD proxy | Long ratio |
|---|---:|---:|---:|---:|---:|---:|---:|
| 0 | 18 | 2,735.10 | 47.94 | 62.24% | 421,832.47 | 3,383.53 | 0.41 |
| 1 | 1,391 | -879.43 | 51.66 | 12.24% | 2,623.04 | 6,433.50 | 0.54 |
| 2 | 932 | 12,307.96 | 148.61 | 70.94% | 5,814.45 | 7,889.00 | 0.41 |

The notebook's descriptive labels characterize these groups approximately as:

- **Cluster 0:** lower-frequency trader-days with lower trade-value proxy and positive average PnL. The very large mean trade size and small cluster make this group worth checking for outliers.
- **Cluster 1:** lower-frequency trader-days with negative average PnL and a low mean win rate.
- **Cluster 2:** higher-frequency trader-days with higher average PnL and win rate.

Cluster labels are data-driven groupings, not permanent trader identities. Cluster sizes and profiles depend on scaling, features and the chosen number of clusters.

## Visualizations generated in the notebook

The notebook generates plots for:

- Mean daily PnL by sentiment
- Trade frequency, trade-value proxy and long ratio by sentiment
- Daily PnL by sentiment and leverage/trade-value segment
- Random Forest feature importance
- Confusion matrix and classification report
- K-Means elbow method
- Mean feature values by cluster

The repository currently contains the notebook and exported CSV summary, but no separate image files or `images/` directory. These charts are saved as notebook outputs rather than standalone files, so no unrelated or fabricated images are embedded here. To display the actual visuals on the repository landing page, export the plots from a fresh notebook run to `images/` and add Markdown image references.

## Repository contents

```text
Trader_Performance_vs_Market_Sentiment_Analysis/
├── Trader_Performance_vs_Market_Sentiment_Analysis.ipynb
├── Output table.csv
├── A short write-up
├── LICENSE
└── README.md
```

## Reproduce the analysis

### 1. Clone the repository

```bash
git clone https://github.com/sahil2003-ai/Trader_Performance_vs_Market_Sentiment_Analysis.git
cd Trader_Performance_vs_Market_Sentiment_Analysis
```

### 2. Install dependencies

The notebook uses pandas, NumPy, Matplotlib, Seaborn, scikit-learn, XGBoost and Yellowbrick, among other standard Python packages.

```bash
python -m venv .venv
```

Activate the environment:

```bash
# Windows PowerShell
.venv\\Scripts\\Activate.ps1

# macOS / Linux
source .venv/bin/activate
```

Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost yellowbrick jupyter
```

### 3. Add the source datasets

Place `fear_greed_index.csv` and `historical_data.csv` in the directory expected by the notebook. Confirm their provenance, license, date range and units before using or redistributing them.

### 4. Run the notebook

```bash
jupyter notebook Trader_Performance_vs_Market_Sentiment_Analysis.ipynb
```

Run cells in order and compare fresh output with [`Output table.csv`](Output%20table.csv). Note that the notebook includes model grid searches, which may take time depending on hardware and package versions.

## Limitations and next steps

- **Source data not bundled:** include authorized sources, dates and licenses for the raw input files.
- **PnL units:** document currency/units and whether fees/funding are reflected in `Closed PnL`.
- **Trade value is not leverage:** use actual leverage fields or clearly retain the `Size USD` proxy label.
- **Cleaning log inconsistency:** one notebook cell prints 65,149 rows before cleaning, while the loaded trades table has 211,224 rows; correct the hard-coded log so it reports the actual pre-cleaning count.
- **Sentiment join coverage:** one daily row has no matching sentiment classification; investigate date alignment and report merge coverage.
- **Time-aware validation:** use date-based/forward validation to assess generalization rather than relying only on a random split.
- **Potential outliers:** investigate the very large average trade size in cluster 0 before interpreting that segment.
- **Uncertainty:** include confidence intervals or bootstrap intervals for sentiment-group comparisons.
- **Financial interpretation:** these exploratory patterns are not financial advice and should not be treated as a live trading recommendation.
- **Visual evidence:** export genuine notebook charts to an `images/` directory and embed them in the README.

## Skills demonstrated

Python · pandas · data cleaning · timestamp alignment · feature engineering · groupby aggregation · market sentiment analysis · classification · GridSearchCV · Random Forest · XGBoost · model evaluation · feature importance · K-Means clustering · data visualization · analytical communication

## Author

**Sahil Gaikwad**  
[GitHub](https://github.com/sahil2003-ai) · [LinkedIn](https://www.linkedin.com/in/sahil-gaikwad-a76b7224a/)
