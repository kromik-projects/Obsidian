# Understanding Returns

Before calculating sigma moves, you must understand how to properly calculate and interpret returns. This is fundamental to all quantitative analysis.

---

## 1. Why Returns, Not Prices?

We analyze **returns** rather than prices because:

1. **Comparability**: A $5 move in a $500 stock (1%) is different from $5 in a $50 stock (10%)
2. **Stationarity**: Returns tend to be more statistically stable than prices
3. **Compounding**: Returns can be compounded to get total performance
4. **Normality**: Returns are closer to normally distributed than prices

---

## 2. Types of Returns

### Simple (Arithmetic) Return

The percentage change in price.

$$R_t^{simple} = \frac{P_t - P_{t-1}}{P_{t-1}} = \frac{P_t}{P_{t-1}} - 1$$

#### Example
- Yesterday's close: $100
- Today's close: $103

$$R = \frac{103 - 100}{100} = \frac{3}{100} = 0.03 = 3\%$$

### Log (Continuously Compounded) Return

The natural logarithm of the price ratio.

$$R_t^{log} = \ln\left(\frac{P_t}{P_{t-1}}\right) = \ln(P_t) - \ln(P_{t-1})$$

#### Example
Same prices as above:

$$R = \ln\left(\frac{103}{100}\right) = \ln(1.03) = 0.0296 = 2.96\%$$

### Comparison: Simple vs Log Returns

| Aspect | Simple Return | Log Return |
|--------|---------------|------------|
| Interpretation | Intuitive | Less intuitive |
| Aggregation over time | Multiply: $(1+R_1)(1+R_2)...$ | Add: $R_1 + R_2 + ...$ |
| Aggregation across assets | Can average | Cannot directly average |
| Symmetry | Asymmetric | Symmetric |
| Distribution | Slightly skewed | More symmetric |

### Symmetry Example

Stock moves from $100 → $110 → $100

**Simple returns:**
- Up: $\frac{110-100}{100} = +10\%$
- Down: $\frac{100-110}{110} = -9.09\%$

**Log returns:**
- Up: $\ln(110/100) = +9.53\%$
- Down: $\ln(100/110) = -9.53\%$

Log returns are symmetric!

---

## 3. Converting Between Return Types

### Simple to Log
$$R^{log} = \ln(1 + R^{simple})$$

### Log to Simple
$$R^{simple} = e^{R^{log}} - 1$$

### When Are They Approximately Equal?

For small returns (< 5%), simple and log returns are nearly identical:

| Simple Return | Log Return | Difference |
|---------------|------------|------------|
| 1%            | 0.995%     | 0.005%     |
| 2%            | 1.980%     | 0.020%     |
| 5%            | 4.879%     | 0.121%     |
| 10%           | 9.531%     | 0.469%     |
| 20%           | 18.232%    | 1.768%     |

---

## 4. Return Time Periods

### Scaling Returns

**Daily to Annual (approximation):**

For **simple returns** (not exact due to compounding):
$$R_{annual} \approx R_{daily} \times 252$$

For **log returns** (exact):
$$R_{annual} = R_{daily} \times 252$$

Where 252 = approximate trading days per year.

### Common Time Periods

| Period | Trading Days | Calendar Days |
|--------|--------------|---------------|
| Daily  | 1            | 1             |
| Weekly | 5            | 7             |
| Monthly| 21           | 30            |
| Quarterly | 63        | 91            |
| Annual | 252          | 365           |

---

## 5. Calculating Returns from Data

### Step-by-Step Process

Given a price series: $P_0, P_1, P_2, ..., P_n$

**Step 1:** Choose return type (usually log for sigma analysis)

**Step 2:** Calculate each return:
$$R_t = \ln(P_t) - \ln(P_{t-1})$$

**Step 3:** You get $n$ returns from $n+1$ prices

### Worked Example

