# Trader Performance vs. Market Sentiment Analysis

> Data-science analysis exploring relationships between market sentiment and trader-performance measures.

![Status](https://img.shields.io/badge/Status-Portfolio--Project-blue)

## 📌 Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Objectives](#objectives)
- [Features](#features)
- [Dataset](#dataset)
- [Tech Stack](#tech-stack)
- [Project Workflow](#project-workflow)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Results and Insights](#results-and-insights)
- [Screenshots](#screenshots)
- [Challenges and Solutions](#challenges-and-solutions)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [What I Learned](#what-i-learned)
- [Author](#author)
- [License](#license)

## 📖 Overview

Data-science analysis exploring relationships between market sentiment and trader-performance measures. This README documents the intended workflow and the files available in the repository. Verify all outputs against the current code and data before using them as evidence.

## 🎯 Problem Statement

Combining sentiment with trading outcomes requires careful time alignment and validation to avoid misleading conclusions.

## 🎯 Objectives

- Inspect and align sentiment and performance data.
- Explore associations between indicators.
- Evaluate any predictive experiment using time-aware validation.

## ✨ Features

- Analysis notebook.
- Output table CSV.
- Short write-up.

## 📂 Dataset

Saved notebook output reports **2,644 sentiment records × 4 fields** and **211,224 trade records × 16 fields** at the initial load.

- **Sentiment fields:** timestamp, value, classification, date.
- **Trade fields include:** account, coin, execution price, size, side, timestamp, closed PnL, fees, and trade identifiers.
- **Data quality warning:** A notebook message says “Rows before cleaning: 65149” but later reports 211,224 rows after `dropna()`. This inconsistency must be corrected before claiming cleaning improved the dataset.
- **Privacy:** Account addresses and transaction hashes appear in trade data; avoid publishing them in screenshots or examples.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python/pandas | Data preparation and analysis |
| Jupyter Notebook | Exploration |
| scikit-learn/XGBoost | Only if confirmed in the notebook |

## 🔄 Project Workflow

1. Open the notebook and review data loading and transformations.
2. Inspect Output table.csv and the short write-up for fields, dates, units, and provenance.
3. Check missing values, duplicate rows, time zones, and alignment between sentiment and performance.
4. Define the target and determine what information would be available at prediction time.
5. Explore distributions and relationships with visualizations.
6. If modelling, use chronological splits and simple baselines.
7. Evaluate on a held-out period and interpret findings as associations unless causal design supports more.

## 🗂️ Repository Structure

```text
Trader_Performance_vs_Market_Sentiment_Analysis/
├── Trader_Performance_vs_Market_Sentiment_Analysis.ipynb
├── Output table.csv
├── A short write-up
└── LICENSE
└── README.md
```

The list above highlights known project files and folders; inspect the repository for the complete current structure.

## ⚙️ Installation

### Prerequisites

- Install the tools listed in the Tech Stack that apply to this project.
- For Python projects, use a Python version compatible with the dependencies actually imported by the code.
- For Power BI projects, use Power BI Desktop.

### Setup

Open the notebook in Jupyter/Colab and install packages imported by it. A requirements.txt was not listed at the repository root.

Do not run generic commands that do not match the files in this repository. Confirm the data paths, database dialect, and package versions before execution.

## ▶️ Usage

Run the notebook from top to bottom after confirming data paths. Read the short write-up alongside the output table.

## 📊 Results and Insights

### Saved notebook model evaluation

| Metric | Saved result |
|---|---:|
| Best model | Random Forest |
| Accuracy | 0.8077 (80.77%) |
| F1-score | 0.8515 |
| Test examples in classification report | 468 |

Saved feature importance was led by `long_ratio` (0.4237), `n_trades` (0.2073), `avg_leverage` (0.1654), and `avg_trade_size` (0.1557). These are model associations, not causal effects.

The provided `Output table.csv` summarizes PnL statistics by sentiment category. Descriptive differences do not establish that sentiment caused trading performance. Metrics above are saved notebook outputs, not independently reproduced results; verify joins, target definition, and the inconsistent cleaning log before using them as final claims.

## 🖼️ Screenshots

No image files were confirmed for this repository during this update. If you have screenshots, upload them into an `images/` folder, then embed each real path here with a short caption. Do not use placeholder image paths.

## 🧩 Challenges and Solutions

| Challenge | Solution / validation approach |
|---|---|
| Time alignment and leakage | Ensure sentiment values precede the outcomes they are used to explain or predict. |

## ⚠️ Limitations

- The notebook cleaning log is inconsistent (65,149 before cleaning vs. 211,224 after); resolve this before publication.
- Model metrics are saved notebook outputs and were not independently reproduced.
- Account addresses and transaction hashes may be sensitive identifiers.
- Sentiment/performance associations do not prove causation or establish a profitable trading strategy.

## 🚀 Future Improvements

- [ ] Document data source and time alignment.
- [ ] Add charts and verified results.
- [ ] Add baseline metrics and leakage checks if modelling.

## 📚 What I Learned

- Time-aware analysis and feature validation.
- Separating association from prediction.

## 👤 Author

**Sahil Gaikwad**

- GitHub: [sahil2003-ai](https://github.com/sahil2003-ai)
- LinkedIn: [Sahil Gaikwad](https://www.linkedin.com/in/sahil-gaikwad-a76b7224a/)

## 📄 License

A LICENSE file is present; review its terms and the data source terms.
