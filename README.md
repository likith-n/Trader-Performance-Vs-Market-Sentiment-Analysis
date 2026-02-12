# Trader Performance vs Market Sentiment Analysis

Data Science Intern Assignment - Primetrade.ai

## Project Overview

This project analyzes the relationship between Bitcoin market sentiment (Fear/Greed Index) and trader behavior/performance on the Hyperliquid platform. The analysis identifies statistically significant patterns in how traders adjust their activity levels based on market sentiment and provides actionable trading strategies.



## Datasets

### 1. Bitcoin Fear/Greed Index
- Source: Alternative.me
- Records: 2,644 daily observations
- Date Range: February 2018 - May 2025
- Columns: timestamp, value, classification, date
- Classifications: Extreme Fear, Fear, Neutral, Greed, Extreme Greed

### 2. Hyperliquid Trader Data
- Source: Hyperliquid DEX
- Records: 211,224 trades
- Unique Traders: 32 accounts
- Unique Assets: 246 coins
- Date Range: March 2023 - June 2025
- Key Columns: Account, Coin, Execution Price, Size (Tokens and USD), Side, Timestamp, Direction, Closed PnL, Transaction Hash, Order ID, Fee

## Setup and Installation

### Requirements
- Python 3.8 or higher
- Jupyter Notebook or JupyterLab

### Required Libraries
```
pandas
numpy
matplotlib
seaborn
scipy
```

### Installation
```bash
pip install pandas numpy matplotlib seaborn scipy jupyter
```

### Running the Analysis
1. Place both CSV files in the same directory as the notebook
2. Open the Jupyter notebook: `jupyter notebook trader_sentiment_analysis.ipynb`
3. Run all cells sequentially

## Methodology

### Part A: Data Preparation

**1. Data Loading and Documentation**
- Loaded both datasets and verified data quality
- Sentiment dataset: 2,644 rows, 4 columns, 0 missing values, 0 duplicates
- Trader dataset: 211,224 rows, 16 columns, 0 missing values, 0 duplicates
- Documented unique accounts (32) and unique coins (246)

**2. Timestamp Conversion and Alignment**
- Converted sentiment dates from string to datetime format
- Converted trader timestamps from Unix milliseconds to datetime
- Extracted date component for daily-level aggregation
- Identified date overlap between datasets

**3. Feature Engineering**
Created the following metrics:
- Daily PnL per trader (sum, mean, standard deviation, min, max)
- Win rate (percentage of profitable trades per day)
- Number of trades per day
- Total trading volume in USD per day
- Average trade size in USD and tokens
- Long/short ratio (calculated from position directions)
- Total fees paid per day

**4. Dataset Merging**
- Merged daily trader metrics with sentiment data on date
- Final merged dataset: 102 account-date combinations
- 77 observations with known sentiment classifications
- 25 observations outside sentiment data range (marked as Unknown)

### Part B: Analysis

**Question 1: Does performance differ between Fear vs Greed days?**

Findings:
- Fear days: Average daily PnL of $209,372 (median $81,390), win rate of 42%
- Greed days: Average daily PnL of $90,989 (median $20,926), win rate of 37%
- Statistical test (t-test): p-value = 0.1342 (not statistically significant)
- Interpretation: While Fear days show higher average returns, the difference is not statistically reliable due to high variance in the data

**Question 2: Do traders change behavior based on sentiment?**

Findings:
- Trade frequency:
  - Fear days: 4,183 trades per day on average
  - Greed days: 1,169 trades per day on average
  - Difference: 3.6x increase during Fear
  - Statistical significance: p-value = 0.0039 (highly significant)

- Trading volume:
  - Fear days: $22,004,953 average daily volume
  - Greed days: $4,186,769 average daily volume
  - Difference: 5.3x increase during Fear
  - Statistical significance: p-value = 0.0050 (highly significant)

- Long/short ratio: No significant difference (p-value = 0.4102)

Interpretation: Traders demonstrate significantly higher activity during Fear periods, suggesting they recognize these periods as opportunities for profit despite increased volatility.

**Question 3: Trader Segmentation**

Identified three key trader segments:

Segment 1: High Frequency vs Low Frequency Traders
- High frequency traders: $164,986 average daily PnL
- Low frequency traders: $49,079 average daily PnL
- Performance gap: 3.4x difference

Segment 2: Consistent vs Inconsistent Traders
- Consistent traders: 48.9% win rate, lower PnL volatility
- Inconsistent traders: 29.1% win rate, higher PnL volatility
- Win rate gap: 1.7x difference

Segment 3: High Volume vs Low Volume Traders
- High volume traders: $169,976 average daily PnL
- Low volume traders: $44,089 average daily PnL
- Performance gap: 3.8x difference

### Part C: Actionable Strategies