| Day | Price | ln(Price) | Log Return |
|-----|-------|-----------|------------|
| 0   | 100.00 | 4.6052   | -          |
| 1   | 101.50 | 4.6201   | 0.0149 (1.49%) |
| 2   | 99.80  | 4.6030   | -0.0171 (-1.71%) |
| 3   | 102.30 | 4.6278   | 0.0248 (2.48%) |
| 4   | 101.00 | 4.6151   | -0.0127 (-1.27%) |
| 5   | 103.50 | 4.6396   | 0.0245 (2.45%) |

**Calculations:**
- $R_1 = \ln(101.50) - \ln(100.00) = 4.6201 - 4.6052 = 0.0149$
- $R_2 = \ln(99.80) - \ln(101.50) = 4.6030 - 4.6201 = -0.0171$
- And so on...

---

## 6. Return Statistics

Once you have returns, calculate:

### Mean Return
$$\bar{R} = \frac{1}{n}\sum_{t=1}^{n} R_t$$

From our example:
$$\bar{R} = \frac{0.0149 + (-0.0171) + 0.0248 + (-0.0127) + 0.0245}{5} = \frac{0.0344}{5} = 0.00688 = 0.688\%$$

### Return Variance
$$s^2 = \frac{1}{n-1}\sum_{t=1}^{n}(R_t - \bar{R})^2$$

| $R_t$ | $R_t - \bar{R}$ | $(R_t - \bar{R})^2$ |
|-------|-----------------|---------------------|
| 0.0149 | 0.0080 | 0.0000640 |
| -0.0171 | -0.0240 | 0.0005760 |
| 0.0248 | 0.0179 | 0.0003204 |
| -0.0127 | -0.0196 | 0.0003842 |
| 0.0245 | 0.0176 | 0.0003098 |
| **Sum** | | **0.0016544** |

$$s^2 = \frac{0.0016544}{4} = 0.0004136$$

### Return Standard Deviation
$$s = \sqrt{0.0004136} = 0.0203 = 2.03\%$$

---

## 7. Annualizing Return Statistics

### Annualizing Mean Return

$$\bar{R}_{annual} = \bar{R}_{daily} \times 252$$

Example: $0.688\% \times 252 = 173.4\%$ annually

### Annualizing Volatility (Standard Deviation)

$$\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$$

Example: $2.03\% \times \sqrt{252} = 2.03\% \times 15.87 = 32.2\%$ annually

> **Why square root?** Because variance scales linearly with time (under certain assumptions), so standard deviation scales with the square root of time.

---

## 8. Which Return to Use for Sigma Analysis?

### Recommendation: Log Returns

For calculating sigma moves, **log returns** are preferred because:

1. **Additivity**: Log returns sum over time
2. **Symmetry**: Equal magnitude for up/down moves
3. **Better normality**: Closer to normal distribution
4. **No negative prices**: $e^{R}$ is always positive

### The Choice Matters!

For a 20% simple return down:
- Simple: -20%
- Log: $\ln(0.80) = -22.3\%$

The difference affects your sigma classification!

---

## 9. Handling Special Cases

### Dividends

For **total return** (including dividends):

$$R_t = \ln\left(\frac{P_t + D_t}{P_{t-1}}\right)$$

Where $D_t$ = dividend on day $t$

### Stock Splits

Always use **adjusted prices** that account for splits, or your returns will show false extreme moves.

### Missing Data

Options:
1. Skip the gap (use previous available price)
2. Interpolate (less preferred)
3. Note the gap in analysis

---

## 10. Complete Workflow

```
Price Data → Adjusted for Splits/Dividends → Calculate Log Returns →
Compute Mean & Std Dev → Ready for Sigma Analysis
```

---

## Key Formulas Summary

| Formula | Expression |
|---------|------------|
| Simple Return | $R = \frac{P_t - P_{t-1}}{P_{t-1}}$ |
| Log Return | $R = \ln(P_t) - \ln(P_{t-1})$ |
| Mean Return | $\bar{R} = \frac{1}{n}\sum R_t$ |
| Annualized Mean | $\bar{R}_{annual} = \bar{R}_{daily} \times 252$ |
| Annualized Volatility | $\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$ |

---

## Next Steps

Continue to [[03-Standard-Deviation-Deep-Dive]] for advanced volatility concepts.

---

#returns #log-returns #simple-returns #volatility
