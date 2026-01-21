# Worked Examples

Complete step-by-step solutions to common sigma move problems. Work through these before attempting the exercise sets.

---

## Example 1: Basic Return Calculation

### Problem
Stock ABC closed at $150.00 yesterday and $156.75 today. Calculate:
a) Simple return
b) Log return

### Solution

**a) Simple Return:**
$$R_{simple} = \frac{P_t - P_{t-1}}{P_{t-1}} = \frac{156.75 - 150.00}{150.00} = \frac{6.75}{150.00} = 0.045 = 4.5\%$$

**b) Log Return:**
$$R_{log} = \ln\left(\frac{P_t}{P_{t-1}}\right) = \ln\left(\frac{156.75}{150.00}\right) = \ln(1.045) = 0.0440 = 4.40\%$$

**Verification:** $e^{0.0440} - 1 = 1.045 - 1 = 0.045$ ✓

---

## Example 2: Mean and Standard Deviation

### Problem
Calculate the mean and standard deviation for these daily returns (%):
1.2, -0.8, 0.5, -0.3, 1.8, -1.5, 0.9, 0.2, -0.6, 0.4

### Solution

**Step 1: Calculate Mean**
$$\bar{R} = \frac{1.2 - 0.8 + 0.5 - 0.3 + 1.8 - 1.5 + 0.9 + 0.2 - 0.6 + 0.4}{10} = \frac{1.8}{10} = 0.18\%$$

**Step 2: Calculate Deviations**

| Return | $R - \bar{R}$ | $(R - \bar{R})^2$ |
|--------|---------------|-------------------|
| 1.2    | 1.02          | 1.0404            |
| -0.8   | -0.98         | 0.9604            |
| 0.5    | 0.32          | 0.1024            |
| -0.3   | -0.48         | 0.2304            |
| 1.8    | 1.62          | 2.6244            |
| -1.5   | -1.68         | 2.8224            |
| 0.9    | 0.72          | 0.5184            |
| 0.2    | 0.02          | 0.0004            |
| -0.6   | -0.78         | 0.6084            |
| 0.4    | 0.22          | 0.0484            |
| **Sum** |              | **8.9560**        |

**Step 3: Calculate Variance and Standard Deviation**
$$s^2 = \frac{8.9560}{10-1} = \frac{8.9560}{9} = 0.9951$$

$$s = \sqrt{0.9951} = 0.998\% \approx 1.0\%$$

**Answer:** Mean = 0.18%, Standard Deviation = 1.0%

---

## Example 3: Basic Sigma Move Classification

### Problem
Using the statistics from Example 2 (μ = 0.18%, σ = 1.0%), classify these returns:
a) +0.5%
b) -2.3%
c) -4.5%

### Solution

**a) Return = +0.5%**
$$z = \frac{0.5 - 0.18}{1.0} = \frac{0.32}{1.0} = +0.32\sigma$$
**Classification: Normal** (within ±1σ)

**b) Return = -2.3%**
$$z = \frac{-2.3 - 0.18}{1.0} = \frac{-2.48}{1.0} = -2.48\sigma$$
**Classification: Significant** (between 2σ and 3σ)

**c) Return = -4.5%**
$$z = \frac{-4.5 - 0.18}{1.0} = \frac{-4.68}{1.0} = -4.68\sigma$$
**Classification: Rare** (between 4σ and 5σ)

---

## Example 4: Annualizing Volatility

### Problem
A stock has daily volatility of 1.5%. Calculate:
a) Weekly volatility
b) Monthly volatility (21 trading days)
c) Annual volatility

### Solution

**a) Weekly (5 days):**
$$\sigma_{weekly} = 1.5\% \times \sqrt{5} = 1.5\% \times 2.236 = 3.35\%$$

**b) Monthly (21 days):**
$$\sigma_{monthly} = 1.5\% \times \sqrt{21} = 1.5\% \times 4.583 = 6.87\%$$

**c) Annual (252 days):**
$$\sigma_{annual} = 1.5\% \times \sqrt{252} = 1.5\% \times 15.875 = 23.8\%$$

---

## Example 5: EWMA Volatility Update

### Problem
Given:
- Previous EWMA variance: 0.0001 (σ = 1.0%)
- Lambda (λ): 0.94
- Yesterday's return: -2.5%

Calculate the new EWMA volatility.

### Solution

**Step 1: Apply EWMA Formula**
$$\sigma_t^2 = \lambda \sigma_{t-1}^2 + (1-\lambda) R_{t-1}^2$$

$$\sigma_t^2 = 0.94 \times 0.0001 + 0.06 \times (-0.025)^2$$

$$\sigma_t^2 = 0.000094 + 0.06 \times 0.000625$$

