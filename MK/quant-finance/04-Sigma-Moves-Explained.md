# Sigma Moves Explained

This is the core of what you're trying to analyze: **how to identify and classify large price deviations**. A sigma move tells you how unusual a price change is relative to historical behavior.

---

## 1. What is a Sigma Move?

A **sigma move** (or **σ move**) measures how many standard deviations a return is from the expected (mean) return.

### The Core Formula

$$\text{Sigma Move} = z = \frac{R_t - \mu}{\sigma}$$

Where:
- $R_t$ = Return at time $t$ (today's return)
- $\mu$ = Mean (average) return (often approximated as 0 for daily returns)
- $\sigma$ = Standard deviation of returns

### Interpretation

| Sigma Value | Meaning |
|-------------|---------|
| z = 0 | Return exactly at the mean |
| z = +1 | Return is 1σ above mean |
| z = -1 | Return is 1σ below mean |
| z = +3 | Return is 3σ above mean (rare up move) |
| z = -5 | Return is 5σ below mean (very rare crash) |

---

## 2. Complete Step-by-Step Calculation

### The Process

1. **Gather historical returns** (e.g., past 60 days)
2. **Calculate mean return** ($\mu$)
3. **Calculate standard deviation** ($\sigma$)
4. **For today's return**, apply the formula
5. **Classify** the sigma magnitude

### Detailed Example

**Historical daily returns (20 days):**
0.8, -0.5, 0.3, -0.2, 1.1, -0.7, 0.4, 0.6, -0.9, 0.2,
0.5, -0.3, 0.7, -0.4, 0.1, -0.6, 0.9, -0.1, 0.3, -0.8

**Step 1: Calculate Mean**
$$\mu = \frac{0.8-0.5+0.3-0.2+1.1-0.7+0.4+0.6-0.9+0.2+0.5-0.3+0.7-0.4+0.1-0.6+0.9-0.1+0.3-0.8}{20}$$
$$\mu = \frac{1.4}{20} = 0.07\%$$

**Step 2: Calculate Standard Deviation**

| Return | $(R - \mu)$ | $(R - \mu)^2$ |
|--------|-------------|---------------|
| 0.8    | 0.73        | 0.5329        |
| -0.5   | -0.57       | 0.3249        |
| 0.3    | 0.23        | 0.0529        |
| -0.2   | -0.27       | 0.0729        |
| 1.1    | 1.03        | 1.0609        |
| -0.7   | -0.77       | 0.5929        |
| 0.4    | 0.33        | 0.1089        |
| 0.6    | 0.53        | 0.2809        |
| -0.9   | -0.97       | 0.9409        |
| 0.2    | 0.13        | 0.0169        |
| 0.5    | 0.43        | 0.1849        |
| -0.3   | -0.37       | 0.1369        |
| 0.7    | 0.63        | 0.3969        |
| -0.4   | -0.47       | 0.2209        |
| 0.1    | 0.03        | 0.0009        |
| -0.6   | -0.67       | 0.4489        |
| 0.9    | 0.83        | 0.6889        |
| -0.1   | -0.17       | 0.0289        |
| 0.3    | 0.23        | 0.0529        |
| -0.8   | -0.87       | 0.7569        |
| **Sum** |           | **6.9020**    |

$$\sigma = \sqrt{\frac{6.9020}{19}} = \sqrt{0.3633} = 0.603\%$$

**Step 3: Classify Today's Return**

Suppose today's return is **-2.5%**

$$z = \frac{-2.5 - 0.07}{0.603} = \frac{-2.57}{0.603} = -4.26\sigma$$

**This is a 4.26-sigma down move!**

---

## 3. Sigma Classification Scale

### Standard Classification

| Sigma Range | Classification | Rarity (Normal Dist) |
|-------------|----------------|---------------------|
| 0 to ±1σ    | Normal         | ~68% of days        |
| ±1σ to ±2σ  | Elevated       | ~27% of days        |
| ±2σ to ±3σ  | Significant    | ~4.3% of days       |
| ±3σ to ±4σ  | Extreme        | ~0.26% of days      |
| ±4σ to ±5σ  | Rare           | ~0.006% of days     |
| ±5σ to ±6σ  | Very Rare      | ~0.00006% of days   |
| Beyond ±6σ  | Tail Event     | Theoretically almost never |

### Practical Classification for Trading

| Sigma | Typical Interpretation | Action Implication |
|-------|----------------------|-------------------|
| < 1σ  | Noise               | Normal fluctuation |
| 1-2σ  | Notable             | Worth monitoring |
| 2-3σ  | Significant         | Investigate cause |
| 3-4σ  | Major move          | Risk assessment needed |
| 4-5σ  | Crisis-level        | Possible regime change |
| 5+σ   | Black swan territory | Historical event |

---

## 4. Probability Table (Normal Distribution)

### One-Tailed Probabilities

| Sigma | P(Z > z) | Expected Frequency |
|-------|----------|-------------------|
| 1.0   | 15.87%   | 40 days/year |
| 1.5   | 6.68%    | 17 days/year |
| 2.0   | 2.28%    | 6 days/year |
| 2.5   | 0.62%    | 1.5 days/year |
| 3.0   | 0.135%   | 1 day/3 years |
| 3.5   | 0.023%   | 1 day/17 years |
| 4.0   | 0.0032%  | 1 day/126 years |
| 4.5   | 0.00034% | 1 day/1,170 years |
| 5.0   | 0.000029%| 1 day/13,932 years |

### Two-Tailed Probabilities (Either Direction)

| Sigma | P(|Z| > z) | Expected Frequency |
|-------|------------|-------------------|
| 1.0   | 31.73%     | 80 days/year |
| 2.0   | 4.55%      | 11 days/year |
| 3.0   | 0.27%      | 1 day/1.5 years |
| 4.0   | 0.0063%    | 1 day/63 years |
| 5.0   | 0.000057%  | 1 day/7,000 years |
| 6.0   | 0.0000002% | 1 day/500,000 years |

---

## 5. The Mean Assumption

### Option 1: Use Calculated Mean

$$z = \frac{R_t - \bar{R}}{\sigma}$$

More accurate but requires mean calculation.

### Option 2: Assume Mean = 0

$$z = \frac{R_t}{\sigma}$$

For daily returns, the mean is typically very small (0.02-0.05%), so this simplification is often acceptable:

**Example:**
- True mean: 0.04%
- σ = 1.5%
- Return: -3.0%

With mean: $z = \frac{-3.0 - 0.04}{1.5} = -2.03\sigma$

Without mean: $z = \frac{-3.0}{1.5} = -2.00\sigma$

Difference is negligible for most purposes.

### When Mean Matters

- Strongly trending markets
- Longer time periods (weekly, monthly returns)
- High-frequency data with drift

---

## 6. Lookback Period Selection

### How Much History to Use?

| Lookback | Pros | Cons |
|----------|------|------|
| 10 days  | Captures current regime | Very noisy |
| 20 days  | Monthly view | Still volatile |
| 60 days  | Quarterly view | Good balance |
| 120 days | Half-year view | May include old regimes |
| 252 days | Full year | Smooths seasonality |

### Recommendation for Different Uses

| Purpose | Suggested Lookback |
|---------|-------------------|
| Intraday trading | 5-20 days |
| Swing trading | 20-60 days |
| Position trading | 60-120 days |
| Risk management | 252 days (or longer) |

---

## 7. Real-World Examples

### Example 1: Normal Day

Stock XYZ historical data (60 days):
- Mean return: 0.05%
- Standard deviation: 1.2%

Today's return: +0.8%

$$z = \frac{0.8 - 0.05}{1.2} = \frac{0.75}{1.2} = +0.625\sigma$$

**Classification: Normal** (well within ±1σ)

### Example 2: Notable Move

Same stock, today's return: -2.5%

$$z = \frac{-2.5 - 0.05}{1.2} = \frac{-2.55}{1.2} = -2.125\sigma$$

**Classification: Significant** (2-3σ range)

### Example 3: Extreme Move

Same stock, today's return: -5.0%

$$z = \frac{-5.0 - 0.05}{1.2} = \frac{-5.05}{1.2} = -4.21\sigma$$

**Classification: Rare** (4-5σ range)

### Example 4: Black Monday (October 19, 1987)

- S&P 500 dropped 20.5% in one day
- Historical daily σ was approximately 1%
- This was roughly a **20-sigma event!**

Under normal distribution, this should happen once every $10^{89}$ years - far older than the universe!

---

## 8. Calculating Sigma for Multiple Assets

### Create a Sigma Dashboard

| Stock | Return | Mean | σ | Sigma Move | Classification |
|-------|--------|------|---|------------|----------------|
| AAPL  | -2.1%  | 0.08%| 1.5% | -1.45σ | Elevated |
| MSFT  | +1.8%  | 0.06%| 1.3% | +1.34σ | Elevated |
| TSLA  | -5.2%  | 0.12%| 3.2% | -1.66σ | Elevated |
| SPY   | -1.0%  | 0.03%| 0.9% | -1.14σ | Elevated |

### Cross-Asset Analysis

When multiple assets show high sigma moves simultaneously:
- **Correlation spike** - systemic risk
- **Market-wide event** - macro factor
- **Sector rotation** - industry-specific news

---

## 9. The Algorithm Summary

```
SIGMA MOVE CALCULATION:

Input:
  - Historical returns R₁, R₂, ..., Rₙ
  - Current return Rₜ

Process:
  1. μ = (1/n) × Σ Rᵢ           [Calculate mean]
  2. σ = √[(1/(n-1)) × Σ(Rᵢ-μ)²] [Calculate std dev]
  3. z = (Rₜ - μ) / σ           [Calculate z-score]

Output:
  - z (the sigma move)
  - Classification based on |z| value
```

---

## 10. Important Caveats

### Normal Distribution Assumption

The probability tables assume **normal distribution**, but markets have:
- **Fat tails** (leptokurtosis): Extreme moves more frequent
- **Negative skew**: Crashes more severe than rallies
- **Volatility clustering**: Calm follows calm, turbulent follows turbulent

### What This Means Practically

A "5-sigma event" in theory happens once in 7,000 years.
In practice, we see 5-sigma moves **every few years**.

> "In markets, 6-sigma events happen every few years. In manufacturing, 6-sigma means defect-free."

### Adjusting Expectations

| Theoretical σ | Real-World Equivalent |
|---------------|----------------------|
| 3σ event (1/year) | Actually ~4-6/year |
| 4σ event (1/63 years) | Actually ~1-2/year |
| 5σ event (1/7000 years) | Actually every few years |

---

## Key Formula

$$\boxed{z = \frac{R_t - \mu}{\sigma}}$$

This single formula is the foundation of all sigma move analysis.

---

## Next Steps

Continue to [[05-Volatility-Estimation]] for advanced techniques to estimate σ more accurately.

---

#sigma-moves #z-score #volatility #extreme-events
