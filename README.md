# Trader Performance vs. Market Sentiment Analysis

A data-science analysis exploring how daily trader performance metrics vary across Fear & Greed sentiment categories.

![Status](https://img.shields.io/badge/Status-Documented-yellow)

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Objectives](#-objectives)
- [Features](#-features)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Project Workflow](#-project-workflow)
- [Repository Structure](#-repository-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Results and Insights](#-results-and-insights)
- [Screenshots](#-screenshots)
- [Challenges and Solutions](#-challenges-and-solutions)
- [Limitations](#-limitations)
- [Future Improvements](#-future-improvements)
- [What I Learned](#-what-i-learned)
- [Author](#-author)
- [License](#-license)

## 📖 Overview

A data-science analysis exploring how daily trader performance metrics vary across Fear & Greed sentiment categories.

## 🎯 Problem Statement

The project addresses a data-analysis or modeling question using the dataset and implementation available in this repository. The aim is to produce transparent, reproducible evidence rather than unsupported performance claims.

## 🎯 Objectives

- Understand the data and define the target or business question.
- Document data preparation, feature engineering, and analysis/modeling steps.
- Report available metrics with their evidence and validation status.
- Make the workflow reproducible and explain limitations.

## ✨ Features

The project features are documented in the notebooks, scripts, and outputs. See the source files for the precise implementation.

## 📂 Dataset

Document the exact source, dimensions, fields, target definition, missing values, and license from the repository's actual data files.

## 🛠️ Tech Stack

List only the libraries and tools directly evidenced in source files and dependency manifests.

## 🔄 Project Workflow

1. Load and validate the data.\n2. Inspect data quality and target definitions.\n3. Run analysis or train models.\n4. Evaluate results using an appropriate validation strategy.\n5. Document findings and limitations.

## 🗂️ Repository Structure

| File | Purpose |
|---|---|
| `Trader_Performance_vs_Market_Sentiment_Analysis.ipynb` | Data preparation, aggregation, and modeling experiments |
| `Output table.csv` | Summary statistics by sentiment category |
| `A short write-up` | Methodology and descriptive interpretation |
| `LICENSE` | Repository license |

## ⚙️ Installation

1. Confirm paths and provenance for the underlying sentiment and trade datasets.
2. Parse timestamps and time zones consistently.
3. Validate merge coverage and resolve the cleaning-log discrepancy.
4. Check missing values and duplicate keys at the intended data grain.
5. Recreate sentiment-level summaries and compare with the saved CSV.
6. If modeling, define the target, use time-aware validation, compare a baseline, and report per-class metrics.

## ▶️ Usage

1. Confirm paths and provenance for the underlying sentiment and trade datasets.
2. Parse timestamps and time zones consistently.
3. Validate merge coverage and resolve the cleaning-log discrepancy.
4. Check missing values and duplicate keys at the intended data grain.
5. Recreate sentiment-level summaries and compare with the saved CSV.
6. If modeling, define the target, use time-aware validation, compare a baseline, and report per-class metrics.

## 📊 Results and Insights

| Sentiment | Mean daily PnL | Median daily PnL | Mean PnL/trade | Days | Mean trades/day | Long ratio |
|---|---:|---:|---:|---:|---:|---:|
| Extreme Fear | 52,793.59 | 22,561.74 | 38.43 | 14 | 1,528.57 | 0.49 |
| Extreme Greed | 23,817.29 | 3,127.54 | 56.74 | 114 | 350.81 | 0.46 |
| Fear | 36,891.82 | 1,412.31 | 31.28 | 91 | 679.53 | 0.51 |
| Greed | 11,140.57 | 678.48 | 39.41 | 193 | 260.64 | 0.49 |
| Neutral | 19,297.32 | 1,818.57 | 63.82 | 67 | 562.48 | 0.50 |

PnL units/currency are not specified in the available outputs. The table reports associations across the merged sample; it does not mean sentiment caused the differences or that a sentiment-based trading strategy will be profitable.

## 🖼️ Screenshots

Add genuine charts or app screenshots stored in the repository. Do not use mock screenshots or claim that a file exists unless verified.

## 🧩 Challenges and Solutions

| Challenge | Solution |
|---|---|
| Saved outputs may not match current data or dependencies | Rerun the workflow and compare fresh outputs. |
| High model scores can be caused by leakage or an unsuitable split | Validate feature timing, target construction, split strategy, and baseline. |
| Results may be hard to reproduce | Document package versions, input paths, and random seeds where applicable. |

## ⚠️ Limitations

- Data cleaning and row-count notes are inconsistent and need reconciliation.
- The reported model metrics were not independently reproduced.
- Account addresses and transaction hashes can identify accounts; avoid exposing them in screenshots or reports.
- Correlation and grouped PnL differences do not establish causality or a reliable trading strategy.

## 🚀 Future Improvements

- [ ] Rerun the pipeline and verify all saved metrics.
- [ ] Document dataset provenance and data dictionary.
- [ ] Add genuine output screenshots and a reproducible model comparison.

## 📚 What I Learned

- Building a reproducible data science workflow.
- Choosing and interpreting task-appropriate evaluation metrics.
- Separating descriptive associations from causal claims.
- Documenting model limitations alongside results.

## 👤 Author

**Sahil Gaikwad**

- GitHub: [sahil2003-ai](https://github.com/sahil2003-ai)
- LinkedIn: [Sahil Gaikwad](https://www.linkedin.com/in/sahil-gaikwad-a76b7224a/)

## 📄 License

Confirm the repository license and dataset reuse terms before redistribution.