$$\sigma_t^2 = 0.000094 + 0.0000375 = 0.0001315$$

**Step 2: Take Square Root**
$$\sigma_t = \sqrt{0.0001315} = 0.01147 = 1.15\%$$

**Answer:** New EWMA volatility = 1.15% (up from 1.0% due to the large move)

---

## Example 6: Probability of Sigma Move

### Problem
Under the normal distribution, what is the probability of:
a) A +3σ or greater move
b) A move exceeding ±2.5σ in either direction
c) At least one 3σ move in 252 trading days

### Solution

**a) P(Z > 3):**
Using standard normal table: $\Phi(3) = 0.99865$
$$P(Z > 3) = 1 - 0.99865 = 0.00135 = 0.135\%$$

**b) P(|Z| > 2.5):**
$$P(|Z| > 2.5) = 2 \times P(Z > 2.5) = 2 \times (1 - 0.9938) = 2 \times 0.0062 = 0.0124 = 1.24\%$$

**c) At least one 3σ in 252 days:**
Daily $P(|Z| > 3) = 0.0027$
$$P(\text{at least one}) = 1 - (1 - 0.0027)^{252} = 1 - 0.9973^{252}$$
$$= 1 - 0.505 = 0.495 = 49.5\%$$

---

## Example 7: Complete Daily Analysis

### Problem
You're tracking Stock XYZ. Historical data (past 20 days) gives:
- Mean return: 0.05%
- Standard deviation: 1.25%

Today's prices: Open $85.20, High $87.50, Low $82.00, Close $82.50

Yesterday's close: $86.00

Analyze today's move.

### Solution

**Step 1: Calculate Today's Return**
$$R = \ln\left(\frac{82.50}{86.00}\right) = \ln(0.9593) = -0.0416 = -4.16\%$$

**Step 2: Calculate Sigma Move**
$$z = \frac{-4.16 - 0.05}{1.25} = \frac{-4.21}{1.25} = -3.37\sigma$$

**Step 3: Classification**
This is a **3.37σ down move** - classified as **Extreme** (3-4σ range).

**Step 4: Probability Assessment**
Under normal distribution:
$$P(Z < -3.37) \approx 0.000375 = 0.0375\%$$
This should happen about 1 in 2,667 days, or roughly once per 10.6 years.

**Step 5: Additional Observations**
- Intraday range: High-Low = $87.50 - $82.00 = $5.50 (6.5% of low)
- Closed near daily low → selling pressure persisted
- Large range suggests high intraday volatility

---

## Example 8: Rolling Window Calculation

### Problem
Calculate the 5-day rolling mean and σ for days 5-7 using this data:

| Day | Return (%) |
|-----|------------|
| 1   | 0.8        |
| 2   | -0.5       |
| 3   | 1.2        |
| 4   | -0.3       |
| 5   | 0.6        |
| 6   | -1.4       |
| 7   | 0.9        |

### Solution

**Day 5 (Window: Days 1-5):**

Mean: $\frac{0.8 - 0.5 + 1.2 - 0.3 + 0.6}{5} = \frac{1.8}{5} = 0.36\%$

Deviations from 0.36:

| R | R - μ | (R - μ)² |
|---|-------|----------|
| 0.8 | 0.44 | 0.1936 |
| -0.5 | -0.86 | 0.7396 |
| 1.2 | 0.84 | 0.7056 |
| -0.3 | -0.66 | 0.4356 |
| 0.6 | 0.24 | 0.0576 |
| Sum | | 2.1320 |

$\sigma_5 = \sqrt{\frac{2.1320}{4}} = \sqrt{0.533} = 0.73\%$

**Day 6 (Window: Days 2-6):**

Mean: $\frac{-0.5 + 1.2 - 0.3 + 0.6 - 1.4}{5} = \frac{-0.4}{5} = -0.08\%$

| R | R - μ | (R - μ)² |
|---|-------|----------|
| -0.5 | -0.42 | 0.1764 |
| 1.2 | 1.28 | 1.6384 |
| -0.3 | -0.22 | 0.0484 |
| 0.6 | 0.68 | 0.4624 |
| -1.4 | -1.32 | 1.7424 |
| Sum | | 4.0680 |

$\sigma_6 = \sqrt{\frac{4.0680}{4}} = \sqrt{1.017} = 1.01\%$

**Day 7 (Window: Days 3-7):**

Mean: $\frac{1.2 - 0.3 + 0.6 - 1.4 + 0.9}{5} = \frac{1.0}{5} = 0.20\%$

| R | R - μ | (R - μ)² |
|---|-------|----------|
| 1.2 | 1.00 | 1.0000 |
| -0.3 | -0.50 | 0.2500 |
| 0.6 | 0.40 | 0.1600 |
| -1.4 | -1.60 | 2.5600 |
| 0.9 | 0.70 | 0.4900 |
| Sum | | 4.4600 |

