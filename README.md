# Trader Performance vs Market Sentiment Analysis

This project analyzes how trader performance varies with market sentiment using historical trade data and a Fear & Greed sentiment index.

## Overview

The notebook performs the following:
- **Data cleaning & feature engineering** for trade and sentiment datasets
- **Daily trader- and market-level performance metrics** (PnL, winrate, trade count, leverage proxies)
- **Joining trader performance with daily sentiment classifications** (Fear, Greed, Extreme Greed, etc.)
- **Clustering traders into archetypes** using KMeans
- **Predictive modeling** that classifies whether a trader-day is profitable based on behavior + sentiment features (~0.81 accuracy)

---

## Files

| File | Description |
|------|-------------|
| `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb` | Main analysis notebook with all code and outputs |
| `feargreedindex.csv` | Market sentiment time series (timestamp, value, classification, date) |
| `historicaldata.csv` | Trade-level dataset (account, coin, prices, size, side, timestamps, PnL, etc.) |

---

## Setup

### 1. Python Version
The project requires Python 3.8 or higher.

### 2. Clone the Repository
```bash
git clone https://github.com/sahil2003-ai/Trader_Performance_vs_Market_Sentiment_Analysis.git
cd Trader_Performance_vs_Market_Sentiment_Analysis
```

### 3. Create a Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 4. Install Dependencies
```bash
pip install -r requirements.txt
```

Or install manually:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost yellowbrick jupyter
```

---

## How to Run

### Option 1: Using Jupyter Notebook (Local)

1. Make sure `feargreedindex.csv` and `historicaldata.csv` are in the same directory as the notebook.

2. Start Jupyter:
   ```bash
   jupyter notebook
   ```

3. Open `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb` in your browser.

4. Go to **Kernel → Restart & Run All** to execute the entire notebook.

### Option 2: Using Google Colab

1. Go to [Google Colab](https://colab.research.google.com/) and create a new notebook.

2. Upload the following files:
   - `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb`
   - `feargreedindex.csv`
   - `historicaldata.csv`

3. Open the notebook in Colab.

4. Ensure the file paths match:
   ```python
   sentiment_path = "feargreedindex.csv"
   trades_path = "historicaldata.csv"
   ```

5. Run **Runtime → Run All**.

---

## Notebook Flow

| Section | Description |
|---------|-------------|
| **Imports & Setup** | Load libraries: pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost, yellowbrick |
| **Data Preparation** | Load CSVs, handle missing values, convert timestamps, create date columns |
| **Aggregation** | Compute daily per-trader and daily overall metrics (PnL, winrate, trade count, leverage) |
| **Sentiment Join** | Merge daily metrics with sentiment classification (Fear, Greed, Extreme Greed, etc.) |
| **Insights** | Analyze how profit, activity, and leverage behave under different sentiment regimes |
| **Predictive Model** | Train classifiers to predict profitable trader-days (~0.81 accuracy) |
| **Clustering** | Use KMeans to cluster traders into behavioral archetypes |

---

## Extending the Project

- Add more features (volatility, time-of-day, per-coin PnL)
- Tune or swap models in the predictive section
- Export cleaned datasets or trained models
- Build a Streamlit dashboard on top of the analysis

---

## License
MIT License