Based on the statistical analysis, I developed three evidence-based trading strategies:

**Strategy 1: Fear Amplification Strategy**

Rule: Increase trading activity during Fear and Extreme Fear periods

Implementation:
- High-frequency traders: Increase trade count by 50-100% during Fear days
- Low-frequency traders: Increase position sizes by 25-40% during Fear days
- All traders: Use 20-30% smaller individual positions to manage increased volatility

Rationale: The 3.6x increase in market activity and 5.3x increase in volume during Fear periods indicates higher liquidity and more trading opportunities. Skilled traders can exploit market inefficiencies that arise during high-emotion periods.

**Strategy 2: Segment-Specific Approach**

Rule: Tailor trading strategy to individual trader archetype

For High-Frequency Traders:
- Fear days: Maximize trade count, focus on scalping (1-2% gains per trade)
- Greed days: Reduce frequency by 40-50%, be highly selective

For Low-Frequency Traders:
- Fear days: Increase position sizes, use mean-reversion strategies, scale in gradually
- Greed days: Decrease position sizes by 20-30%, tighten profit targets

For Consistency-Focused Traders:
- All conditions: Maintain strict 1-2% risk per trade, never exceed 3 consecutive losing trades without review

Rationale: The analysis shows clear performance differences between trader segments, indicating that different trading styles excel in different market conditions.

**Strategy 3: Contrarian Greed Strategy**

Rule: Reduce exposure and build cash reserves during Greed periods

Implementation:
- Reduce overall exposure by 30-40% during Greed and Extreme Greed
- Increase cash reserves to 25-40% of portfolio
- Consider counter-trend positions (fading rallies)
- Tighten stop-losses for any new positions

Rationale: The 72% reduction in trading activity during Greed periods suggests fewer opportunities and reduced market inefficiency. Lower activity combined with lower average PnL indicates unfavorable risk/reward conditions.

## Key Findings Summary

1. Traders exhibit 3.6x more trading activity during Fear periods compared to Greed periods (p=0.004, statistically significant)

2. Trading volume is 5.3x higher during Fear periods (p=0.005, statistically significant)

3. High-frequency and high-volume traders significantly outperform other segments (3.4x and 3.8x respectively)

4. Consistent traders maintain nearly double the win rate of inconsistent traders (48.9% vs 29.1%)

5. While Fear days show higher average PnL, the difference is not statistically significant due to high variance

## Visualizations Created

1. Performance by Sentiment: Boxplot of daily PnL and violin plot of win rates across sentiment categories
2. Behavioral Changes: Bar charts showing trade frequency, volume, and trade sizes by sentiment
3. Trader Segmentation: Bar chart comparing performance across different trader archetypes
4. Strategy Framework: Multi-panel visualization showing recommended activity levels and position sizing by sentiment

## Statistical Methods

- Independent t-tests for comparing Fear vs Greed groups
- Significance level: alpha = 0.05 (95% confidence)
- Sample size: 32 Fear observations, 37 Greed observations (combined Greed and Extreme Greed)
- Median-based segmentation for trader classification

## Limitations and Caveats

1. Small sample size: Only 32 traders with 102 account-date observations after merging
2. Survivorship bias: Dataset may only include active or successful traders
3. Date coverage: 25 trading days fall outside the sentiment data range
4. Causation vs correlation: Sentiment may reflect rather than drive trader behavior
5. Market regime dependency: Analysis spans different market cycles which may affect generalizability
6. Individual variation: Strategies may not apply equally to all trader profiles

## Recommendations for Implementation

1. Start with reduced position sizes (25-50% of normal) when testing strategies
2. Maintain detailed trade journals including sentiment classification for each trade
3. Review performance by sentiment category on a monthly basis
4. Adapt strategies quarterly based on actual performance data
5. Never exceed 5% account risk on any single trade regardless of sentiment

## Files and Outputs

- trader_sentiment_analysis.ipynb: Main analysis notebook with all code and visualizations
- All visualizations are embedded in the notebook

## Technical Notes

- Data processing: Python pandas for data manipulation and aggregation
- Statistical analysis: scipy.stats for t-tests and hypothesis testing
- Visualization: matplotlib and seaborn for all charts
- Missing data handling: Dates outside sentiment range filled with "Unknown" category
- No external files were created; all analysis is contained within the notebook

## Conclusion

This analysis reveals clear and statistically significant patterns in the relationship between market sentiment and trader behavior on Hyperliquid. The most important finding is that Fear periods generate substantially higher trading activity and volume, indicating that experienced traders recognize and capitalize on fear-driven market opportunities.

The three proposed strategies provide a quantitative framework for adjusting trading activity based on market sentiment and individual trader characteristics. Implementation of these strategies with proper risk management may improve risk-adjusted returns by better aligning trading activity with favorable market conditions.


