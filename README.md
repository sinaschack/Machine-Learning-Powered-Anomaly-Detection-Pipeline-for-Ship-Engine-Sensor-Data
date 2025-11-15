# Machine-Learning-Powered-Anomaly-Detection-Pipeline-for-Ship-Engine-Sensor-Data
End-to-end data science project applying statistical analysis and unsupervised machine learning to detect anomalous operational behaviour in ship engine telemetry.

## Overview

This project develops a robust anomaly detection system for monitoring ship engine performance using real-time sensor data. The objective is to identify abnormal behaviour—such as overheating, pressure spikes, or unstable operating states—that may indicate developing mechanical issues. The analysis supports predictive maintenance, improves fleet reliability, and reduces operational downtime by prioritising engine readings that require human inspection.

## Dataset

The dataset contains **19,535 observations** across **six key engine features**:

* **Engine RPM**
* **Lubrication Oil Pressure**
* **Fuel Pressure**
* **Coolant Pressure**
* **Lubrication Oil Temperature**
* **Coolant Temperature**

Historical patterns suggest that **1–5%** of readings are expected to be anomalous.

## Skills Demonstrated

* Exploratory data analysis (EDA) and descriptive statistics
* Outlier detection using IQR and multivariate methods
* Machine learning for anomaly detection (One-Class SVM & Isolation Forest)
* Dimensionality reduction and visualisation (PCA)
* Parameter tuning for rare-event detection
* Interpreting engineering telemetry to support operational decision-making

## Methodology

### 1. **Data Preprocessing**

* Checked and cleaned 19k+ engine readings
* Standardised all features
* Conducted descriptive analysis to identify skewness, bimodality, and extreme values

### 2. **Statistical Anomaly Detection (IQR Method)**

* Applied IQR thresholds for each sensor
* Flagged anomalies when **two or more features exceeded IQR bounds**
* Identified **411 anomalies (2.16%)**, aligning with the expected 1–5% range
* Features most associated with anomalies:

  * **Lub Oil Temperature** (13.4% individual outliers)
  * **Fuel Pressure** (5.81%)

### 3. **Machine Learning Models**

#### **One-Class SVM**

* Tuned *nu* and *gamma* to control anomaly sensitivity
* Identified optimal *nu* range: **0.0014 – 0.049** (producing 1–5% anomalies)
* PCA plots and decision boundary visualisations confirmed stability
* Provided fine-grained control and reliable detection patterns

#### **Isolation Forest**

* Anomaly rate driven almost entirely by **contamination parameter**
* *n_estimators* and *random_state* showed negligible influence
* Less flexible and more sensitive to misconfiguration
* Exhibited limited adaptability for complex engine behaviour

### 4. **Dimensionality Reduction & Visualisation (PCA)**

* Reduced six sensor features to two principal components
* Visualised anomaly clusters across all methods
* Demonstrated clear separation of abnormal states driven by temperature and pressure fluctuations

## Key Findings

* The **IQR method** successfully identified 2.16% anomalies, offering a transparent baseline.
* **One-Class SVM** was the most effective ML model:

  * Stable performance across the 1–5% anomaly threshold
  * Strong sensitivity control via *nu* and *gamma*
* **Isolation Forest** was less reliable due to heavy dependence on contamination.
* Temperature-related features (especially **Lub Oil Temp**) had the highest anomaly concentration.
* PCA visualisation consistently revealed clusters tied to high RPM, overheating, and pressure spikes.

## Conclusions and Recommendations

### **Most Effective Method**

**One-Class SVM** provided the most accurate and controllable anomaly detection, outperforming Isolation Forest and offering reliable alignment with expected anomaly levels.

### **Alignment with Expected 1–5% Range**

* One-Class SVM met the requirement using *nu* ∈ **[0.0014, 0.049]**
* Isolation Forest matched the range only when contamination was manually forced
* IQR results supported machine learning findings, highlighting temperature and pressure features as dominant anomaly drivers

### **Next Steps**

* Conduct expert review of automatically flagged anomalies
* Fine-tune SVM model parameters based on engineering feedback
* Deploy system for real-time monitoring of ship engine health
* Integrate alerting mechanisms to reduce breakdowns and minimise delays
