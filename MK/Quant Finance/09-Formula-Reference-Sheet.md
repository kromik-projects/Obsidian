# Formula Reference Sheet

Quick reference for all key formulas in sigma move analysis.

---

## Returns

### Simple Return
$$R_t = \frac{P_t - P_{t-1}}{P_{t-1}} = \frac{P_t}{P_{t-1}} - 1$$

### Log Return (Preferred)
$$R_t = \ln\left(\frac{P_t}{P_{t-1}}\right) = \ln(P_t) - \ln(P_{t-1})$$

### Conversion
$$R_{log} = \ln(1 + R_{simple})$$
$$R_{simple} = e^{R_{log}} - 1$$

---

## Central Tendency

### Sample Mean
$$\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$$

### Population Mean
$$\mu = \frac{1}{N}\sum_{i=1}^{N} x_i$$

---

## Dispersion

### Sample Variance
$$s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2$$

### Computational Variance
$$s^2 = \frac{\sum x_i^2 - n\bar{x}^2}{n-1}$$

### Sample Standard Deviation
$$s = \sqrt{s^2} = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2}$$

### Population Standard Deviation
$$\sigma = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(x_i - \mu)^2}$$

---

## Sigma Moves (Z-Score)

### Z-Score Formula
$$z = \frac{x - \mu}{\sigma} = \frac{R_t - \bar{R}}{s}$$

### Simplified (Mean ≈ 0)
$$z \approx \frac{R_t}{s}$$

---

## Annualization

### Annualized Mean Return
$$\bar{R}_{annual} = \bar{R}_{daily} \times 252$$

### Annualized Volatility
$$\sigma_{annual} = \sigma_{daily} \times \sqrt{252}$$

### General Time Scaling
$$\sigma_T = \sigma_t \times \sqrt{\frac{T}{t}}$$

### Scaling Factors

| From Daily To | Multiply by |
|---------------|-------------|
| Weekly | √5 = 2.236 |
| Monthly | √21 = 4.583 |
| Quarterly | √63 = 7.937 |
| Annual | √252 = 15.875 |

---

## Volatility Estimators

### EWMA
$$\sigma_t^2 = \lambda \sigma_{t-1}^2 + (1-\lambda) R_{t-1}^2$$

Standard λ = 0.94

### GARCH(1,1)
$$\sigma_t^2 = \omega + \alpha R_{t-1}^2 + \beta \sigma_{t-1}^2$$

### Parkinson (Range-Based)
$$\sigma_P = \sqrt{\frac{1}{4\ln(2)n}\sum_{t=1}^{n}[\ln(H_t/L_t)]^2}$$

Simplified: $\sigma_P \approx 0.601 \times \text{Avg}[\ln(H/L)]$

### Garman-Klass
$$\sigma_{GK}^2 = \frac{1}{n}\sum\left[0.5(\ln H - \ln L)^2 - 0.386(\ln C - \ln O)^2\right]$$

---

## Probability (Normal Distribution)

### Standard Normal PDF
$$\phi(z) = \frac{1}{\sqrt{2\pi}}e^{-z^2/2}$$

### Cumulative Distribution
$$\Phi(z) = P(Z \leq z) = \int_{-\infty}^{z} \phi(t)dt$$

### Tail Probabilities
$$P(Z > z) = 1 - \Phi(z)$$
$$P(|Z| > z) = 2(1 - \Phi(z))$$

### Mills Ratio (Large z Approximation)
$$P(Z > z) \approx \frac{\phi(z)}{z} = \frac{e^{-z^2/2}}{z\sqrt{2\pi}}$$

---

## Higher Moments

### Skewness
$$\text{Skew} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^3$$

### Kurtosis
$$\text{Kurt} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^4$$

### Excess Kurtosis
$$\text{Excess Kurt} = \text{Kurt} - 3$$

---

## Rolling Windows

### Rolling Mean
$$\bar{R}_t^{(w)} = \frac{1}{w}\sum_{i=t-w+1}^{t} R_i$$

### Rolling Variance
$$s_t^2 = \frac{\sum_{i=t-w+1}^{t} R_i^2 - w(\bar{R}_t)^2}{w-1}$$

### Rolling Update
$$\bar{R}_{t+1} = \bar{R}_t + \frac{R_{t+1} - R_{t-w+1}}{w}$$

---

## Quick Reference Tables

### Sigma Move Probabilities (Normal)

| σ | P(one-tail) | P(two-tail) | ~1 in X days |
|---|-------------|-------------|--------------|
| 1 | 15.87% | 31.73% | 3 |
| 2 | 2.28% | 4.55% | 22 |
| 3 | 0.135% | 0.27% | 370 |
| 4 | 0.0032% | 0.0063% | 15,800 |
| 5 | 0.000029% | 0.000057% | 1.75M |

### Common Z-Values

| Confidence | Z |
|------------|---|
| 90% | 1.645 |
| 95% | 1.960 |
| 99% | 2.576 |
| 99.5% | 2.807 |
| 99.9% | 3.291 |

### Typical Volatility Ranges

| Asset Type | Daily σ | Annual σ |
|------------|---------|----------|
| Large-cap | 1-2% | 15-30% |
| Small-cap | 2-4% | 30-60% |
| Index | 0.8-1.2% | 12-20% |
| Bonds | 0.2-0.5% | 3-8% |

---

## Calculation Workflow

```
1. Prices → Log Returns
   R_t = ln(P_t/P_{t-1})

2. Returns → Mean
   μ = (1/n)ΣR_t

3. Returns + Mean → Variance
   s² = Σ(R-μ)²/(n-1)

4. Variance → Std Dev
   s = √s²

5. Current Return + Stats → Sigma
   z = (R_today - μ)/s

6. Classify sigma level
```

---

## Symbols Reference

| Symbol | Meaning |
|--------|---------|
| $P_t$ | Price at time t |
| $R_t$ | Return at time t |
| $\mu$ | Population mean |
| $\bar{x}$, $\bar{R}$ | Sample mean |
| $\sigma$ | Population std dev |
| $s$ | Sample std dev |
| $z$ | Z-score (sigma move) |
| $n$ | Sample size |
| $N$ | Population size |
| $w$ | Window size |
| $\lambda$ | EWMA decay factor |
| $\Phi$ | Normal CDF |
| $\phi$ | Normal PDF |

---

#reference #formulas #cheat-sheet
