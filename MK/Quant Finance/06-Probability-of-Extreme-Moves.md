# Probability of Extreme Moves

Understanding the mathematics behind extreme event probabilities is essential for interpreting sigma moves correctly.

---

## 1. The Normal Distribution Assumption

### Probability Density Function

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

### Cumulative Distribution Function

$$\Phi(z) = P(Z \leq z) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{z} e^{-t^2/2} dt$$

This integral has no closed form - we use tables or numerical methods.

---

## 2. Calculating Tail Probabilities

### One-Tailed Probability (Exceeding z)

$$P(Z > z) = 1 - \Phi(z)$$

### Two-Tailed Probability (Exceeding |z|)

$$P(|Z| > z) = 2 \times P(Z > z) = 2(1 - \Phi(z))$$

---

## 3. Complete Probability Table

### Standard Normal Probabilities

| z | Φ(z) | P(Z > z) | P(\|Z\| > z) | 1 in X days |
|---|------|----------|--------------|-------------|
| 0.5 | 0.6915 | 0.3085 | 0.6171 | 1.6 |
| 1.0 | 0.8413 | 0.1587 | 0.3173 | 3.2 |
| 1.5 | 0.9332 | 0.0668 | 0.1336 | 7.5 |
| 2.0 | 0.9772 | 0.0228 | 0.0455 | 22 |
| 2.5 | 0.9938 | 0.0062 | 0.0124 | 81 |
| 3.0 | 0.99865 | 0.00135 | 0.0027 | 370 |
| 3.5 | 0.99977 | 0.00023 | 0.00047 | 2,128 |
| 4.0 | 0.999968 | 0.000032 | 0.000063 | 15,787 |
| 4.5 | 0.9999966 | 0.0000034 | 0.0000068 | 147,059 |
| 5.0 | 0.99999971 | 0.00000029 | 0.00000057 | 1,744,278 |
| 6.0 | 0.999999999 | 1.0×10⁻⁹ | 2.0×10⁻⁹ | 506,797,346 |

### Conversion to Trading Days

With ~252 trading days per year:

| Sigma | Expected Frequency (Two-Tailed) |
|-------|--------------------------------|
| 1σ    | 80 times per year |
| 2σ    | 11 times per year |
| 3σ    | Once per 1.5 years |
| 4σ    | Once per 63 years |
| 5σ    | Once per 6,922 years |
| 6σ    | Once per 2 million years |
| 7σ    | Once per 780 million years |

---

## 4. Approximating Tail Probabilities

### For Large z (Mills Ratio Approximation)

For $z > 3$:

$$P(Z > z) \approx \frac{\phi(z)}{z} = \frac{e^{-z^2/2}}{z\sqrt{2\pi}}$$

### Example: Calculating P(Z > 4)

$$P(Z > 4) \approx \frac{e^{-16/2}}{4\sqrt{2\pi}} = \frac{e^{-8}}{10.027} = \frac{0.000335}{10.027} = 0.0000334$$

More exact value: 0.0000317

### Quick Mental Estimates

| Sigma | Quick Estimate |
|-------|----------------|
| 3σ | ~1 in 370 |
| 4σ | ~1 in 16,000 |
| 5σ | ~1 in 1.7 million |
| 6σ | ~1 in 500 million |

Rule of thumb: Each additional sigma multiplies rarity by ~10-100x.

---

## 5. The Probability Integral

### Computing Φ(z) by Hand

For moderate z, use polynomial approximation:

$$\Phi(z) \approx 1 - \phi(z)(b_1t + b_2t^2 + b_3t^3 + b_4t^4 + b_5t^5)$$

Where:
- $t = \frac{1}{1 + 0.2316419z}$
- $\phi(z) = \frac{1}{\sqrt{2\pi}}e^{-z^2/2}$
- $b_1 = 0.319381530$
- $b_2 = -0.356563782$
- $b_3 = 1.781477937$
- $b_4 = -1.821255978$
- $b_5 = 1.330274429$

This gives accuracy to about 7 decimal places.

---

## 6. From Z-Score to Probability: Worked Examples

### Example 1: What's the probability of a 2.5σ move?

**Two-tailed (either direction):**
$$P(|Z| > 2.5) = 2 \times P(Z > 2.5) = 2 \times 0.0062 = 0.0124 = 1.24\%$$

**Expected frequency:** Once every 81 trading days, or about 3 times per year.

### Example 2: Probability of 3σ down move?

**One-tailed (down only):**
$$P(Z < -3) = P(Z > 3) = 0.00135 = 0.135\%$$

**Expected frequency:** Once every 741 trading days, or about once per 3 years.

### Example 3: Probability of 4σ up move?

**One-tailed (up only):**
$$P(Z > 4) = 0.0000317 = 0.00317\%$$

