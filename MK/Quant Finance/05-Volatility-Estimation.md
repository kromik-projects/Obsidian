# Volatility Estimation Techniques

Accurate volatility estimation is crucial for meaningful sigma move classification. This guide covers various methods from simple to sophisticated.

---

## 1. Historical Volatility (Simple Standard Deviation)

### The Basic Method

$$\sigma_{historical} = \sqrt{\frac{1}{n-1}\sum_{t=1}^{n}(R_t - \bar{R})^2}$$

### Characteristics
- **Simple** to calculate
- **Backward-looking** (uses past data only)
- **Equal weighting** (all observations count the same)
- **Sensitive** to sample period choice

### Implementation

```
1. Collect n historical returns
2. Calculate mean return
3. Calculate squared deviations
4. Average and take square root
```

---

## 2. Exponentially Weighted Moving Average (EWMA)

### The Problem with Simple σ

All past returns weighted equally means:
- A shock 60 days ago counts same as yesterday
- Slow to react to changing volatility
- Doesn't capture volatility clustering

### EWMA Solution

Weight recent observations more heavily:

$$\sigma_t^2 = \lambda \sigma_{t-1}^2 + (1-\lambda) R_{t-1}^2$$

Where:
- $\lambda$ = decay factor (typically 0.94 for daily data)
- $\sigma_t^2$ = variance estimate at time $t$
- $R_{t-1}$ = previous return

### Expanded Form

$$\sigma_t^2 = (1-\lambda) \sum_{i=1}^{\infty} \lambda^{i-1} R_{t-i}^2$$

### Choosing Lambda (λ)

| λ Value | Half-life (days) | Characteristics |
|---------|------------------|-----------------|
| 0.90    | 6.6              | Very reactive |
| 0.94    | 11.1             | RiskMetrics standard |
| 0.97    | 22.8             | Smoother |
| 0.99    | 68.9             | Very smooth |

**Half-life formula:**
$$h = \frac{\ln(0.5)}{\ln(\lambda)}$$

### Step-by-Step EWMA Calculation

**Given:** λ = 0.94, Initial σ² = 0.0001 (1% volatility)

| Day | Return (%) | Return² | EWMA Variance | EWMA σ (%) |
|-----|------------|---------|---------------|------------|
| 0   | -          | -       | 0.000100      | 1.00       |
| 1   | 0.5        | 0.000025| 0.000094 + 0.0000015 = 0.0000955 | 0.98 |
| 2   | -2.0       | 0.0004  | 0.0000898 + 0.000024 = 0.000114 | 1.07 |
| 3   | 1.5        | 0.000225| 0.000107 + 0.0000135 = 0.000120 | 1.10 |
| 4   | -0.3       | 0.000009| 0.000113 + 0.00000054 = 0.000114 | 1.07 |

**Calculation for Day 2:**
$$\sigma_2^2 = 0.94 \times 0.0000955 + 0.06 \times 0.0004 = 0.000114$$
$$\sigma_2 = \sqrt{0.000114} = 0.0107 = 1.07\%$$

---

## 3. GARCH Models

### GARCH(1,1) - The Workhorse Model

**Generalized Autoregressive Conditional Heteroskedasticity**

$$\sigma_t^2 = \omega + \alpha R_{t-1}^2 + \beta \sigma_{t-1}^2$$

Where:
- $\omega$ = constant term (long-run variance component)
- $\alpha$ = weight on recent squared return
- $\beta$ = weight on previous variance
- Constraint: $\alpha + \beta < 1$ for stationarity

### Interpretation

- **$\omega$**: Base level of variance
- **$\alpha$**: How fast volatility reacts to shocks
- **$\beta$**: How persistent volatility is

### Long-Run Variance

$$\sigma_{long-run}^2 = \frac{\omega}{1 - \alpha - \beta}$$

### Typical Parameter Values

