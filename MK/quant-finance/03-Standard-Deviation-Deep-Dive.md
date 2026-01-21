# Standard Deviation Deep Dive

Standard deviation is the cornerstone of measuring price volatility and classifying sigma moves. This guide provides a comprehensive treatment.

---

## 1. What Standard Deviation Measures

Standard deviation ($\sigma$ or $s$) measures the **dispersion** or **spread** of data around the mean.

- **Low σ**: Data clustered tightly around mean (low volatility)
- **High σ**: Data spread widely around mean (high volatility)

---

## 2. The Complete Standard Deviation Formula

### Population Standard Deviation

$$\sigma = \sqrt{\frac{\sum_{i=1}^{N}(x_i - \mu)^2}{N}}$$

### Sample Standard Deviation

$$s = \sqrt{\frac{\sum_{i=1}^{n}(x_i - \bar{x})^2}{n-1}}$$

### Expanded Step-by-Step

$$s = \sqrt{\frac{(x_1-\bar{x})^2 + (x_2-\bar{x})^2 + ... + (x_n-\bar{x})^2}{n-1}}$$

---

## 3. Step-by-Step Calculation Method

### The Algorithm

1. **Calculate the mean** ($\bar{x}$)
2. **Subtract the mean** from each value ($x_i - \bar{x}$)
3. **Square each difference** $(x_i - \bar{x})^2$
4. **Sum all squared differences** $\sum(x_i - \bar{x})^2$
5. **Divide by (n-1)** for sample variance
6. **Take square root** for standard deviation

### Complete Worked Example

**Daily returns (%):** 0.5, -1.2, 0.8, 1.5, -0.3, 0.2, -0.8, 1.1, 0.4, -0.6

**Step 1: Calculate Mean**
$$\bar{x} = \frac{0.5 + (-1.2) + 0.8 + 1.5 + (-0.3) + 0.2 + (-0.8) + 1.1 + 0.4 + (-0.6)}{10}$$
$$\bar{x} = \frac{1.6}{10} = 0.16\%$$

**Step 2-4: Deviations and Squared Deviations**

| Day | $x_i$ | $x_i - \bar{x}$ | $(x_i - \bar{x})^2$ |
|-----|-------|-----------------|---------------------|
| 1   | 0.5   | 0.34            | 0.1156              |
| 2   | -1.2  | -1.36           | 1.8496              |
| 3   | 0.8   | 0.64            | 0.4096              |
| 4   | 1.5   | 1.34            | 1.7956              |
| 5   | -0.3  | -0.46           | 0.2116              |
| 6   | 0.2   | 0.04            | 0.0016              |
| 7   | -0.8  | -0.96           | 0.9216              |
| 8   | 1.1   | 0.94            | 0.8836              |
| 9   | 0.4   | 0.24            | 0.0576              |
| 10  | -0.6  | -0.76           | 0.5776              |
| **Sum** | | | **6.8240** |

**Step 5: Calculate Variance**
$$s^2 = \frac{6.8240}{10-1} = \frac{6.8240}{9} = 0.7582\%^2$$

**Step 6: Calculate Standard Deviation**
$$s = \sqrt{0.7582} = 0.871\%$$

**Interpretation:** Daily returns typically deviate about 0.87% from the mean of 0.16%.

---

## 4. Understanding the Formula Components

### Why Square the Differences?

1. **Eliminates negative signs**: Deviations below mean don't cancel those above
2. **Penalizes large deviations**: A 2% deviation contributes 4x as much as a 1% deviation
3. **Mathematical properties**: Enables calculus-based analysis

### Why Divide by (n-1)?

This is **Bessel's correction** for sample statistics.

**The problem:**
- We estimate $\mu$ using $\bar{x}$ from the same data
- Data points are naturally closer to their own mean than to the true population mean
- Using $n$ would underestimate the true variance

**Mathematical proof shows:** Using $(n-1)$ gives an **unbiased estimator** of population variance.

### When to Use n vs (n-1)

| Use $n$ | Use $(n-1)$ |
|---------|-------------|
| You have the entire population | You have a sample |
| Calculating descriptive stats only | Making inferences about population |
| Very large n (difference negligible) | Small sample sizes |

---

## 5. Alternative Calculation Formula

There's a computationally equivalent formula that's sometimes easier:

$$s^2 = \frac{\sum x_i^2 - n\bar{x}^2}{n-1}$$

Or equivalently:

$$s^2 = \frac{\sum x_i^2 - \frac{(\sum x_i)^2}{n}}{n-1}$$

### Example Using Alternative Formula

Same data: 0.5, -1.2, 0.8, 1.5, -0.3, 0.2, -0.8, 1.1, 0.4, -0.6

| $x_i$ | $x_i^2$ |
|-------|---------|
| 0.5   | 0.25    |
| -1.2  | 1.44    |
| 0.8   | 0.64    |
| 1.5   | 2.25    |
| -0.3  | 0.09    |
| 0.2   | 0.04    |
| -0.8  | 0.64    |
| 1.1   | 1.21    |
| 0.4   | 0.16    |
| -0.6  | 0.36    |
| **Sum: 1.6** | **Sum: 7.08** |

$$s^2 = \frac{7.08 - 10(0.16)^2}{9} = \frac{7.08 - 0.256}{9} = \frac{6.824}{9} = 0.7582$$

