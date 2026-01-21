# Fat Tails and Market Reality

The normal distribution is a convenient assumption, but real market returns exhibit characteristics that make extreme events far more common than theory predicts.

---

## 1. What Are Fat Tails?

### Definition

**Fat tails** (or **heavy tails**) mean that extreme events occur more frequently than a normal distribution predicts.

### Visual Comparison

```
Normal Distribution:
     _____
    /     \
   /       \          Thin tails: drops off rapidly
  /         \
_/           \_______

Fat-Tailed Distribution:
     ___
    /   \
   /     \            Fat tails: elevated probability
  /       \           at extremes
_/         \__________
```

### Quantifying Fat Tails: Kurtosis

**Kurtosis** measures tail thickness:

$$\text{Kurtosis} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^4$$

**Excess Kurtosis** = Kurtosis - 3

| Excess Kurtosis | Interpretation |
|-----------------|----------------|
| = 0 | Normal tails (mesokurtic) |
| > 0 | Fat tails (leptokurtic) |
| < 0 | Thin tails (platykurtic) |

**Stock returns typically have excess kurtosis of 3-10+**

---

## 2. Evidence of Fat Tails in Markets

### Historical Examples of "Impossible" Events

| Event | Date | S&P 500 Move | Sigma | Normal Probability |
|-------|------|--------------|-------|-------------------|
| Black Monday | Oct 19, 1987 | -20.5% | ~22σ | 1 in 10^150 years |
| Flash Crash | May 6, 2010 | -6% intraday | ~6σ | 1 in 2M years |
| COVID Crash | Mar 16, 2020 | -12% | ~12σ | 1 in 10^30 years |
| Swiss Franc | Jan 15, 2015 | +30% (EURCHF) | ~40σ | Effectively impossible |

These events happen, yet normal distribution says they shouldn't exist!

### Empirical Frequency vs Normal Prediction

| Sigma Level | Normal Prediction | Actual Observation |
|-------------|------------------|-------------------|
| 3σ | 1/year | 5-10/year |
| 4σ | 1/63 years | 1-2/year |
| 5σ | 1/7000 years | Every few years |
| 6σ | 1/500K years | ~Once per decade |
| 10σ+ | Never | Has happened multiple times |

---

## 3. Why Markets Have Fat Tails

### Structural Reasons

1. **Leverage**: Magnifies moves
2. **Stop losses**: Create cascades
3. **Margin calls**: Forced selling
4. **Herding**: Everyone exits simultaneously
5. **Liquidity withdrawal**: Market makers step back
6. **Feedback loops**: Price moves cause more price moves

### Behavioral Reasons

1. **Fear and panic**: Emotional selling
2. **FOMO**: Emotional buying
3. **Anchoring**: Delayed response then overreaction
4. **Information cascades**: Following others blindly

### Mathematical Reasons

1. **Volatility clustering**: High vol follows high vol
2. **Regime changes**: Market dynamics shift
3. **Non-stationarity**: Distribution parameters change over time

---

## 4. Alternative Distributions

### Student's t-Distribution

Better fits market returns than normal:

$$f(x) = \frac{\Gamma\left(\frac{\nu+1}{2}\right)}{\sqrt{\nu\pi}\Gamma\left(\frac{\nu}{2}\right)}\left(1+\frac{x^2}{\nu}\right)^{-\frac{\nu+1}{2}}$$

Where ν (nu) = degrees of freedom

| ν | Tail Behavior |
|---|---------------|
| ν → ∞ | Approaches normal |
| ν = 30 | Slightly fatter than normal |
| ν = 5 | Noticeably fat |
| ν = 3 | Very fat tails |

**Stock returns often fit t-distribution with ν ≈ 4-6**

### t-Distribution vs Normal: Tail Probabilities

| Sigma | Normal P(Z > z) | t(ν=5) P(T > t) | Ratio |
|-------|-----------------|-----------------|-------|
| 3 | 0.135% | 0.73% | 5.4x |
| 4 | 0.0032% | 0.12% | 37x |
| 5 | 0.000029% | 0.027% | 931x |

### Power Law Distributions

Extreme events follow:

$$P(X > x) \propto x^{-\alpha}$$

Where α ≈ 3 for stock returns (Pareto exponent)

---

## 5. Quantifying Tail Risk

### Expected Shortfall (CVaR)

Average loss given that loss exceeds VaR:

$$ES_\alpha = E[X | X < VaR_\alpha]$$

### Tail Index Estimation (Hill Estimator)

$$\hat{\alpha} = \left(\frac{1}{k}\sum_{i=1}^{k}\ln\frac{X_{(i)}}{X_{(k)}}\right)^{-1}$$

Where $X_{(i)}$ are the k largest observations.

### Practical Measures

| Measure | Description |
|---------|-------------|
| VaR | Maximum loss at confidence level |
| CVaR/ES | Average of losses beyond VaR |
| Tail ratio | Observed vs expected extreme events |
| Maximum drawdown | Largest peak-to-trough decline |

