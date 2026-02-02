# -Crypto-PCA-analysis
A quantitative analysis tool that uses Principal Component Analysis (PCA) to identify correlations between various cryptocurrencies and Bitcoin. The script filters signals based on the statistical significance (p-value) of historical correlation patterns and identifies potential entry points based on standard deviation (sigma) from the norm.

---

# 📈 Statistical Arbitrage & Market Decomposition (PCA)

This project implements a sophisticated analytical pipeline for cryptocurrency markets using **Principal Component Analysis (PCA)** and **Econometric Modeling**. It aims to decompose market movements into systematic factors and identify tradeable statistical anomalies (Mean Reversion) using the Augmented Dickey-Fuller (ADF) test.

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## 🎯 Project Objectives
The primary goal is to move beyond simple price action and analyze the **underlying structure** of the market:
1.  **Dimensionality Reduction**: Identifying the "Market Factor" vs. "Idiosyncratic Deviations."
2.  **Anomaly Detection**: Spotting assets that are significantly decoupled from the general market trend.
3.  **Spread Modeling**: Creating a beta-neutral spread between an outlier asset and the market leader (BTC).
4.  **Statistical Verification**: Testing the spread for stationarity to confirm mean-reverting behavior.

## 🛠 Project Workflow

### 1. Dynamic Universe Selection
The script automatically queries the Binance API to fetch the **Top N assets by 24h volume**. 
*   **Filtering Logic**: Automatically excludes stablecoins (USDC, FDUSD, etc.) and leveraged tokens (UP/DOWN) to ensure a high-quality data sample.
*   **Data Retrieval**: Downloads high-frequency (30m) historical k-lines for the selected universe.

### 2. PCA Decomposition
Using `sklearn.decomposition.PCA`, the model breaks down the returns matrix:
*   **PC1 (Market Factor)**: Represents the collective movement of the entire crypto market.
*   **PC2 (Anomaly Factor)**: Captures deviations. Assets with high "loadings" on PC2 are those behaving differently from the rest of the market.
*   **Scree Plot**: Visualizes the explained variance ratio of each component.

### 3. Econometric Spread Analysis
For assets identified as "anomalies," the system performs a deep dive:
*   **Log-Price Modeling**: Linearizes price relationships.
*   **Beta Calculation**: Determines the asset's sensitivity to Bitcoin using `np.polyfit`.
*   **Augmented Dickey-Fuller (ADF) Test**: Statistically verifies if the spread (residuals) is stationary. A p-value < 0.05 confirms the asset is a candidate for a Mean Reversion strategy.

### 4. Tactical Execution Metrics
*   **Rolling Z-Score**: Normalizes the spread deviation to identify statistically significant entry and exit points (Overbought/Oversold).
*   **Risk Metrics**: Provides descriptive statistics (`mean`, `std`, `max drawdowns`) for position sizing and risk management.

## 📊 Key Visualizations
*   **Heatmap**: Cross-correlation matrix of the top 30 assets.
*   **PC2 Loadings Chart**: Highlights specific coins that are currently "decoupled" from the market.
*   **3-Panel Spread Report**: 
    1. Log-Price Model vs. Fair Value.
    2. Global Spread (Cointegration Strategy).
    3. Tactical Z-Score (Timing).

## 🚀 Installation & Usage

1.  **Dependencies**:
    ```bash
    pip install pandas numpy scikit-learn statsmodels seaborn matplotlib python-binance
    ```
2.  **Execution**:
    Open the Jupyter Notebook and run the cells. The script is configured to run without API keys for public data access.

## Why this matters for Finance
In an institutional context (Banking/Audit), this approach demonstrates:
*   **Systemic Risk Management**: Understanding how assets correlate during market stress.
*   **Evidence-Based Trading**: Using p-values and Z-scores rather than subjective technical analysis.
*   **Data Engineering**: Managing large matrices of time-series data efficiently.

---
**Disclaimer**: *This project is for educational and research purposes. Quantitative models involve significant risk, and statistical significance in the past does not guarantee future results.*

---