Same answer!

---

## 6. Properties of Standard Deviation

### Key Mathematical Properties

1. **Non-negative**: $s \geq 0$ always
2. **Zero only if constant**: $s = 0$ iff all values are identical
3. **Same units as data**: If data is in %, σ is in %
4. **Sensitive to outliers**: One extreme value can significantly increase σ

### Scaling Properties

If you multiply all data by constant $c$:
$$s_{new} = |c| \times s_{original}$$

If you add constant $c$ to all data:
$$s_{new} = s_{original}$$ (unchanged!)

---

## 7. Volatility vs Standard Deviation

In finance, **volatility** typically means standard deviation of returns.

### Daily Volatility
$$\sigma_{daily} = s_{daily\ returns}$$

### Annualized Volatility
$$\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$$

### Why $\sqrt{252}$?

Under the assumption that daily returns are **independent and identically distributed (i.i.d.)**:

- Variance of sum = Sum of variances
- $Var(R_1 + R_2 + ... + R_{252}) = 252 \times Var(R_{daily})$
- $\sigma_{annual}^2 = 252 \times \sigma_{daily}^2$
- $\sigma_{annual} = \sqrt{252} \times \sigma_{daily}$

### Volatility Conversion Table

| From | To | Multiply σ by |
|------|-----|---------------|
| Daily | Weekly | $\sqrt{5} = 2.236$ |
| Daily | Monthly | $\sqrt{21} = 4.583$ |
| Daily | Annual | $\sqrt{252} = 15.875$ |
| Weekly | Annual | $\sqrt{52} = 7.211$ |
| Monthly | Annual | $\sqrt{12} = 3.464$ |

---

## 8. Interpreting Standard Deviation Values

### Typical Daily Volatility Ranges

| Asset Type | Daily σ | Annual σ |
|------------|---------|----------|
| Large-cap stocks | 1-2% | 15-30% |
| Small-cap stocks | 2-4% | 30-60% |
| Tech stocks | 2-3% | 30-50% |
| Index (S&P 500) | 0.8-1.2% | 12-20% |
| Bonds | 0.2-0.5% | 3-8% |
| Cryptocurrencies | 3-6% | 50-100% |

### What the Numbers Mean

For a stock with daily σ = 2%:
- ~68% of days, the return will be within ±2% of the mean
- ~95% of days, the return will be within ±4% of the mean
- ~99.7% of days, the return will be within ±6% of the mean

*(Assuming normal distribution - which isn't perfectly true!)*

---

## 9. Rolling Standard Deviation

Instead of one σ for all time, calculate σ over a moving window.

### Formula for Rolling σ

At time $t$, with window size $w$:

$$s_t = \sqrt{\frac{\sum_{i=t-w+1}^{t}(R_i - \bar{R}_{window})^2}{w-1}}$$

### Example: 5-Day Rolling Volatility

| Day | Return | 5-Day Window | Rolling σ |
|-----|--------|--------------|-----------|
| 1   | 0.5%   | -            | -         |
| 2   | -1.2%  | -            | -         |
| 3   | 0.8%   | -            | -         |
| 4   | 1.5%   | -            | -         |
| 5   | -0.3%  | [0.5,-1.2,0.8,1.5,-0.3] | 1.04% |
| 6   | 0.2%   | [-1.2,0.8,1.5,-0.3,0.2] | 1.00% |
| 7   | -0.8%  | [0.8,1.5,-0.3,0.2,-0.8] | 0.93% |

### Common Window Sizes

| Window | Days | Use Case |
|--------|------|----------|
| Short | 5-10 | Immediate volatility |
| Medium | 20-30 | Monthly volatility |
| Long | 60-90 | Quarterly volatility |
| Very Long | 252 | Annual volatility |

---

## 10. Practical Considerations

### Choosing Sample Period

- **Too short**: Noisy estimate, unstable
- **Too long**: May not reflect current conditions
- **Common choice**: 20-60 trading days for tactical analysis

### Data Quality Issues

1. **Outliers**: Consider if extreme values are real or data errors
2. **Missing data**: Decide how to handle gaps
3. **Corporate actions**: Use adjusted prices
4. **Time zones**: Ensure consistent pricing time

### Regime Changes

Volatility is not constant! Watch for:
- Market crises (volatility spikes)
- Calm periods (volatility compression)
- Structural breaks (fundamental changes)

---

## 11. Summary Workflow

```
1. Gather adjusted price data
2. Calculate log returns
3. Choose sample period
4. Calculate mean return
5. Calculate deviations from mean
6. Square deviations
7. Sum squared deviations
8. Divide by (n-1)
9. Take square root → Daily σ
10. Multiply by √252 → Annual σ (if needed)
```

---

## Key Formulas

| Formula | Expression |
|---------|------------|
| Sample Std Dev | $s = \sqrt{\frac{\sum(x_i - \bar{x})^2}{n-1}}$ |
| Alternative | $s = \sqrt{\frac{\sum x_i^2 - n\bar{x}^2}{n-1}}$ |
| Annualized | $\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$ |

---

## Next Steps

Continue to [[04-Sigma-Moves-Explained]] to learn how to classify moves by their sigma magnitude.

---

#standard-deviation #volatility #variance #statistics
