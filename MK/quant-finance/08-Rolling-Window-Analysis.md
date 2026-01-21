# Rolling Window Analysis

Instead of using a single historical volatility estimate, rolling windows allow you to track how volatility evolves over time, providing more contextually relevant sigma move classifications.

---

## 1. Why Rolling Windows?

### The Problem with Static σ

Using one σ value for all time assumes volatility is constant. But volatility:
- **Clusters**: High vol follows high vol
- **Mean reverts**: Eventually returns to average
- **Regime shifts**: Can change fundamentally

### The Solution

Calculate σ over a **moving window** that slides through time, capturing the current volatility regime.

---

## 2. Rolling Window Mechanics

### Definition

At each time $t$, use data from $[t-w+1, t]$ where $w$ = window size

### Visualization

```
Time:    1  2  3  4  5  6  7  8  9  10 11 12 ...
Data:    x  x  x  x  x  x  x  x  x  x  x  x  ...

Window 1 (w=5): [1-5]
         ─────

Window 2:       [2-6]
            ─────

Window 3:          [3-7]
               ─────

...continues sliding forward
```

---

## 3. Rolling Mean Calculation

### Formula

$$\bar{R}_t = \frac{1}{w}\sum_{i=t-w+1}^{t} R_i$$

### Efficient Update (Rolling Sum)

Instead of recalculating from scratch:

$$\bar{R}_{t+1} = \bar{R}_t + \frac{R_{t+1} - R_{t-w+1}}{w}$$

### Example: 5-Day Rolling Mean

| Day | Return | 5-Day Sum | Rolling Mean |
|-----|--------|-----------|--------------|
| 1   | 0.5%   | -         | -            |
| 2   | -1.2%  | -         | -            |
| 3   | 0.8%   | -         | -            |
| 4   | 1.5%   | -         | -            |
| 5   | -0.3%  | 1.3%      | 0.26%        |
| 6   | 0.2%   | 1.0%      | 0.20%        |
| 7   | -0.8%  | 1.4%      | 0.28%        |
| 8   | 1.1%   | 1.7%      | 0.34%        |

Calculation for Day 6:
- Add new return: 0.2%
- Remove oldest (Day 1): 0.5%
- New sum: 1.3% - 0.5% + 0.2% = 1.0%
- Mean: 1.0% / 5 = 0.20%

---

## 4. Rolling Standard Deviation

### Formula

$$s_t = \sqrt{\frac{\sum_{i=t-w+1}^{t}(R_i - \bar{R}_t)^2}{w-1}}$$

### Computational Form (More Efficient)

$$s_t = \sqrt{\frac{\sum_{i=t-w+1}^{t} R_i^2 - w\bar{R}_t^2}{w-1}}$$

This avoids recalculating all deviations.

### Complete Worked Example: 5-Day Rolling σ

| Day | Return (%) | $R^2$ | Rolling Sum | Rolling $\sum R^2$ | Mean | σ |
|-----|------------|-------|-------------|-------------------|------|---|
| 1   | 0.5        | 0.25  | -           | -                 | -    | - |
| 2   | -1.2       | 1.44  | -           | -                 | -    | - |
| 3   | 0.8        | 0.64  | -           | -                 | -    | - |
| 4   | 1.5        | 2.25  | -           | -                 | -    | - |
| 5   | -0.3       | 0.09  | 1.3         | 4.67              | 0.26 | **1.04%** |
| 6   | 0.2        | 0.04  | 1.0         | 4.46              | 0.20 | **1.00%** |
| 7   | -0.8       | 0.64  | 1.4         | 3.66              | 0.28 | **0.93%** |

**Day 5 Calculation:**

$$s_5 = \sqrt{\frac{4.67 - 5(0.26)^2}{4}} = \sqrt{\frac{4.67 - 0.338}{4}} = \sqrt{\frac{4.332}{4}} = \sqrt{1.083} = 1.04\%$$

**Day 6 Calculation:**
- Remove Day 1: $R^2$ sum = 4.67 - 0.25 = 4.42
- Add Day 6: $R^2$ sum = 4.42 + 0.04 = 4.46
- Sum = 1.3 - 0.5 + 0.2 = 1.0, Mean = 0.20%

$$s_6 = \sqrt{\frac{4.46 - 5(0.20)^2}{4}} = \sqrt{\frac{4.46 - 0.20}{4}} = \sqrt{1.065} = 1.03\%$$

---

## 5. Rolling Sigma Moves

### Real-Time Classification

At each time $t$:

$$z_t = \frac{R_t - \bar{R}_{t-1}}{\sigma_{t-1}}$$

**Important:** Use the **previous period's** mean and σ (not including current return) to classify the current return.

### Example Calculation

Given at end of Day 6:
- Rolling mean (Days 2-6): 0.20%
- Rolling σ (Days 2-6): 1.00%

Day 7 return: -2.5%

$$z_7 = \frac{-2.5 - 0.20}{1.00} = -2.70\sigma$$

Classification: **Significant down move**

---

## 6. Choosing Window Size

### Trade-offs

