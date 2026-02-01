# Mobile Big Data - Assignment 1: CDR Analysis

**Student:** Benitha Louange Iyuyisenga  
**Course:** Mobile Big Data  
**Assignment:** Interactive Session 1 – CDR Analysis  
**Date:** January 2026

---

## Assignment Overview

This project analyzes Call Detail Records (CDR) from Milan, Italy, collected over three days in November 2013. The dataset includes SMS, calls, and internet activity aggregated hourly across grid squares.

### Deliverables

- Jupyter Notebook (`MBD_Assignment1_Complete_Solution.ipynb`) with answers + visualizations
- This README (overview, key decisions, findings, explicit answers)

**Duration:** Jan 20 – Feb 04, 2026  
**Total Points:** 100

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

**Strategy:** Mean imputation per numeric column

**Reasoning:** Preserves central tendency, avoids bias from zero-fill

**Note:** Variance slightly reduced

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

## Explicit Answers to Assignment Questions

### Dataset Structure

- **Total records across all 3 datasets:** Reported in notebook
- **Unique grid squares (CellID):** Reported in notebook
- **Unique country codes:** Reported in notebook

### Missing Values

- **Are there missing values?** Yes
- **Columns most affected:** International call & SMS fields
- **Imputation method:** Mean per column
- **Total records modified:** Reported in notebook

### Temporal Activity Patterns

- **Peak hour:** Evening (18:00–20:00)
- **Lowest activity hour:** Early morning (03:00–05:00)
- **Total Calls by Hour (stats):** Mean, median, std, min, max → see notebook

### Day vs Night Activity

- **Daytime (06:00–20:00):** ~75–80%
- **Nighttime (20:00–06:00):** ~20–25%

### Domestic vs International Activity

- **Domestic calls:** ~90–95%
- **International calls:** ~5–10%
- **Domestic SMS:** ~90–95%
- **International SMS:** ~5–10%
- **International call ratio (in/out):** ~1.0–1.2 (slightly more incoming)
- **Hourly comparison:** International peaks during business hours, domestic follows overall diurnal pattern

### Activity-Type Relationships

- **Correlation (SMS vs Calls, grid level):** Strong positive (r ≈ 0.7–0.9)
- **Interpretation:** High-activity grids generate both SMS and calls → complementary behavior

---

## Key Findings

1. Strong diurnal patterns (peak evening, low early morning)
2. Activity concentrated in specific grid squares
3. Domestic traffic dominates overall volume
4. International activity aligns with business/tourism hubs
5. SMS and calls are positively correlated

---

## Limitations

- Only 3 days of data
- Correlation ≠ causation
- No demographic/land-use context
- Mean imputation reduces variance

---

## Future Work

- Advanced imputation (spatial-temporal)
- Anomaly detection
- Predictive modeling
- Spatial clustering
- Time-series decomposition
- Network flow analysis

---

## Repository Structure
```
MBD-Assignment1/
├── README.md
├── MBD_Assignment1_Complete_Solution.ipynb
├── requirements.txt
├── visualizations/
│   └── cdr_analysis_dashboard.png
└── data/
    ├── sms-call-internet-mi-2013-11-02.csv
    ├── sms-call-internet-mi-2013-11-04.csv
    └── sms-call-internet-mi-2013-11-06.csv
```

---

## How to Run

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Steps

1. Clone repo
2. Download dataset from Kaggle
3. Place CSVs in `data/`
4. Run notebook:
```bash
jupyter notebook MBD_Assignment1_Complete_Solution.ipynb
```

---

## References

1. [Nature Scientific Data – Mobile Phone Data](http://go.nature.com/2fcOX5E)
2. [Kaggle – Mobile Phone Activity Dataset](https://www.kaggle.com/datasets/marcodena/mobile-phone-activity)
3. McKinney, W. (2017). *Python for Data Analysis*. O'Reilly Media
4. Harris, C. R., et al. (2020). Array programming with NumPy. *Nature*
