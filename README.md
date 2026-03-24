# 🇨🇳 China AI Growth Dataset (2010–2026)
### A Comprehensive End-to-End Data Analysis, Visualization & Predictive Modeling Project
 
<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/License-CC0%201.0-lightgrey?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Data-2010--2026-orange?style=for-the-badge"/>
</p>
 
---
 
## 📌 Project Overview
 
This project delivers a **full end-to-end data science pipeline** on China's AI/technology growth data from **2010 to 2026**, covering:
 
- 📥 Data Loading & Inspection
- 🧹 Data Cleaning & Imputation
- 🔍 Exploratory Data Analysis (EDA)
- 📊 Multi-panel Data Visualization (7 charts)
- ⚙️ Feature Engineering & Linear Regression
- 🔮 3-Year Publication Forecasting (2027–2029)
 
The dataset contains **17 yearly observations** across **12 key indicators** including research output, government/private investment, company counts, patent share, and R&D expenditure.
 
---
 
## 📁 Repository Structure
 
```
china-ai-growth-analysis/
│
├── 📄 README.md                          ← You are here
├── 📊 china_ai_growth_dataset_2010_2026.csv   ← Raw dataset
├── 🐍 china_ai_analysis.py               ← Main analysis script
├── 📈 china_ai_enriched.csv              ← Enriched output (with new features)
│
└── 📂 outputs/
    ├── fig1_investment_trend.png          ← Total / Govt / Private investment
    ├── fig2_dual_axis_share.png           ← Publication vs Patent share
    ├── fig3_scatter_regression.png        ← R&D expenditure vs Growth Rate
    ├── fig4_stacked_bar.png               ← Startups vs Established companies
    ├── fig5_investment_efficiency.png     ← Publications per Billion USD
    ├── fig6_actual_vs_predicted.png       ← Regression model output
    └── fig7_publications_forecast.png     ← 2027–2029 forecast
```
 
---
 
## 📋 Dataset Description
 
| Column | Description |
|--------|-------------|
| `Year` | Time period (2010–2026) |
| `Country` | China |
| `AI_Publication_Share (%)` | % share of global research publications |
| `AI_Total_Publications` | Total research publications per year |
| `AI_Investment_Billion_USD` | Total annual tech investment (Billion USD) |
| `Government_AI_Spending_Billion_USD` | Government R&D expenditure |
| `Private_AI_Investment_Billion_USD` | Private sector investment |
| `AI_Companies_Count` | Total technology companies |
| `AI_Startups_Count` | Startup companies count |
| `AI_Patents_Share (%)` | % share of global patents |
| `R&D_Expenditure (% of GDP)` | National R&D as % of GDP |
| `AI_Growth_Rate (%)` | Annual growth rate — **target variable** |
 
