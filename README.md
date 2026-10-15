# Trader Performance vs. Market Sentiment Analysis

A data-science project exploring whether market-sentiment indicators are associated with trader-performance measures.

## Objective
Bring sentiment and trading-related data into a documented analysis pipeline, investigate relationships, and evaluate whether any predictive signal remains under a realistic validation strategy.

## Workflow Described
- Data preparation and cleaning
- Sentiment analysis
- Calculation of trader-performance metrics
- Model experiments using scikit-learn and XGBoost
- Visual analysis with Matplotlib and Seaborn

The README previously described scripts such as `data_preparation.py`, `sentiment_analysis.py`, `model_training.py`, `evaluation.py`, and `main.py`. Confirm these paths exist before running the commands below.

## Tools
Python, pandas, scikit-learn, XGBoost, and visualization/NLP libraries used by the implementation.

## How to Run
1. Clone the repository and create a virtual environment.
2. Install dependencies from `requirements.txt`, if present.
3. Review the data source and any API or licensing requirements.
4. Run the preparation, modelling, and evaluation steps documented in the actual source files.

## Evaluation and Leakage Controls
- Align sentiment observations with the correct trading time.
- Avoid using information that was unavailable at prediction time.
- Use chronological splits rather than random splits for time-dependent prediction.
- Compare against simple baselines.
- Report metrics and uncertainty on a held-out period.
- Distinguish association from causation.

## Recommended Improvements
Document dataset provenance, exact target definitions, time alignment, model metrics, and a reproducible command sequence. Remove any unsupported claims about predictive performance.

> This project is for educational research and is not investment advice.