For daily stock returns:
- $\omega$ ≈ 0.00001
- $\alpha$ ≈ 0.05 - 0.10
- $\beta$ ≈ 0.85 - 0.95

### EWMA as Special Case

EWMA is GARCH(1,1) with:
- $\omega = 0$
- $\alpha = 1 - \lambda$
- $\beta = \lambda$

### Example GARCH Calculation

**Parameters:** ω = 0.00001, α = 0.08, β = 0.90

| Day | Return (%) | $R^2$ | Previous $\sigma^2$ | New $\sigma^2$ | σ (%) |
|-----|------------|-------|---------------------|----------------|-------|
| 0   | -          | -     | 0.000100            | -              | 1.00  |
| 1   | -2.5       |0.000625| 0.000100           | 0.00014        | 1.18  |
| 2   | 1.0        |0.000100| 0.000140           | 0.000144       | 1.20  |

**Day 1 calculation:**
$$\sigma_1^2 = 0.00001 + 0.08(0.000625) + 0.90(0.0001) = 0.00001 + 0.00005 + 0.00009 = 0.00015$$

---

## 4. Realized Volatility (High-Frequency)

### Using Intraday Data

If you have intraday prices, you can compute more accurate volatility.

### Standard Realized Volatility

$$RV_t = \sum_{i=1}^{M} r_{t,i}^2$$

Where:
- $M$ = number of intraday intervals
- $r_{t,i}$ = return in interval $i$ on day $t$

### Example: 5-Minute Returns

For a stock with 78 five-minute bars per day:

| Interval | Price | Return | Return² |
|----------|-------|--------|---------|
| 1        | 100.00| -      | -       |
| 2        | 100.15| 0.15%  | 0.000225|
| 3        | 100.05| -0.10% | 0.000100|
| ...      | ...   | ...    | ...     |
| 78       | 101.20| 0.08%  | 0.000064|

$$RV = \sum \text{Return}^2 = \text{annualize appropriately}$$

### Advantages
- Uses more information
- More accurate volatility estimate
- Captures intraday dynamics

### Disadvantages
- Requires high-frequency data
- Microstructure noise at very high frequencies
- More complex implementation

---

## 5. Parkinson Volatility (Range-Based)

### Using High-Low Range

$$\sigma_{Parkinson} = \sqrt{\frac{1}{4 \ln(2)} \cdot \frac{1}{n} \sum_{t=1}^{n} \left[\ln\left(\frac{H_t}{L_t}\right)\right]^2}$$

Where:
- $H_t$ = High price on day $t$
- $L_t$ = Low price on day $t$

### Simplified Form

$$\sigma_P \approx 0.601 \times \text{Average}\left[\ln\left(\frac{H}{L}\right)\right]$$

### Example Calculation

| Day | High | Low | ln(H/L) | [ln(H/L)]² |
|-----|------|-----|---------|------------|
| 1   | 102  | 99  | 0.0299  | 0.000894   |
| 2   | 103  | 100 | 0.0296  | 0.000876   |
| 3   | 101  | 98  | 0.0302  | 0.000912   |
| 4   | 104  | 101 | 0.0293  | 0.000858   |
| 5   | 102  | 99  | 0.0299  | 0.000894   |
| **Avg** | | | | **0.000887** |

$$\sigma_P = \sqrt{\frac{0.000887}{4 \times 0.693}} = \sqrt{\frac{0.000887}{2.772}} = \sqrt{0.000320} = 1.79\%$$

### Advantages
- More efficient (uses more price information)
- 5x more efficient than close-to-close
- Less affected by closing price randomness

### Disadvantages
- Assumes continuous trading
- Biased downward with gaps

---

## 6. Garman-Klass Volatility

### Using OHLC Data

$$\sigma_{GK}^2 = \frac{1}{n}\sum_{t=1}^{n}\left[0.5(\ln H_t - \ln L_t)^2 - (2\ln 2 - 1)(\ln C_t - \ln O_t)^2\right]$$