> **Source:** [Kaggle — China Tech Development Data (2010–2026)](https://www.kaggle.com/) | License: CC0 Public Domain
 
---
 
## 🛠️ Installation & Setup
 
### Prerequisites
 
- Python 3.8 or higher
- pip
 
### Clone the Repository
 
```bash
git clone https://github.com/YOUR_USERNAME/china-ai-growth-analysis.git
cd china-ai-growth-analysis
```
 
### Install Dependencies
 
```bash
pip install pandas numpy matplotlib scipy scikit-learn
```
 
### Run the Analysis
 
```bash
python china_ai_analysis.py
```
 
All charts and the enriched CSV will be saved to the `outputs/` folder automatically.
 
---
 
## 📊 Analysis Walkthrough
 
### Step 1 — Data Loading & Inspection
 
```python
import pandas as pd
df = pd.read_csv("china_ai_growth_dataset_2010_2026.csv")
print(df.head())
print(df.describe())
```
 
- Shape: **17 rows × 12 columns**
- 1 missing value found in `AI_Growth_Rate (%)` for year 2010
 
---
 
### Step 2 — Data Cleaning
 
```python
# Impute missing AI_Growth_Rate (%) with column mean
mean_growth = df["AI_Growth_Rate (%)"].mean()  # → 12.69%
df["AI_Growth_Rate (%)"].fillna(mean_growth, inplace=True)
```
 
✅ Zero duplicates | ✅ Consistent dtypes | ✅ 1 NaN imputed with mean
 
---
 
### Step 3 — EDA: Correlation & YoY Growth
 
**Top Correlations:**
 
| Variable Pair | Pearson r |
|---|---|
| `AI_Total_Publications` ↔ `R&D_Expenditure (% of GDP)` | **0.985** |
| `AI_Patents_Share (%)` ↔ `AI_Investment_Billion_USD` | **0.950** |
| `AI_Total_Publications` ↔ `AI_Startups_Count` | **0.997** |
| `AI_Growth_Rate (%)` ↔ `R&D_Expenditure (% of GDP)` | **−0.505** |
 
**Year-over-Year Growth (Publications):** ranged from **6.9%** (2026) to **20%** (2015–2017).
 
---
 
### Step 4 — Visualizations
 
| Chart | Description |
|---|---|
| `fig1` | 📈 Investment Trend — Total, Government & Private (2010–2026) |
| `fig2` | 🔬 Dual-axis: Publication Share % vs Patent Share % |
| `fig3` | 💹 Scatter + Regression: R&D Expenditure vs AI Growth Rate |
| `fig4` | 🏢 Stacked Bar: Startups vs Established Companies (with ratio labels) |
| `fig5` | ⚡ Investment Efficiency: Publications per Billion USD |
| `fig6` | 🤖 Actual vs Predicted AI Growth Rate |
| `fig7` | 🔮 Publications Forecast: 2027–2029 |
 
---
 
### Step 5 — Feature Engineering & Regression
 
**Investment Efficiency** = `AI_Total_Publications / AI_Investment_Billion_USD`
 
> Jumped from ~6,600 pub/$B (2010–2019) → **14,516 pub/$B** in 2024, showing dramatic research scaling.
 
**Multiple Linear Regression** predicting `AI_Growth_Rate (%)`:
 
```
Features: AI_Investment_Billion_USD + R&D_Expenditure (% of GDP)
 
Intercept  :  64.07
Coefficient (AI_Investment_Billion_USD)  :  +1.72
Coefficient (R&D_Expenditure % of GDP)  : −29.24
 
R² Score   :  0.39
RMSE       :  6.37%
```
 
> Note: The moderate R² (0.39) reflects that macro shocks (COVID-2020, tech crackdowns-2024) significantly influence growth rates beyond these two features.
 
---
 
### Step 6 — Forecasting (2027–2029)
 
Using the **Compound Annual Growth Rate (CAGR)** over the stable post-rebound period (2021–2026):
 
```
CAGR = 8.09%
```
 
| Year | Projected Publications |
|------|----------------------|
| 2027 | **167,572** |
| 2028 | **181,121** |
| 2029 | **195,782** |
 
---
 
## 🔑 Key Findings
 
- 🚀 China's AI publications grew **675%** from 2010 (20,000) to 2026 (155,000)
- 💰 Total investment peaked at **$14B in 2023**, then contracted sharply in 2024 (–33%)
- 📉 Two negative growth years recorded: **2020 (–5%, COVID)** and **2024 (–8%, investment contraction)**
- 🏭 Startups consistently represent **37–69%** of total AI companies, showing a vibrant innovation ecosystem
- 📐 R&D Expenditure as % of GDP grew from **1.71% (2010)** to **2.75% (2026)**
- 🌏 Patent share climbed from **20% to 72%** globally — a 3.6× increase in 16 years
 
---
 
## 🧰 Tech Stack
 
| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, EDA |
| `numpy` | Numerical computation |
| `matplotlib` | All visualizations |
| `scipy.stats` | Linear regression (scatter plot) |
| `scikit-learn` | Multiple linear regression, metrics |
 
---
 
## 🤝 Contributing
 
Contributions are welcome! Feel free to:
 
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request
 
---
 
## 📜 License
 
This project is licensed under **CC0 1.0 Universal (Public Domain)**. The dataset is sourced from Kaggle under the same license. You are free to use, modify, and distribute this work without restriction.
 
---
 
## 👤 Author
 
> Notebook- Shravan Padhar

> Notebook link-[Kaggle — Notebook ](https://www.kaggle.com/shravanpadhar/gdp-forecasting-linear-regression-r)

> Dataset: China AI Growth Dataset (2010–2026) — Kaggle
 
---
 
<p align="center">
  ⭐ If you found this project helpful, please consider giving it a star!
</p>
