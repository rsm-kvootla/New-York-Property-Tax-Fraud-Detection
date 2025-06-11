# New York Property Tax Fraud Detection

## Project Overview

This project develops a data-driven, unsupervised fraud detection framework to identify potentially misreported or under-assessed properties within the New York City property tax dataset. With over 1 million property records, even small anomalies can result in substantial lost revenue. By combining engineered valuation ratios, geographic normalization, and anomaly detection algorithms, this project provides a scalable solution to highlight suspicious properties for further investigation.

## Methods

Two unsupervised machine learning techniques were used:

- **PCA + Minkowski Distance**: Projects records into a reduced-dimension space and identifies outliers based on Euclidean distance from the dataset center.
- **Autoencoder + Reconstruction Error**: Uses a shallow neural network to reconstruct input features and flags records with high reconstruction error.

The final fraud score is the **average of both methods**, allowing for a balanced detection of both linear and nonlinear anomalies.

## Data Preparation

- **Dataset**: 1,070,994 NYC property records (2010–2011)
- **Cleaning**:
  - Excluded public/civic records
  - Imputed missing values using contextual logic (e.g., grouped by tax class & borough)
- **Feature Engineering**:
  - 9 valuation ratios (r1–r9), normalized by ZIP and Tax Class
  - Composite indicators: `value_ratio`, `size_ratio`
  - Derived features like `bldsize`, `bldvol`, `ltsize`

## Evaluation & Results

- Properties were scored using PCA and autoencoder models, then ranked.
- Top 1–5% of records were flagged for auditing.
- Visual diagnostics included heatmaps and owner-frequency bar charts.
- **Notable fraud indicators**:
  - Large buildings with zero market value
  - Properties with more building volume than lot size
  - Implausible tax class assignments


## Financial Relevance

- Focused on identifying the most anomalous properties for **auditor prioritization**
- Suitable for integration into tax enforcement workflows or city compliance dashboards
- Scalable to larger datasets and adaptable to include expert feedback or new valuation fields

## Case Studies

Examples of flagged records:
- **Record #718883**: 14-story building with market value of only $12
- **Record #349361**: Reported as 1 story but visibly 5 stories tall
- **Record #95620**: Physically impossible structure footprint, likely entry error or manipulation

## Tech Stack

Python, Pandas, NumPy, Scikit-learn, TensorFlow (Keras), Matplotlib, Seaborn, Jupyter Notebook

## Repository Structure

| File                                | Description                                           |
|-------------------------------------|-------------------------------------------------------|
| `data_cleaning.ipynb`               | Removes non-risk records, imputes missing data       |
| `feature_engineering.ipynb`         | Creates ratios and normalized variables              |
| `pca_autoencoder_modeling.ipynb`    | Implements PCA + Minkowski and Autoencoder methods   |
| `visualizations.ipynb`              | Generates score plots, heatmaps, and bar charts      |

## Data
- For original data file, please contact me at kvootla@ucsd.edu (source: https://data.cityofnewyork.us/Housing-Development/Property-Valuation-and-Assessment-Data/rgy2-tti8)
- A data dictionary is attached for your perusal 

## Key Outcomes

- Delivered a robust, interpretable fraud risk score for every NYC property
- Identified thousands of records with extreme underassessment or structural inconsistencies
- Provided visual tools for investigators to explore anomalies by variable or by owner