---

## 6. Adjusting Sigma Analysis for Fat Tails

### Option 1: Use Higher Effective Sigma

When markets have fat tails, treat observed moves as larger:

| Observed Normal σ | Effective "True" σ |
|-------------------|-------------------|
| 3σ | ~2.5σ in fat-tailed |
| 4σ | ~3σ in fat-tailed |
| 5σ | ~3.5σ in fat-tailed |

### Option 2: Apply a Tail Multiplier

Adjust probabilities:

$$P_{adjusted} = P_{normal} \times k$$

Where k = tail inflation factor (typically 3-10 for extreme events)

### Option 3: Use t-Distribution

Calculate z-scores but look up probabilities in t-distribution table.

---

## 7. Practical Implications

### For Risk Management

1. **Don't trust normal VaR**: Use fat-tailed VaR or CVaR
2. **Stress testing**: Simulate larger moves than "expected"
3. **Position sizing**: Account for possibility of 10σ+ moves
4. **Stop losses**: May not execute at intended price in crashes

### For Sigma Classification

| Classification | Under Normal | Under Fat Tails |
|----------------|--------------|-----------------|
| "Rare" (4σ) | 1/63 years | Several per year |
| "Very Rare" (5σ) | 1/7000 years | Every few years |
| "Impossible" (6σ+) | Never | Has happened |

### Adjusted Interpretation Guide

| Observed Sigma | Practical Classification |
|----------------|-------------------------|
| 1-2σ | Normal variation |
| 2-3σ | Notable but common |
| 3-4σ | Significant event |
| 4-5σ | Major event (but not truly rare) |
| 5-6σ | Crisis-level |
| 6σ+ | Black swan / tail event |

---

## 8. Measuring Fat Tails in Your Data

### Step 1: Calculate Excess Kurtosis

$$\text{Excess Kurtosis} = \frac{\frac{1}{n}\sum(x_i - \bar{x})^4}{s^4} - 3$$

### Step 2: Count Tail Events

Compare actual vs expected:

```
Observed 3σ+ events: X
Expected under normal: 252 × 0.0027 = 0.68/year

Tail Ratio = X / 0.68
```

### Step 3: Visual Check (Q-Q Plot)

Plot sample quantiles against theoretical normal quantiles.
- If linear: normal distribution fits
- If curved at ends: fat tails present

### Example Kurtosis Calculation

Returns: -3.5%, 0.2%, 1.1%, -0.8%, -2.1%, 4.2%, -0.3%, 0.5%, -1.2%, 0.8%

Mean = -0.11%, Std Dev = 2.02%

| Return | $(R-\bar{R})/s$ | $z^4$ |
|--------|-----------------|-------|
| -3.5% | -1.68 | 7.96 |
| 0.2% | 0.15 | 0.0005 |
| 1.1% | 0.60 | 0.13 |
| -0.8% | -0.34 | 0.013 |
| -2.1% | -0.99 | 0.96 |
| 4.2% | 2.13 | 20.6 |
| -0.3% | -0.09 | 0.00007 |
| 0.5% | 0.30 | 0.008 |
| -1.2% | -0.54 | 0.085 |
| 0.8% | 0.45 | 0.041 |
| **Sum** | | **29.8** |

Kurtosis = 29.8 / 10 = 2.98
Excess Kurtosis = 2.98 - 3 = -0.02 ≈ 0

(Small sample - larger samples would show fat tails more clearly)

---

## 9. The Taleb Perspective

Nassim Taleb's key insights on fat tails:

### "Black Swans"

- Extreme events dominate returns
- Cannot be predicted from historical data
- Normal distribution is "intellectual fraud" for risk

### Key Quotes

> "The normal distribution is perhaps the most dangerous assumption in finance."

> "In the real world, 6 sigma events happen every few years."

### Practical Advice

1. Assume extreme events will happen
2. Position for asymmetric outcomes
3. Don't bet the house on "impossible" events not occurring

---

## 10. Summary: Adjusted Framework

### The Reality-Adjusted Sigma Scale

| Sigma | Normal Says | Reality Says |
|-------|-------------|--------------|
| 1σ | Common | Common |
| 2σ | Occasional | Common |
| 3σ | Rare | Occasional |
| 4σ | Very Rare | Uncommon |
| 5σ | Almost Never | Rare |
| 6σ | Impossible | Very Rare |
| 10σ | Beyond Impossible | Has Happened |

### Key Takeaways

1. **Normal distribution underestimates extremes** by orders of magnitude
2. **Fat tails are the norm** in financial markets
3. **Adjust your expectations** - "rare" events happen regularly
4. **Use sigma as relative measure**, not absolute probability
5. **Risk management must account** for fat tails

---

## Next Steps

Continue to [[08-Rolling-Window-Analysis]] for dynamic volatility measurement.

---

#fat-tails #kurtosis #risk #black-swan #tail-risk
