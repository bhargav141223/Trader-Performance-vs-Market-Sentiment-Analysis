# Trader Performance vs Market Sentiment Analysis - Project Write-up

## Methodology

### Data Preparation
- **Datasets**: Bitcoin Fear/Greed Index (2,644 daily records, 2018-2020) and Hyperliquid trader historical data (23,285 trades, 7 accounts)
- **Alignment**: Converted timestamps to IST timezone, merged datasets on date at daily level (23,279 aligned records)
- **Quality Check**: Historical data had 5 missing values, no duplicates; Sentiment data was complete with no duplicates

### Key Metrics Created
- Daily PnL per trader: Sum of Closed PnL grouped by date and account
- Win Rate: Percentage of profitable trades per account
- Average Trade Size: Mean Size USD per account (leverage proxy)
- Trade Frequency: Number of trades per day
- Long/Short Ratio: BUY vs SELL trade count ratio

### Analysis Approach
1. **Performance Analysis**: Grouped by sentiment classification to compare PnL, win rate, and volatility
2. **Behavioral Analysis**: Examined trade count, position size, and L/S bias across sentiment regimes
3. **Segmentation**: Created 3 trader segments using median splits:
   - Frequent vs Infrequent (based on trade count)
   - High vs Low Leverage (based on average position size)
   - Consistent Winners vs Inconsistent (based on total PnL > 0 and win rate > 45%)

## Key Findings

### 1. Performance by Market Sentiment
**Extreme Fear** shows the highest average PnL ($259) but with the highest volatility (3,748) and lowest win rate (32.9%). This suggests high-risk, high-reward trading during market panic.

**Extreme Greed** demonstrates the best efficiency: highest win rate (48.4%) with the lowest volatility (766), despite moderate average PnL ($59). This indicates more stable, consistent performance during market euphoria.

**Fear and Greed** regimes show intermediate performance, with Fear having higher PnL ($166) but lower win rate (40.2%) compared to Greed ($104 PnL, 40.8% win rate).

### 2. Behavioral Changes Based on Sentiment
**Position Size Paradox**: Traders take their largest average positions during Fear regimes ($28,164), exactly when win rates are lowest. This counter-intuitive behavior suggests emotional trading during market stress.

**L/S Bias Shift**: During Extreme Fear, traders show a strong long bias (L/S ratio: 1.44), potentially trying to "catch the bottom." During Extreme Greed, the bias flips to short (L/S ratio: 0.90), suggesting profit-taking or contrarian positioning.

**Trade Frequency**: Extreme Greed sees the highest trading activity (6,924 trades), while Extreme Fear has the lowest (1,246 trades), indicating traders are more active during confident market phases.

### 3. Trader Segment Insights
**Frequent Traders** (4 accounts) achieve significantly higher win rates (48.4%) compared to Infrequent traders (38.1%), suggesting experience and market engagement correlate with success.

**High Leverage Traders** (4 accounts) take positions averaging $12,558+ vs Low Leverage at $2,688, but this doesn't necessarily correlate with better performance.

**Consistent Winners** (2 accounts) are rare - only 2 out of 7 accounts meet the criteria of positive total PnL with >45% win rate, indicating consistent profitability is challenging.

## Strategy Recommendations

### Strategy 1: Fear-Size Alignment Rule
**Target Segment**: High Leverage (High Exposure) & Inconsistent Traders

**Rule**: During Extreme Fear days, reduce average position size by 50% and tighten stop-losses.

**Rationale**: Our analysis reveals a "Size Paradox" - traders currently take their largest positions ($28,164) during Fear regimes, exactly when win rates are at their lowest (32.9%) and PnL volatility peaks (3,748). By reducing size during high-volatility/low-probability windows, traders can avoid massive drawdowns that characterize inconsistent performance.

**Expected Impact**: Reduced drawdown risk during market stress while maintaining exposure to potential mean-reversion opportunities.

### Strategy 2: Greed Efficiency Scaling Rule
**Target Segment**: Consistent Winners & Frequent Traders

**Rule**: During Extreme Greed days, increase trade frequency to capture high-probability moves but maintain a short-bias (selling/profit-taking stance).

**Rationale**: Extreme Greed is the most "efficient" market phase, offering the highest win rate (48.4%) and lowest PnL volatility (766). The overall market L/S ratio drops to 0.90 during this phase, suggesting successful traders transition to contrarian or profit-taking positioning. Increased frequency during high-efficiency periods maximizes capture of favorable conditions.

**Expected Impact**: Improved risk-adjusted returns by capitalizing on the most predictable market regime with appropriate positioning.

## Additional Insights

### Market Regime Characteristics
- **Neutral periods** (5,854 trades) show balanced behavior (L/S ratio: 1.00) with moderate performance (46.3% win rate, $106 avg PnL)
- **Sentiment transitions** present the highest opportunity for strategic positioning
- **Volatility clustering** is evident, with Fear periods showing 5x higher PnL volatility than Greed periods

### Trader Archetypes (Bonus Analysis)
KMeans clustering identified 3 distinct trader profiles:
1. **High-Performers** (Cluster 2): $1.56M total PnL, moderate size ($10,974), high frequency (5,622 trades)
2. **Low-Risk** (Cluster 1): $222K total PnL, small size ($3,785), low frequency (1,104 trades)
3. **Balanced** (Cluster 0): $509K total PnL, large size ($18,032), very high frequency (9,904 trades)

### Predictive Capability
A simple Random Forest model using position size, trade count, sentiment value, and current PnL can predict next-day profitability with 63% accuracy, suggesting behavioral and sentiment features have predictive power for short-term performance.

## Conclusion
This analysis demonstrates that market sentiment significantly impacts both trader behavior and performance. The most actionable insight is that traders often behave counter-productively during extreme sentiment regimes - increasing risk when they should be reducing it. The proposed strategies address this by aligning position sizing and directional bias with sentiment-based efficiency metrics, potentially improving risk-adjusted returns across different trader segments.
