
---

## ⚙️ Model Calibration & Sensitivity

By default, the model is configured with **conservative parameters** to identify only the most mathematically robust opportunities (high statistical significance). However, the sensitivity can be adjusted to expand the analysis.

### 1. Optimal Universe Size (Top 20-40)
The choice of `TOP_N` is crucial for the PCA covariance matrix stability:
*   **The "Sweet Spot" (20-40 coins)**: This range captures enough market breadth to identify real decoupling while maintaining high data quality and liquidity.
*   **Too Few (< 20)**: The sample becomes dominated by "Bitcoin Proxies." PC1 will explain almost 90% of the variance, leaving no room for anomaly detection.
*   **Too Many (> 50)**: Introducing low-liquidity "Alt-coins" can dilute the data with idiosyncratic noise, making the principal components less reliable.

### 2. Tuning the Sensitivity
If you want to generate more charts and identify more potential trades, you can adjust the following hyperparameters:

| Parameter | Conservative (Default) | Aggressive (Discovery) | Impact |
| :--- | :--- | :--- | :--- |
| `ANOMALY_THRESHOLD` | **0.4** | **0.25** | Lowering this will identify coins with even minor decoupling from PC1. |
| `ADF_P_VALUE_CUTOFF`| **0.05** | **0.10** | Increasing this accepts spreads with 90% confidence instead of 95% (more signals, higher risk of false stationarity). |
| `Z_ENTRY_LEVEL` | **2.0** | **1.5** | Narrowing the Z-score bands will trigger entry signals much more frequently. |

### 3. Understanding the "No Signal" Scenario
If the model is run with default parameters and returns no charts, it indicates that **the market is currently highly efficient**. In this state, almost all top-tier assets are moving in perfect lockstep with the Market Factor (PC1), and no statistically significant mean-reversion opportunities exist.

---

## 📈 Recent Market Insights (Oct 2025 – Jan 2026)

Based on continuous monitoring and forward-testing during the Q4 2025 – Q1 2026 period, several key refinements were identified to optimize the model's performance in high-volatility environments:

### 1. The $3\sigma$ (Three-Sigma) Approach
While the standard $2\sigma$ (95% confidence) threshold is common, recent market data suggests that **$3\sigma$ boundaries** (representing 99.7% of all moves) provide a significantly better signal-to-noise ratio.
*   **Insight**: In the current market regime, $2\sigma$ deviations often represent "just increased volatility" volatility, whereas $3\sigma$ levels highlight true **structural mispricings** and "fat-tail" events that are more likely to mean-revert.

### 2. From Speculation to Positional Spot Trading
The model has proven most effective when treated as a **Non-Speculative Positional Tool**:
*   **Strategy**: Instead of aggressive leverage, the optimal approach involves entering **Spot positions** at extreme global spread deviations.
*   **Logic**: This reduces liquidation risk during "black swan" events and allows the trader to hold the position until the cointegration relationship restores.

### 3. Global Spread vs. Tactical Z-Score
Recent analysis indicates that the **Global Spread Deviation** (the absolute residual from the static model) is often a more reliable anchor than the short-term Rolling Z-Score.
*   **Rationale**: The Z-score is sensitive to the chosen window (e.g., 100 bars). In contrast, the Global Spread captures the **long-term price-to-fair-value gap**, making it ideal for patient, positional entries at extreme market dislocations.

---

