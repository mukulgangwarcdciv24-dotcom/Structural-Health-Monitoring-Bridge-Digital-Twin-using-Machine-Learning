# Structural Health Monitoring: Bridge Digital Twin using Machine Learning

## Overview

This project develops a complete Machine Learning pipeline for Structural Health Monitoring (SHM) of a bridge digital twin. Using 43,200 sensor readings collected at one-minute intervals, the system identifies structural states, detects anomalies, predicts risk events, and generates actionable maintenance recommendations.

The project combines unsupervised learning, supervised learning, and civil engineering domain knowledge to create an interpretable bridge monitoring framework.

---

## Problem Statement

Bridges are continuously exposed to traffic loading, environmental effects, material deterioration, and seismic activity. Traditional inspections are periodic and may fail to identify emerging structural issues before they become critical.

The objective of this project is to develop an ML-based Structural Health Monitoring system capable of:

- Detecting abnormal structural behavior
- Classifying bridge health states
- Predicting anomaly events
- Supporting proactive maintenance decisions

---

## Dataset

### Dataset Statistics

| Metric | Value |
|----------|----------|
| Total Readings | 43,200 |
| Total Features | 54 |
| Selected Features | 13 |
| Time Resolution | 1 Minute |
| Time Period | January 2023 |

### Selected Features

- Strain
- Deflection
- Tilt
- Displacement
- Crack Propagation
- Cable Tension
- Corrosion Level
- Vehicle Load
- Traffic Volume
- Vibration
- Wind Speed
- Seismic Activity
- Soil Settlement

---

## Data Preprocessing

### Missing Value Treatment

Approximately 4% of observations contained missing values.

To preserve temporal continuity, missing values were handled using:

- Forward Fill (ffill)
- Backward Fill (bfill)

### Feature Scaling

All features were standardized using StandardScaler to ensure comparable feature magnitudes across machine learning models.

---

## Feature Selection

Instead of automated feature selection, 13 features were selected using civil engineering domain expertise.

This approach ensures:

- Physical interpretability
- Engineering relevance
- Reduced risk of circular learning
- Improved explainability of results

---

# Machine Learning Pipeline

## 1. K-Means Clustering

### Objective

Identify distinct structural states without using labels.

### Configuration

- Number of Clusters: 3

### Results

| Cluster | Readings | Share |
|----------|----------|----------|
| Healthy | 16,038 | 37.1% |
| Moderate Stress | 15,968 | 37.0% |
| Critical | 11,194 | 25.9% |

### Key Insight

The Critical cluster exhibited significantly higher strain, traffic load, cable tension, and anomaly rates than the Healthy and Moderate Stress clusters.

---

## 2. Isolation Forest

### Objective

Detect anomalies using unsupervised learning.

### Configuration

- Contamination Rate: 5%

### Results

- Total Anomalies Detected: 2,160
- Anomaly Rate: 5.0%

### Most Influential Features

1. Strain
2. Cable Tension
3. Traffic Volume
4. Vehicle Load
5. Vibration

### Key Insight

The Critical cluster showed a 16% anomaly rate compared to approximately 1.1–1.2% in the Healthy and Moderate Stress clusters.

---

## 3. Random Forest Classifier

### Objective

Predict anomaly events from raw sensor readings.

### Configuration

- 200 Trees
- Maximum Depth = 10
- Class Weight = Balanced
- Chronological 80/20 Train-Test Split

### Performance Metrics

| Metric | Value |
|----------|----------|
| Accuracy | 93.3% |
| ROC-AUC | 0.897 |
| Precision | 0.20 |
| Recall | 0.42 |
| F1 Score | 0.27 |

### Top Features

1. Deflection
2. Tilt
3. Strain
4. Wind Speed
5. Traffic Volume

### Key Insight

The model achieved strong discriminative performance with a ROC-AUC of 0.897 while maintaining a realistic chronological train-test split.

---

## Maintenance Decision Engine

A rule-based maintenance engine combines outputs from:

- Isolation Forest
- Random Forest
- Maintenance Alert Indicator

### Alert Levels

| Score | Alert Level | Action |
|----------|----------|----------|
| 0 | GREEN | No Action Required |
| 1 | YELLOW | Monitor Closely |
| 2 | ORANGE | Schedule Inspection |
| 3 | RED | Immediate Action Required |

This converts machine learning outputs into actionable engineering decisions.

---

## Key Findings

- Critical structural states exhibit significantly higher anomaly rates.
- K-Means and Isolation Forest independently validate each other's results.
- Random Forest achieved a ROC-AUC of 0.897.
- Strain and Cable Tension dominate unsupervised anomaly detection.
- Deflection and Tilt dominate supervised anomaly prediction.
- Combining multiple models improves monitoring reliability.

---

## Technologies Used

### Programming

- Python

### Libraries

- Pandas
- NumPy
- Scikit-Learn
- Matplotlib
- Seaborn

### Machine Learning

- K-Means Clustering
- Principal Component Analysis (PCA)
- Isolation Forest
- Random Forest

---

## Future Improvements

- Real-world bridge sensor deployment
- LSTM-based time-series forecasting
- Transformer-based anomaly detection
- Finite Element Model integration
- Real-time monitoring dashboard
- Live anomaly alert system

---

## Repository Structure

```
structural-health-monitoring-bridge-digital-twin/
│
├── README.md
├── SHM_Bridge_v3.ipynb
├── SHM_Bridge_Report.pdf
├── SHM_Bridge_Presentation.pptx
├── SHM_Bridge_Digital_Twin.html
├── bridge_digital_twin_dataset.csv
└── images/
    ├── kmeans_clusters.png
    ├── anomaly_distribution.png
    └── feature_importance.png
```

---

## Author

**Mukul Gangwar**  
B.Tech Civil Engineering  
IIT (BHU) Varanasi
