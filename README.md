# Trader Performance vs Market Sentiment Analysis

## Overview
This project analyzes how market sentiment (Fear/Greed Index) relates to trader behavior and performance on Hyperliquid. The goal is to uncover patterns that could inform smarter trading strategies.

## Project Structure
```
dat_science/
├── data/
│   ├── fear_greed_index.csv      # Bitcoin market sentiment data
│   └── historical_data.csv       # Hyperliquid trader historical data
├── code/
│   └── intern_code .ipynb        # Main analysis notebook
├── outputs/
│   ├── avg_daily_pnl.png         # Average daily PnL trend
│   ├── behavior_ls_bias.png      # Long/Short bias by sentiment
│   ├── daily_trades_bar.png      # Daily trading volume
│   ├── leverage_dist_proxy.png   # Leverage distribution
│   ├── ls_pie.png                # Long/Short ratio pie chart
│   ├── performance_sentiment.png # Performance by sentiment
│   ├── winner_exposure_box.png   # Trade size by winner segment
│   └── winrate_vs_size.png       # Win rate vs trade size
└── docs/
    └── Data Science Intern project .pdf  # Original assignment
```

## Setup

### Prerequisites
- Python 3.8+
- Jupyter Notebook

### Required Packages
```bash
pip install pandas matplotlib seaborn numpy scikit-learn
```

### How to Run
1. Open the notebook:
```bash
jupyter notebook code/intern_code\ .ipynb
```

2. Run cells sequentially from Part A through Bonus Part

## Data Files
- **fear_greed_index.csv**: Daily Bitcoin Fear/Greed Index (2018-2020)
  - Columns: timestamp, value, classification, date
  
- **historical_data.csv**: Hyperliquid trader data
  - 23,285 rows, 16 columns
  - Key fields: Account, Trade ID, Side, Size USD, Closed PnL, Timestamp IST

## Analysis Summary

### Part A: Data Preparation
- Loaded and documented both datasets
- Aligned timestamps to daily level
- Created key metrics: daily PnL, win rate, leverage distribution, trade counts, L/S ratio

### Part B: Analysis
- **Performance by Sentiment**: Extreme Fear shows highest PnL but highest volatility; Extreme Greed shows best win rate with lowest volatility
- **Behavioral Changes**: Traders increase position sizes during Fear (counter-intuitive), decrease during Greed
- **Trader Segments**: Identified 3 segments - Frequent/Infrequent, High/Low Leverage, Consistent Winners/Inconsistent

### Part C: Strategy Recommendations
1. **Fear-Size Alignment Rule**: Reduce position size by 50% during Extreme Fear for high-leverage traders
2. **Greed Efficiency Scaling Rule**: Increase trade frequency during Extreme Greed with short-bias for consistent winners

### Bonus
- **Clustering**: KMeans clustering identified 3 trader archetypes (High-performers, Low-risk, High-volume)
- **Predictive Model**: Random Forest classifier predicts next-day profitability with 63% accuracy

## Outputs
All charts are saved in the `outputs/` directory as PNG files for easy viewing and inclusion in reports.

## Contact
Project completed for Primetrade.ai Data Science Intern application
