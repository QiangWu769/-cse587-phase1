# CSE 4/587 — End-to-End Big Data Pipeline

## S&P 500 Stock Prices Analysis (2014–2017)

### Project Overview
This project builds an end-to-end big data pipeline using Hadoop and Spark to analyze S&P 500 stock market data.

- **Phase 1:** Problem definition, data acquisition, HDFS ingestion, data cleaning, and exploratory data analysis.
- **Phase 2:** Large-scale machine learning using PySpark MLlib (classification, regression, clustering) and in-depth data analysis.

### Team Members
| Name | UBIT |
|------|------|
| Harshvardhan Shinde | hdshinde |
| Lorenzo Price | lorenzop |
| Qiang Wu | qiangwu2 |

### Dataset
- **Source:** [Kaggle — S&P 500 Stock Prices](https://www.kaggle.com/datasets/gauravmehta13/sp-500-stock-prices) (CC0 Public Domain)
- **Size:** 497,472 rows × 7 columns (raw) → 497,460 rows × 16 columns (cleaned)
- **Time Span:** January 2014 – December 2017
- **Coverage:** 505 S&P 500 component stocks (daily OHLCV data)

### Project Structure
```
├── phase1/
│   ├── Phase1_Report.ipynb          # Full Phase 1 report notebook (Tasks 1-5)
│   ├── Phase1_Report.html           # HTML version
│   ├── Phase1_Report.pdf            # PDF version
│   ├── phase1_task4_5.ipynb         # Executable notebook for data cleaning & EDA
│   ├── hdfs_screenshot.png          # HDFS verification screenshot
│   ├── sp500_companies.csv          # Supplementary sector data
│   ├── work_division.md             # Team work division
│   ├── meetings_log.md              # Team meetings log
│   └── Project Phase 1 (1).pdf     # Assignment specification
│
├── phase2/
│   ├── Phase2_Report_executed.ipynb  # Full Phase 2 report with outputs
│   ├── Phase2_Report.html            # HTML version
│   ├── Phase2_Report.pdf             # PDF version
│   ├── phase2_notebook_source.ipynb  # Source notebook (no outputs)
│   └── Project Phase 2.pdf          # Assignment specification
│
└── README.md
```

---

## Phase 1 (100 pts)

| Task | Description | Points |
|------|-------------|--------|
| Task 1 | Problem Statement (3 ML problems) | 20 pts |
| Task 2 | Data Sources & Citations | 15 pts |
| Task 3 | HDFS Utilization (raw + cleaned data) | 15 pts |
| Task 4 | Data Cleaning (6 operations) | 25 pts |
| Task 5 | Exploratory Data Analysis (6 EDA operations) | 25 pts |

---

## Phase 2 (100 pts)

### Task 1: Spark ML (50 pts)
Three ML algorithms implemented with PySpark MLlib:

| Problem | Algorithm | Key Metrics |
|---------|-----------|-------------|
| Classification (stock direction) | Random Forest | Accuracy, F1, AUC-ROC |
| Regression (daily return) | Gradient-Boosted Trees | RMSE, MAE, R² |
| Clustering (stock grouping) | K-Means | Silhouette Score |

- Hyperparameter tuning via 3-fold cross-validation with grid search
- Feature engineering with lagged features to prevent data leakage
- Baseline comparisons for regression model

### Task 2: Data Analysis Objectives (30 pts)
Six analysis objectives addressed using Spark:

1. Daily return distribution — normality testing, fat tails
2. Sector-level performance — risk-return profiles by GICS sector
3. Temporal patterns — day-of-week, monthly, and yearly effects
4. Correlation analysis — feature redundancy and selection
5. Volatility ranking — most/least volatile stocks by sector
6. Volume spikes — relationship with market events

### Task 3: Presentation (20 pts)
5-minute video covering Phase 1 and Phase 2.

---

## How to Reproduce

### 1. Clone the repo
```bash
git clone https://github.com/QiangWu769/-cse587-phase1.git
cd -- -cse587-phase1
```

### 2. Install dependencies
```bash
pip install pyspark pandas numpy matplotlib seaborn scipy jupyter
```

### 3. Download the dataset
Download from [Kaggle](https://www.kaggle.com/datasets/gauravmehta13/sp-500-stock-prices) and place `cleaned_sp500.csv` in the project root.

### 4. Run Phase 2 notebook
```bash
cd phase2
jupyter notebook Phase2_Report_executed.ipynb
```

### Tools Used
- Python (pandas, matplotlib, seaborn, scipy)
- PySpark MLlib (RandomForest, GBT, KMeans)
- Jupyter Notebook
- Hadoop HDFS (Docker: apache/hadoop:3)