$\sigma_7 = \sqrt{\frac{4.4600}{4}} = \sqrt{1.115} = 1.06\%$

**Summary Table:**

| Day | Rolling μ | Rolling σ |
|-----|-----------|-----------|
| 5   | 0.36%     | 0.73%     |
| 6   | -0.08%    | 1.01%     |
| 7   | 0.20%     | 1.06%     |

---

## Example 9: Parkinson Volatility

### Problem
Calculate Parkinson volatility using this OHLC data:

| Day | High | Low |
|-----|------|-----|
| 1   | 102  | 98  |
| 2   | 104  | 100 |
| 3   | 103  | 99  |
| 4   | 106  | 101 |
| 5   | 105  | 102 |

### Solution

**Step 1: Calculate ln(H/L) for each day**

| Day | H | L | H/L | ln(H/L) | [ln(H/L)]² |
|-----|---|---|-----|---------|------------|
| 1 | 102 | 98 | 1.0408 | 0.0400 | 0.001600 |
| 2 | 104 | 100 | 1.0400 | 0.0392 | 0.001537 |
| 3 | 103 | 99 | 1.0404 | 0.0396 | 0.001568 |
| 4 | 106 | 101 | 1.0495 | 0.0483 | 0.002333 |
| 5 | 105 | 102 | 1.0294 | 0.0290 | 0.000841 |
| **Avg** | | | | | **0.001576** |

**Step 2: Apply Parkinson Formula**
$$\sigma_P = \sqrt{\frac{0.001576}{4 \times \ln(2)}} = \sqrt{\frac{0.001576}{2.773}} = \sqrt{0.000568} = 0.0238 = 2.38\%$$

**Answer:** Parkinson daily volatility = 2.38%

---

## Example 10: Multi-Asset Sigma Dashboard

### Problem
Create a sigma move dashboard for these stocks given today's returns and 60-day statistics:

| Stock | Return | 60-Day Mean | 60-Day σ |
|-------|--------|-------------|----------|
| AAPL  | -1.8%  | 0.06%       | 1.4%     |
| MSFT  | -2.1%  | 0.04%       | 1.3%     |
| GOOGL | +0.5%  | 0.05%       | 1.6%     |
| TSLA  | -5.2%  | 0.08%       | 2.8%     |
| SPY   | -1.2%  | 0.03%       | 0.9%     |

### Solution

**Calculate z-scores:**

AAPL: $z = \frac{-1.8 - 0.06}{1.4} = \frac{-1.86}{1.4} = -1.33\sigma$

MSFT: $z = \frac{-2.1 - 0.04}{1.3} = \frac{-2.14}{1.3} = -1.65\sigma$

GOOGL: $z = \frac{0.5 - 0.05}{1.6} = \frac{0.45}{1.6} = +0.28\sigma$

TSLA: $z = \frac{-5.2 - 0.08}{2.8} = \frac{-5.28}{2.8} = -1.89\sigma$

SPY: $z = \frac{-1.2 - 0.03}{0.9} = \frac{-1.23}{0.9} = -1.37\sigma$

**Dashboard:**

| Stock | Return | Sigma Move | Classification |
|-------|--------|------------|----------------|
| AAPL  | -1.8%  | -1.33σ     | Elevated       |
| MSFT  | -2.1%  | -1.65σ     | Elevated       |
| GOOGL | +0.5%  | +0.28σ     | Normal         |
| TSLA  | -5.2%  | -1.89σ     | Elevated       |
| SPY   | -1.2%  | -1.37σ     | Elevated       |

**Analysis:**
- All stocks except GOOGL are down
- All moves are within 2σ - significant but not extreme
- MSFT has the largest sigma move despite TSLA having largest absolute move (because TSLA has higher normal volatility)
- Correlated selling across tech sector suggests market-wide factor

---

## Practice Tips

1. **Always show your work** - Write out each step
2. **Check units** - Returns in % or decimals?
3. **Verify reasonableness** - Does the answer make sense?
4. **Use the formula sheet** - Don't memorize, understand
5. **Start simple** - Master basic calculations before advanced

---

## Next Steps

Now try the exercises:
- [[exercises/Exercise-Set-01-Basic-Statistics]]
- [[exercises/Exercise-Set-02-Returns-Calculation]]
- [[exercises/Exercise-Set-03-Standard-Deviation]]
- [[exercises/Exercise-Set-04-Sigma-Classification]]
- [[exercises/Exercise-Set-05-Volatility-Analysis]]
- [[exercises/Exercise-Set-06-Comprehensive-Problems]]

---

#examples #practice #step-by-step
