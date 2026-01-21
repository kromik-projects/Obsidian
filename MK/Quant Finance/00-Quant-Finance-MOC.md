# Quant Finance - Map of Content

Welcome to the Quantitative Finance Knowledge Base. This collection focuses on **statistical analysis of stock price movements**, with particular emphasis on identifying and understanding **sigma moves** (large deviations from expected behavior).

---

## Learning Path

### Foundation
1. [[01-Foundational-Statistics]] - Core statistical concepts
2. [[02-Understanding-Returns]] - How to calculate and interpret returns
3. [[03-Standard-Deviation-Deep-Dive]] - The heart of volatility measurement

### Core Analysis
4. [[04-Sigma-Moves-Explained]] - Understanding deviation events
5. [[05-Volatility-Estimation]] - Techniques for measuring volatility
6. [[06-Probability-of-Extreme-Moves]] - Theoretical vs actual probabilities

### Advanced Topics
7. [[07-Fat-Tails-and-Reality]] - Why markets aren't normal
8. [[08-Rolling-Window-Analysis]] - Dynamic volatility measurement

### Reference
- [[09-Formula-Reference-Sheet]] - Quick lookup for all formulas
- [[10-Worked-Examples]] - Step-by-step solutions

### Practice
- [[exercises/Exercise-Set-01-Basic-Statistics]]
- [[exercises/Exercise-Set-02-Returns-Calculation]]
- [[exercises/Exercise-Set-03-Standard-Deviation]]
- [[exercises/Exercise-Set-04-Sigma-Classification]]
- [[exercises/Exercise-Set-05-Volatility-Analysis]]
- [[exercises/Exercise-Set-06-Comprehensive-Problems]]

---

## Quick Reference

### What is a Sigma Move?

A **sigma move** (σ move) measures how many standard deviations a price change is from the expected (mean) change.

$$\text{Sigma Move} = \frac{R_t - \mu}{\sigma}$$

Where:
- $R_t$ = Return at time $t$
- $\mu$ = Mean (average) return
- $\sigma$ = Standard deviation of returns

### Sigma Move Probabilities (Normal Distribution)

| Sigma | Probability | Frequency (Trading Days) |
|-------|-------------|-------------------------|
| ±1σ   | 31.73%      | ~80 days/year          |
| ±2σ   | 4.55%       | ~11 days/year          |
| ±3σ   | 0.27%       | ~1 day/year            |
| ±4σ   | 0.0063%     | ~1 day/16 years        |
| ±5σ   | 0.000057%   | ~1 day/1,744 years     |
| ±6σ   | 0.0000002%  | ~1 day/500,000 years   |

> **Reality Check**: In actual markets, extreme moves occur FAR more frequently than normal distribution predicts!

---

## Tags
#quant-finance #statistics #volatility #sigma-moves #trading
