# CSE 4/587 — End-to-End Big Data Pipeline (Phase 1)

## S&P 500 Stock Prices Analysis (2014–2017)

### Project Overview
This project builds an end-to-end big data pipeline using Hadoop and Spark to analyze S&P 500 stock market data. Phase 1 covers problem definition, data acquisition, HDFS ingestion, data cleaning, and exploratory data analysis.

### Dataset
- **Source:** [Kaggle — S&P 500 Stock Data](https://www.kaggle.com/datasets/camnugent/sandp500) (CC0 Public Domain)
- **Size:** 497,472 rows × 7 columns
- **Time Span:** January 2014 – December 2017
- **Coverage:** 505 S&P 500 component stocks (daily OHLCV data)

### Project Structure
```
├── Phase1_Report.ipynb        # Full report notebook (Tasks 1-5)
├── Phase1_Report.html         # HTML version of the report
├── phase1_task4_5.ipynb       # Executable notebook for data cleaning & EDA
├── hdfs_screenshot.png        # HDFS verification screenshot
├── work_division.md           # Team work division
├── meetings_log.md            # Team meetings log
└── Project Phase 1 (1).pdf   # Assignment specification
```

### Tasks Completed
| Task | Description | Points |
|------|-------------|--------|
| Task 1 | Problem Statement | 20 pts |
| Task 2 | Data Sources & Citations | 15 pts |
| Task 3 | HDFS Utilization (raw + cleaned data) | 15 pts |
| Task 4 | Data Cleaning (6 operations) | 25 pts |
| Task 5 | Exploratory Data Analysis (6 EDA operations) | 25 pts |

### How to Reproduce

#### 1. Clone the repo
```bash
git clone https://github.com/QiangWu769/-cse587-phase1.git
cd -cse587-phase1
```

#### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

#### 3. Download the dataset
Download from [Kaggle](https://www.kaggle.com/datasets/camnugent/sandp500) and place the CSV file in the project root:
```
S&P 500 Stock Prices 2014-2017.csv
```

#### 4. Run the notebooks
```bash
jupyter notebook phase1_task4_5.ipynb
```
This will execute data cleaning (Task 4) and EDA (Task 5), and generate `cleaned_sp500.csv`.

#### 5. HDFS ingestion (Task 3)
```bash
# Start Hadoop via Docker
docker pull apache/hadoop:3
docker run -d --name hadoop --platform linux/amd64 \
  -v "$(pwd):/data" apache/hadoop:3 sleep infinity

# Inside the container: configure and start HDFS
docker exec hadoop bash -c "
  export HADOOP_HOME=/opt/hadoop
  export PATH=\$HADOOP_HOME/bin:\$HADOOP_HOME/sbin:\$PATH
  cat > \$HADOOP_HOME/etc/hadoop/core-site.xml << 'EOF'
<configuration>
  <property><name>fs.defaultFS</name><value>hdfs://localhost:9000</value></property>
</configuration>
EOF
  cat > \$HADOOP_HOME/etc/hadoop/hdfs-site.xml << 'EOF'
<configuration>
  <property><name>dfs.replication</name><value>1</value></property>
</configuration>
EOF
  hdfs namenode -format -force
  hdfs namenode &
  sleep 5
  hdfs datanode &
  sleep 5
  hdfs dfs -mkdir -p /user/project/raw
  hdfs dfs -mkdir -p /user/project/cleaned
  hdfs dfs -put '/data/S&P 500 Stock Prices 2014-2017.csv' /user/project/raw/
  hdfs dfs -put /data/cleaned_sp500.csv /user/project/cleaned/
  hdfs dfs -ls -R /user/project/
"
```

### Tools Used
- Python (pandas, matplotlib, seaborn)
- Jupyter Notebook
- Hadoop HDFS (Docker: apache/hadoop:3)
