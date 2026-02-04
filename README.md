# Mobile Big Data - Assignment 1: CDR Analysis

**Student:** Benitha Louange Iyuyisenga  
**andrewID:** biyuyise
--- 
### GitHub Repo 
[https://github.com/benitha200/MBD-CALL-DETAILS-RECORD-ANALYSIS.git](https://github.com/benitha200/MBD-CALL-DETAILS-RECORD-ANALYSIS.git) 
---

## Assignment Overview

This project analyzes Call Detail Records (CDR) from Milan, Italy, collected over three days in November 2013. The dataset includes SMS, calls, and internet activity aggregated hourly across grid squares.

### Deliverables

- Jupyter Notebook (`MBD_Assignment1_biyuyise.ipynb`) with key findings + visualizations  
- This README (overview, key decisions, findings)
---

## Dataset Information

### Files

- `sms-call-internet-mi-2013-11-02.csv`  
- `sms-call-internet-mi-2013-11-04.csv`  
- `sms-call-internet-mi-2013-11-06.csv`

### Specifications

- **Spatial Resolution:** 235m × 235m grid squares (CellID)  
- **Temporal Resolution:** Hourly (60 minutes)  
- **Activity Types:** SMS (in/out), Calls (in/out), Internet usage  
- **Coverage:** Milan metropolitan area  

---

## Approach

### 1. Data Loading & Integration
- Loaded all 3 CSVs with pandas  
- Combined using `pd.concat(ignore_index=True)`  
- Added date and hour columns  

**Decision:** Concatenation chosen (no relational join needed)

### 2. Feature Engineering
**Extracted:**  
- Hour of day  
- Date  
- Day of week  

**Classified time:**  
- **Daytime:** 06:00–20:00  
- **Nighttime:** 20:00–06:00  

### 3. Missing Value Handling
- **Strategy:** Mean imputation per numeric column  
- **Reasoning:** Preserves central tendency, avoids bias from zero-fill  
- **Note:** Variance slightly reduced  

### 4. Aggregate Features
```python
total_sms = smsin + smsout
total_calls = callin + callout
total_internet = internet
total_activity = total_sms + total_calls + total_internet
```

### 5. Statistical Analysis
- **Pandas:** groupby, descriptive stats, proportions  
- **NumPy:** mean, std, percentile, corrcoef  
- Compared domestic vs international activity  

---

### Dataset Structure
- **Total records analyzed:** 6,564,031  
- **Unique grid squares (CellID):** 10,000  
- **Unique country codes:** 302  
- **Records per day:** Nov 2 -> 1,847,331; Nov 4 -> 2,299,544; Nov 6 -> 2,417,156  

### Missing Values
- **Records with missing values:** 21,137,195  
- **Columns most affected:** International call & SMS fields  
- **Imputation method:** Mean per column  

### Temporal Activity Patterns
- **Peak activity hour:** 17:00  
- **Lowest activity hour:** 04:00  
- **Daytime activity:** 73.6%  
- **Nighttime activity:** 26.4%  

### Domestic vs International Activity
- **Domestic calls:** 33.1%  
- **International calls:** 66.9%  
- **International incoming/outgoing ratio:** 1.67  

### Activity-Type Relationships
- **Correlation (SMS vs Calls):** 0.986 (very strong positive)  
- **Correlation (Domestic vs International patterns):** 0.986  

---

## Key Findings

1. **High international traffic:** International calls dominate (≈67%), suggesting Milan’s role as a global hub.  
2. **Temporal rhythms:** Clear diurnal cycle with peak activity at 17:00 and lowest at 04:00.  
3. **Day vs night split:** Daytime accounts for nearly three-quarters of activity.  
4. **Strong correlations:** SMS and calls are almost perfectly correlated, as are domestic vs international patterns.  
5. **Data quality challenge:** Over 21 million missing values required imputation, slightly reducing variance.  

---


## Repository Structure
```
MBD-Assignment1/
├── README.md
├── MBD_Assignment1_Complete_Solution.ipynb
├── requirements.txt
```

---

## How to Run

### Prerequisites
```bash
pip install -r requirements.txt
```

### Steps
1. Clone repo  
2. Download dataset from Kaggle  
3. Place CSVs in `data/`  
4. Run notebook:
```bash
jupyter notebook MBD_Assignment1_biyuyise.ipynb
```

---


## References
 
2. [Kaggle – Mobile Phone Activity Dataset](https://www.kaggle.com/datasets/marcodena/mobile-phone-activity)  

