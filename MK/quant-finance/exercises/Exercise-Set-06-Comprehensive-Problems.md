# Exercise Set 06: Comprehensive Problems

Complex multi-step problems integrating all concepts. These simulate real-world analysis.

---

## Problem 1: Complete Stock Analysis

You're analyzing Stock XYZ. Here is 30 days of price data:

| Day | Close | Day | Close | Day | Close |
|-----|-------|-----|-------|-----|-------|
| 1   | 100.00| 11  | 103.50| 21  | 106.80|
| 2   | 101.20| 12  | 102.80| 22  | 105.20|
| 3   | 100.50| 13  | 104.20| 23  | 107.50|
| 4   | 102.30| 14  | 103.60| 24  | 106.30|
| 5   | 101.80| 15  | 105.10| 25  | 108.90|
| 6   | 100.20| 16  | 104.40| 26  | 107.50|
| 7   | 101.50| 17  | 106.20| 27  | 109.20|
| 8   | 102.80| 18  | 105.50| 28  | 108.00|
| 9   | 101.90| 19  | 107.30| 29  | 110.50|
| 10  | 103.10| 20  | 106.10| 30  | 109.80|

**Day 31 close: $102.50**

### Tasks:
a) Calculate all 30 daily log returns
b) Calculate mean and standard deviation
c) Annualize the volatility
d) Calculate the sigma move for Day 31
e) Classify the Day 31 move
f) Calculate the probability of this move under normal distribution
g) Discuss whether this event suggests fat tails

---

## Problem 2: Rolling Sigma Analysis

Using the same 30-day data from Problem 1:

### Tasks:
a) Calculate 10-day rolling mean and σ for days 10, 20, and 30
b) If Day 31's return occurred, what would be the sigma classification using:
   - 10-day σ (from days 21-30)
   - 20-day σ (from days 11-30)
   - 30-day σ (all data)
c) Why do the classifications differ?
d) Which lookback is most appropriate for risk management? Why?

---

## Problem 3: EWMA Volatility Tracking

Starting with the data from Problem 1:

### Tasks:
a) Initialize EWMA variance using the variance of first 10 days' returns
b) Track EWMA σ (λ = 0.94) from Day 11 through Day 31
c) Plot mentally or in a table: How does EWMA σ evolve?
d) After Day 31's large move, what is the new EWMA σ?
e) Calculate half-life: How long until this shock decays by 50%?

---

## Problem 4: Multi-Asset Portfolio Analysis

You manage a portfolio with these holdings and today's returns:

| Stock | Position ($) | Today's Return | 60-Day μ | 60-Day σ |
|-------|--------------|----------------|----------|----------|
| AAPL  | 50,000       | -2.8%          | 0.05%    | 1.5%     |
| MSFT  | 40,000       | -2.2%          | 0.06%    | 1.3%     |
| AMZN  | 30,000       | -3.5%          | 0.04%    | 2.0%     |
| GOOGL | 25,000       | -1.8%          | 0.05%    | 1.6%     |
| META  | 20,000       | -4.0%          | 0.03%    | 2.2%     |
| Cash  | 35,000       | 0%             | -        | -        |

### Tasks:
a) Calculate sigma move for each stock
b) Rank stocks by sigma magnitude
c) Calculate portfolio return (weighted by position)
d) Estimate portfolio σ (assume 0.6 correlation between stocks)
   Hint: For equal correlation: σ_p = σ_avg × √(1/n + (1-1/n)×ρ)
e) Calculate portfolio sigma move
f) Which stocks drive the portfolio's poor day?

---

## Problem 5: Historical Event Analysis

On **March 16, 2020**, major indices experienced historic drops:

| Index | Daily Return | Pre-Crash 30-Day σ |
|-------|--------------|-------------------|
| S&P 500 | -11.98% | 1.0% |
| Dow Jones | -12.93% | 1.1% |
| NASDAQ | -12.32% | 1.2% |
| Russell 2000 | -14.30% | 1.4% |

### Tasks:
a) Calculate sigma moves for each index (assume μ ≈ 0)
b) Calculate probability of each event under normal distribution
c) Calculate probability of ALL FOUR happening on same day (assume independence)
d) Why is the independence assumption problematic?
e) If these events happen once per century under normal distribution, and they actually happened, what does this tell you?
f) What would be a more realistic volatility estimate going forward?

---

## Problem 6: Regime Detection

A stock shows this pattern of 60-day rolling volatility:

| Period | Days | Rolling σ | Interpretation |
|--------|------|-----------|----------------|
| 1      | 1-60 | 1.2%      | Normal         |
| 2      | 20-80| 1.3%      | Normal         |
| 3      | 40-100| 1.8%     | ?              |
| 4      | 60-120| 2.5%     | ?              |
| 5      | 80-140| 2.8%     | ?              |
| 6      | 100-160| 2.2%    | ?              |
| 7      | 120-180| 1.5%    | ?              |

### Tasks:
a) Identify the volatility regime changes
b) When did volatility expansion begin?
c) When did it peak?
d) How long was the high-vol period?
e) If you calculated sigma moves using Period 1's σ throughout, how would classifications be affected during Period 5?
f) Recommend a volatility estimation approach for real-time trading

---

## Problem 7: Fat Tails Investigation

You have 1000 days of return data for a stock. Summary statistics:

- Mean: 0.04%
- Standard Deviation: 1.8%
- Skewness: -0.45
- Excess Kurtosis: 4.2

