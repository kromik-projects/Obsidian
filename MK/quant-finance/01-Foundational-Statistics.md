# Foundational Statistics for Quant Finance

Understanding sigma moves requires a solid foundation in statistics. This document covers the essential concepts you need.

---

## 1. Population vs Sample

### Population
The **complete set** of all possible observations.
- Example: ALL daily returns of Apple stock since its IPO

### Sample
A **subset** of the population that we actually observe.
- Example: Daily returns of Apple stock for the past year (252 trading days)

> **Key Point**: In finance, we almost always work with samples because we can't observe future returns.

---

## 2. Measures of Central Tendency

### Arithmetic Mean (Average)

The sum of all values divided by the number of values.

**Population Mean:**
$$\mu = \frac{1}{N}\sum_{i=1}^{N} x_i$$

**Sample Mean:**
$$\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$$

Where:
- $N$ = population size
- $n$ = sample size
- $x_i$ = individual observation

#### Example Calculation

Daily returns (in %): 1.2, -0.5, 0.8, -0.3, 0.4

$$\bar{x} = \frac{1.2 + (-0.5) + 0.8 + (-0.3) + 0.4}{5} = \frac{1.6}{5} = 0.32\%$$

### Median

The middle value when data is sorted.
- For odd $n$: middle value
- For even $n$: average of two middle values

#### Example
Sorted returns: -0.5, -0.3, 0.4, 0.8, 1.2

Median = 0.4% (the 3rd value out of 5)

### Mode

The most frequently occurring value. Less useful for continuous data like returns.

---

## 3. Measures of Dispersion

### Range

$$\text{Range} = x_{max} - x_{min}$$

Simple but ignores distribution of values between extremes.

### Variance

The average of squared deviations from the mean.

**Population Variance:**
$$\sigma^2 = \frac{1}{N}\sum_{i=1}^{N}(x_i - \mu)^2$$

**Sample Variance:**
$$s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2$$

> **Why n-1?** This is called **Bessel's correction**. It corrects for the bias in estimating population variance from a sample. Using $n$ would systematically underestimate the true variance.

#### Step-by-Step Variance Calculation

Data: 1.2, -0.5, 0.8, -0.3, 0.4 (returns in %)
Mean: 0.32%

| $x_i$ | $x_i - \bar{x}$ | $(x_i - \bar{x})^2$ |
|-------|-----------------|---------------------|
| 1.2   | 0.88            | 0.7744              |
| -0.5  | -0.82           | 0.6724              |
| 0.8   | 0.48            | 0.2304              |
| -0.3  | -0.62           | 0.3844              |
| 0.4   | 0.08            | 0.0064              |
| **Sum** |               | **2.0680**          |

$$s^2 = \frac{2.0680}{5-1} = \frac{2.0680}{4} = 0.517\%^2$$

### Standard Deviation

The square root of variance. Returns to original units.

**Population Standard Deviation:**
$$\sigma = \sqrt{\sigma^2} = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(x_i - \mu)^2}$$

**Sample Standard Deviation:**
$$s = \sqrt{s^2} = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2}$$

#### Continuing Our Example

$$s = \sqrt{0.517} = 0.719\%$$

This means daily returns typically deviate about 0.72% from the average.

---

## 4. The Normal Distribution

### Definition

The **normal distribution** (Gaussian distribution) is a symmetric, bell-shaped probability distribution completely described by two parameters:
- Mean ($\mu$): center of the distribution
- Standard deviation ($\sigma$): spread of the distribution

### Probability Density Function (PDF)

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$

### Key Properties

1. **Symmetric** around the mean
2. **Mean = Median = Mode**
3. **68-95-99.7 Rule**:
   - 68.27% of data within ±1σ
   - 95.45% of data within ±2σ
   - 99.73% of data within ±3σ

### Standard Normal Distribution

When $\mu = 0$ and $\sigma = 1$, we have the **standard normal distribution**.

Any normal variable can be converted to standard normal using:

$$z = \frac{x - \mu}{\sigma}$$

This $z$ is called the **z-score** or **standard score** - this is exactly what we use to measure sigma moves!

---

## 5. Z-Scores (The Foundation of Sigma Moves)

### Definition

The z-score tells us how many standard deviations an observation is from the mean.

$$z = \frac{x - \mu}{\sigma}$$

### Interpretation

| Z-Score | Meaning |
|---------|---------|
| z = 0   | Exactly at the mean |
| z = 1   | One σ above the mean |
| z = -1  | One σ below the mean |
| z = 2   | Two σ above the mean |
| z = -3  | Three σ below the mean |

### Example

Stock XYZ has:
- Mean daily return: 0.05%
- Standard deviation: 1.5%
- Today's return: -4.55%

$$z = \frac{-4.55 - 0.05}{1.5} = \frac{-4.60}{1.5} = -3.07$$

This is a **3-sigma down move** (more precisely, -3.07σ).

---

## 6. Probability from Z-Scores

### Z-Score Table (Selected Values)

| z    | P(Z ≤ z) | P(Z > z) | P(\|Z\| > z) |
|------|----------|----------|--------------|
| 0.00 | 0.5000   | 0.5000   | 1.0000       |
| 1.00 | 0.8413   | 0.1587   | 0.3173       |
| 1.96 | 0.9750   | 0.0250   | 0.0500       |
| 2.00 | 0.9772   | 0.0228   | 0.0455       |
| 2.58 | 0.9951   | 0.0049   | 0.0099       |
| 3.00 | 0.9987   | 0.0013   | 0.0027       |
| 4.00 | 0.99997  | 0.00003  | 0.00006      |
| 5.00 | 0.9999997| 0.0000003| 0.0000006    |

Where:
- P(Z ≤ z) = Cumulative probability up to z
- P(Z > z) = Probability of exceeding z (one tail)
- P(|Z| > z) = Probability of exceeding z in either direction (two tails)

---

## 7. Skewness and Kurtosis

### Skewness

Measures asymmetry of the distribution.

$$\text{Skewness} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^3$$

| Value | Interpretation |
|-------|----------------|
| = 0   | Symmetric |
| > 0   | Right-skewed (long right tail) |
| < 0   | Left-skewed (long left tail) |

> **Market Reality**: Stock returns often show **negative skewness** - crashes are more severe than rallies.

### Kurtosis

Measures "tailedness" - how extreme the tails are.

$$\text{Kurtosis} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^4$$

**Excess Kurtosis** = Kurtosis - 3

| Excess Kurtosis | Name | Interpretation |
|-----------------|------|----------------|
| = 0 | Mesokurtic | Normal tails |
| > 0 | Leptokurtic | Fat tails (more extreme events) |
| < 0 | Platykurtic | Thin tails (fewer extreme events) |

> **Market Reality**: Stock returns typically have **positive excess kurtosis** (fat tails) - extreme moves happen more often than normal distribution predicts!

---

## 8. Summary: What This Means for Sigma Moves

1. **Z-scores are sigma moves**: When we say "3-sigma move," we mean z = 3
2. **Normal distribution underestimates extremes**: Real markets have fat tails
3. **Standard deviation is key**: Accurate σ estimation is crucial for meaningful sigma classification
4. **Sample vs population matters**: Always be aware you're estimating from historical data

---

## Quick Formulas Reference

| Measure | Formula |
|---------|---------|
| Mean | $\bar{x} = \frac{1}{n}\sum x_i$ |
| Variance | $s^2 = \frac{1}{n-1}\sum(x_i - \bar{x})^2$ |
| Std Dev | $s = \sqrt{s^2}$ |
| Z-Score | $z = \frac{x - \bar{x}}{s}$ |

---

## Next Steps

Continue to [[02-Understanding-Returns]] to learn how to properly calculate returns for sigma analysis.

---

#statistics #foundation #normal-distribution #z-score