Where:
- O = Open, H = High, L = Low, C = Close

### Simplified Coefficients

$$\sigma_{GK}^2 = 0.5(h-l)^2 - 0.386(c-o)^2$$

Where h, l, c, o are log prices.

### Even More Efficient

Garman-Klass is about 8x more efficient than close-to-close volatility!

---

## 7. Yang-Zhang Volatility

### The Most Complete Estimator

Combines overnight and intraday volatility:

$$\sigma_{YZ}^2 = \sigma_o^2 + k\sigma_c^2 + (1-k)\sigma_{RS}^2$$

Where:
- $\sigma_o^2$ = overnight variance (close to open)
- $\sigma_c^2$ = open to close variance
- $\sigma_{RS}^2$ = Rogers-Satchell variance
- $k$ = optimal weighting factor

### Advantages
- Handles overnight gaps
- Most efficient of OHLC estimators
- Unbiased for assets with opening gaps

---

## 8. Comparison of Estimators

### Relative Efficiency

| Estimator | Relative Efficiency | Data Needed |
|-----------|--------------------:|-------------|
| Close-to-Close | 1.0 | Close only |
| Parkinson | 5.0 | High, Low |
| Garman-Klass | 7.4 | O, H, L, C |
| Yang-Zhang | 14.0 | O, H, L, C |
| Realized Volatility | 20+ | Intraday |

Higher efficiency = fewer data points needed for same accuracy.

### Which to Use?

| Situation | Recommended |
|-----------|-------------|
| Only closing prices | Simple or EWMA |
| Have OHLC | Yang-Zhang or Garman-Klass |
| Have intraday data | Realized Volatility |
| Need quick estimate | Parkinson (just H/L) |
| Modeling time-varying vol | GARCH |

---

## 9. Volatility Lookback Selection

### Impact on Sigma Classification

Different lookback periods → Different σ → Different sigma moves!

**Example:**
- Stock return today: -3.0%
- 20-day σ: 1.0% → Sigma move = -3.0σ
- 60-day σ: 1.5% → Sigma move = -2.0σ
- 252-day σ: 2.0% → Sigma move = -1.5σ

### Best Practices

1. **Be consistent**: Pick a lookback and stick with it
2. **Document**: Always note what lookback you used
3. **Compare**: Sometimes useful to see multiple lookbacks
4. **Context**: Shorter for tactical, longer for strategic

---

## 10. Practical Workflow

```
VOLATILITY ESTIMATION WORKFLOW:

1. GATHER DATA
   - Minimum: Closing prices
   - Better: OHLC data
   - Best: Intraday data

2. CHOOSE METHOD
   - Simple σ for basic analysis
   - EWMA for time-varying
   - GARCH for modeling
   - Yang-Zhang for OHLC efficiency

3. CHOOSE LOOKBACK
   - Document the choice
   - Consider analysis purpose

4. CALCULATE
   - Apply formulas carefully
   - Verify against known values

5. VALIDATE
   - Does it make sense?
   - Compare to market norms
   - Check for data issues
```

---

## Key Formulas Summary

| Method | Formula |
|--------|---------|
| Simple | $\sigma = \sqrt{\frac{\sum(R-\bar{R})^2}{n-1}}$ |
| EWMA | $\sigma_t^2 = \lambda\sigma_{t-1}^2 + (1-\lambda)R_{t-1}^2$ |
| GARCH(1,1) | $\sigma_t^2 = \omega + \alpha R_{t-1}^2 + \beta\sigma_{t-1}^2$ |
| Parkinson | $\sigma = \sqrt{\frac{\ln(H/L)^2}{4\ln(2)}}$ |

---

## Next Steps

Continue to [[06-Probability-of-Extreme-Moves]] to understand the mathematics of rare events.

---

#volatility #EWMA #GARCH #estimation