Observed extreme events:
- Days with |return| > 2σ (3.6%): 58 days
- Days with |return| > 3σ (5.4%): 12 days
- Days with |return| > 4σ (7.2%): 4 days
- Days with |return| > 5σ (9.0%): 2 days

### Tasks:
a) Calculate expected number of events under normal distribution for each sigma level
b) Calculate the ratio of observed to expected
c) What does the negative skewness indicate?
d) What does the positive excess kurtosis indicate?
e) If you use normal-distribution sigma classifications, are you underestimating or overestimating tail risk?
f) Propose an adjustment factor for "real" sigma interpretation

---

## Problem 8: Intraday Sigma Spikes

You track a stock intraday with 5-minute bars. Normal 5-minute σ = 0.15%

At 10:30 AM, news breaks and these 5-minute returns occur:

| Time | 5-Min Return |
|------|--------------|
| 10:30 | -2.5% |
| 10:35 | -1.8% |
| 10:40 | +0.8% |
| 10:45 | -0.5% |
| 10:50 | +0.3% |

### Tasks:
a) Calculate sigma move for each bar
b) How would you describe the event evolution?
c) Calculate total move over 25 minutes
d) If 25-minute normal σ ≈ 0.34% (√5 × 0.15%), classify the 25-min move
e) Compare individual bar classification vs aggregated classification
f) What implications does this have for stop-loss placement?

---

## Problem 9: Volatility Surface Analysis

A stock has different volatility characteristics by time period:

| Period | σ Estimate |
|--------|------------|
| 5-day | 2.2% |
| 10-day | 1.9% |
| 20-day | 1.5% |
| 60-day | 1.3% |
| 252-day | 1.1% |

Today's return: -3.5%

### Tasks:
a) Calculate sigma move for each time horizon
b) Create a "sigma surface" showing how classification changes
c) Which horizon gives the most conservative (highest) sigma estimate?
d) Which gives the most aggressive (lowest)?
e) For a trader with 2-week holding period, which σ is most relevant?
f) For a risk manager, which σ should be used?

---

## Problem 10: Complete Trading Day Analysis

**Date: Fictional Crisis Day**

Market opens limit down. You need to analyze your portfolio.

**Pre-open data (using prior 60-day stats):**

| Position | Size ($K) | Prev Close | 60-Day σ |
|----------|-----------|------------|----------|
| SPY | 200 | 450.00 | 1.0% |
| QQQ | 150 | 380.00 | 1.3% |
| IWM | 100 | 200.00 | 1.5% |
| TLT | 50 | 95.00 | 0.6% |

**9:30 AM prices:**
- SPY: 427.50
- QQQ: 354.92
- IWM: 184.00
- TLT: 98.80

### Tasks:
a) Calculate each position's return and sigma move
b) Calculate portfolio total loss
c) Calculate position-weighted sigma
d) Which position contributed most to portfolio loss in $ terms?
e) Which position had the largest sigma move?
f) How did the flight-to-quality (TLT up) affect overall portfolio sigma?
g) If this is a 4σ portfolio event, what's the theoretical frequency?
h) Write a brief risk report paragraph summarizing the day

---

## Solutions Overview

### Problem 1 Solution Key Points:
- Day 31 return = ln(102.50/109.80) = -6.89%
- 30-day σ ≈ 1.2%
- z ≈ -5.7σ (Very Rare/Tail Event)
- Normal probability ≈ 0.000001%
- Yes, suggests fat tails

### Problem 4 Solution Key Points:
- Portfolio return ≈ -2.4%
- Portfolio sigma ≈ 2.1σ (Significant)
- META has highest individual sigma (-1.83σ) but AMZN close (-1.77σ)
- AAPL contributes most $ loss due to largest position

### Problem 5 Solution Key Points:
- S&P sigma = -12σ, Dow = -11.8σ, NASDAQ = -10.3σ, Russell = -10.2σ
- Joint probability under independence: 10^-50 (essentially impossible)
- Independence fails: market-wide stress creates correlation = 1
- Evidence of fat tails and correlation breakdown

### Problem 7 Solution Key Points:
- Expected 2σ days: 45.5, Observed: 58 (ratio 1.27x)
- Expected 3σ days: 2.7, Observed: 12 (ratio 4.4x)
- Expected 4σ days: 0.06, Observed: 4 (ratio 67x)
- Expected 5σ days: 0.0006, Observed: 2 (ratio 3333x)
- Severe fat tails; multiply normal probabilities by 50-100x for 4σ+

### Problem 10 Solution Key Points:
- SPY: -5.0%, QQQ: -6.6%, IWM: -8.0%, TLT: +4.0%
- SPY: -5σ, QQQ: -5.1σ, IWM: -5.3σ, TLT: +6.7σ (up)
- Portfolio loss: $25,020 (-5.0%)
- TLT's gain reduces portfolio sigma slightly
- IWM had worst sigma move; SPY largest $ loss

---

## Self-Assessment Guide

**Excellent (Can do all steps independently):**
You're ready for real-world quantitative analysis.

**Good (Minor calculation errors, concepts solid):**
Review specific formulas, practice more calculations.

**Developing (Struggling with multi-step problems):**
Return to earlier exercise sets, build foundation.

**Beginning (Difficulty with basic concepts):**
Re-read the theory notes before attempting more problems.

---

#exercises #comprehensive #integration #advanced