**Expected frequency:** Once every 31,546 trading days, or about once per 125 years.

---

## 7. Cumulative Probability Charts

### Visualizing the Distribution

```
                    Normal Distribution
                         _____
                       /       \
                      /         \
                     /           \
                    /             \
                   /               \
                  /                 \
         ______/                     \______
    -4σ  -3σ  -2σ  -1σ   0   +1σ  +2σ  +3σ  +4σ

Area under curve:
  ±1σ: 68.27%
  ±2σ: 95.45%
  ±3σ: 99.73%
  ±4σ: 99.9937%
```

### Tail Area Representation

```
P(Z > 3) = 0.135%

                         _____
                       /       \
                      /         \
                     /           \
                    /             \
                   /               \
                  /                 ■ ← This tiny area
         ______/                     \______
                              +3σ
```

---

## 8. Converting Between Representations

### From Probability to Z-Score

If you know the probability, find the corresponding z:

$$z = \Phi^{-1}(1 - p)$$ for one-tailed

### Common Probability ↔ Z Conversions

| Probability (one-tail) | Z-Score |
|------------------------|---------|
| 10% | 1.282 |
| 5% | 1.645 |
| 2.5% | 1.960 |
| 1% | 2.326 |
| 0.5% | 2.576 |
| 0.1% | 3.090 |
| 0.01% | 3.719 |

### VaR Levels

| Confidence | Z | VaR Calculation |
|------------|---|-----------------|
| 95% | 1.645 | VaR = μ + 1.645σ |
| 99% | 2.326 | VaR = μ + 2.326σ |
| 99.9% | 3.090 | VaR = μ + 3.090σ |

---

## 9. Time Scaling Probabilities

### Daily to Longer Periods

If daily probability of exceeding threshold is $p$:

**Probability of at least one event in n days:**
$$P(\text{at least one}) = 1 - (1-p)^n$$

### Example: 3σ Move in a Year

Daily $P(|Z| > 3) = 0.0027$

Probability of at least one 3σ move in 252 days:
$$P = 1 - (1-0.0027)^{252} = 1 - 0.9973^{252} = 1 - 0.505 = 49.5\%$$

So there's about a 50% chance of seeing a 3σ move in any given year (under normal distribution).

### Summary for Different Sigmas

| Sigma | P(≥1 event/year) under Normal |
|-------|-------------------------------|
| 2σ | 99.99% (essentially certain) |
| 3σ | 49.5% |
| 4σ | 1.6% |
| 5σ | 0.014% |

---

## 10. The Cumulative Nature of Small Probabilities

### Many Small Probabilities Add Up

If you track 100 stocks, each with daily 3σ probability of 0.27%:

Expected 3σ moves per day across portfolio:
$$100 \times 0.0027 = 0.27$$ moves/day

Or about **68 moves per year** somewhere in your portfolio!

### Independence Assumption

This assumes moves are independent. In reality:
- Market-wide events create correlated moves
- During crises, many stocks have extreme moves simultaneously
- Correlation ≈ 1 in tail events

---

## 11. Practical Application: Building a Probability Calculator

### The Algorithm

```
INPUT: z-score (sigma move)

CALCULATE:
  1. p_one_tail = 1 - Φ(|z|)
  2. p_two_tail = 2 × p_one_tail
  3. frequency = 1 / p_two_tail (in days)
  4. years = frequency / 252

OUTPUT:
  - One-tailed probability
  - Two-tailed probability
  - Expected frequency in days
  - Expected frequency in years
```

### Example Calculator Use

**Input:** z = 3.5

**Output:**
- One-tail: 0.0233%
- Two-tail: 0.0465%
- Frequency: 1 in 2,151 days
- Years: 1 in 8.5 years

---

## 12. Important Limitations

### Normal Distribution Underestimates Extremes

The theoretical probabilities assume perfect normality. Real markets show:

| Event | Normal Prediction | Actual Observation |
|-------|-------------------|-------------------|
| 3σ days/year | ~1 | 5-10 |
| 4σ days/year | 1/63 years | 1-2 |
| 5σ events | 1/7000 years | Every few years |

### Why This Matters

- Don't be surprised by "impossible" events
- Use normal probabilities as rough guides only
- Consider fat-tailed distributions for risk management

---

## Key Formulas

| Calculation | Formula |
|-------------|---------|
| One-tail probability | $P(Z > z) = 1 - \Phi(z)$ |
| Two-tail probability | $P(\|Z\| > z) = 2(1 - \Phi(z))$ |
| Expected frequency | $f = 1/p$ days |
| At least one in n days | $P = 1 - (1-p)^n$ |

---

## Next Steps

Continue to [[07-Fat-Tails-and-Reality]] to understand why real markets deviate from normal.

---

#probability #normal-distribution #tail-events #statistics