| Window | Responsiveness | Stability | Use Case |
|--------|---------------|-----------|----------|
| 5-10   | Very High     | Low       | Intraday/HFT |
| 20     | High          | Medium    | Short-term trading |
| 60     | Medium        | High      | Swing trading |
| 120    | Low           | Very High | Position trading |
| 252    | Very Low      | Highest   | Long-term risk |

### Volatility of Volatility

Shorter windows → Higher "vol of vol"

$$\text{Vol of Vol} = \sigma(\sigma_t)$$

### Recommendation

Use multiple windows simultaneously:
- Short (20-day): Current regime
- Medium (60-day): Recent history
- Long (252-day): Historical baseline

---

## 7. Multi-Window Analysis

### Dashboard Approach

| Metric | 20-Day | 60-Day | 252-Day |
|--------|--------|--------|---------|
| Mean Return | 0.15% | 0.08% | 0.05% |
| Volatility | 1.8% | 1.5% | 1.2% |
| Today's Sigma | -1.67σ | -2.0σ | -2.5σ |

### Interpretation

- **All windows agree**: Strong signal
- **Windows disagree**: Regime transition possible
- **Short > Long**: Volatility expanding
- **Short < Long**: Volatility compressing

---

## 8. Handling the Cold Start

### The Problem

Rolling calculations need $w$ observations before first output.

### Solutions

1. **Wait**: No output until window full (cleanest)
2. **Expanding window**: Use all available data until w reached
3. **Initialization**: Use historical estimate to start

### Expanding Window Formula

For $t < w$:

$$s_t = \sqrt{\frac{\sum_{i=1}^{t}(R_i - \bar{R}_t)^2}{t-1}}$$

---

## 9. Rolling Statistics Table Template

### Data Collection

| Day | Price | Return | 20-Day Mean | 20-Day σ | Sigma Move |
|-----|-------|--------|-------------|----------|------------|
| 1   | 100.0 | -      | -           | -        | -          |
| 2   | 101.2 | 1.19%  | -           | -        | -          |
| ... | ...   | ...    | -           | -        | -          |
| 20  | 105.3 | 0.48%  | -           | -        | -          |
| 21  | 103.8 | -1.43% | 0.18%       | 1.05%    | -1.53σ     |
| 22  | 104.2 | 0.38%  | 0.15%       | 1.02%    | +0.23σ     |

### Workflow

```
For each new day t:
  1. Calculate return: R_t = ln(P_t/P_{t-1})
  2. Update rolling window: [t-w+1, t-1]
  3. Calculate rolling mean: μ_{t-1}
  4. Calculate rolling σ: σ_{t-1}
  5. Classify: z_t = (R_t - μ_{t-1}) / σ_{t-1}
```

---

## 10. Rolling Analysis Best Practices

### Consistency

- Always use the same window size for comparisons
- Document your window choice
- Be explicit about whether mean is included

### Edge Cases

- **Gaps**: Decide how to handle missing days
- **Outliers**: Consider whether to include extreme days in window
- **Events**: Corporate actions, splits need adjustment

### Validation

1. Verify calculations with known values
2. Compare to published volatility (VIX, etc.)
3. Check for coding errors in updates

---

## 11. Complete Rolling Analysis Example

### 20-Day Rolling Analysis

**Historical Data (20 days):**

| Day | Return (%) |
|-----|------------|
| 1   | 0.5        |
| 2   | -1.2       |
| 3   | 0.8        |
| 4   | 1.5        |
| 5   | -0.3       |
| 6   | 0.2        |
| 7   | -0.8       |
| 8   | 1.1        |
| 9   | 0.4        |
| 10  | -0.6       |
| 11  | 0.9        |
| 12  | -0.4       |
| 13  | 0.3        |
| 14  | -1.0       |
| 15  | 0.6        |
| 16  | -0.2       |
| 17  | 0.7        |
| 18  | -0.5       |
| 19  | 0.4        |
| 20  | -0.3       |

**Calculations:**

Sum = 1.8%, Mean = 0.09%

$$\sum(R - \bar{R})^2 = 8.22$$

$$\sigma = \sqrt{\frac{8.22}{19}} = 0.658\%$$

**Day 21 Return: -2.8%**

$$z_{21} = \frac{-2.8 - 0.09}{0.658} = \frac{-2.89}{0.658} = -4.39\sigma$$

**Classification: EXTREME DOWN MOVE (4-5σ)**

---

## Key Formulas

| Metric | Formula |
|--------|---------|
| Rolling Mean | $\bar{R}_t = \frac{1}{w}\sum_{i=t-w+1}^{t} R_i$ |
| Rolling Variance | $s_t^2 = \frac{\sum R_i^2 - w\bar{R}_t^2}{w-1}$ |
| Rolling Sigma Move | $z_t = \frac{R_t - \bar{R}_{t-1}}{\sigma_{t-1}}$ |

---

## Next Steps

Review [[09-Formula-Reference-Sheet]] for quick access to all formulas.

---

#rolling-window #volatility #time-series #dynamic-analysis
