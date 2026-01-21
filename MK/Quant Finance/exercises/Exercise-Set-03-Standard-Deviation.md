# Exercise Set 03: Standard Deviation

Deep practice on volatility calculations.

---

## Instructions

- Show complete work for variance before taking square root
- Use n-1 (sample) unless specified as population
- Express final σ in same units as input data

---

## Part A: Basic Standard Deviation

### Exercise 3.1
Calculate sample standard deviation:
Data: 5, 10, 15, 20, 25

### Exercise 3.2
Calculate sample standard deviation for these returns (%):
0.5, -0.8, 1.2, -0.4, 0.3

### Exercise 3.3
Complete the table and calculate σ:

Data: 8, 12, 10, 14, 16

| x | x - x̄ | (x - x̄)² |
|---|-------|----------|
|   |       |          |
|   |       |          |
|   |       |          |
|   |       |          |
|   |       |          |
|Sum|       |          |

### Exercise 3.4
Calculate σ using the computational formula:
Data: 2, 4, 6, 8, 10

### Exercise 3.5
Daily returns (%): 1.8, -1.2, 0.6, -0.9, 1.5, -0.3, 0.8

Calculate standard deviation.

---

## Part B: Population vs Sample

### Exercise 3.6
For data: 3, 6, 9, 12
Calculate: a) Population σ, b) Sample s

### Exercise 3.7
Returns: 1.0, -0.5, 0.8, -0.2, 0.4, -0.3

Calculate both population and sample standard deviation. What's the difference?

### Exercise 3.8
If sample variance = 16 with n = 10, what would population variance be if this were the entire population?

### Exercise 3.9
Explain when you would use n vs n-1 in the denominator.

### Exercise 3.10
Sample s = 2.5% with n = 25. Estimate the population σ if this sample is representative.

---

## Part C: Volatility from Returns Data

### Exercise 3.11
Calculate daily volatility:

| Day | Return (%) |
|-----|------------|
| 1   | 0.8        |
| 2   | -1.5       |
| 3   | 0.3        |
| 4   | -0.6       |
| 5   | 1.2        |
| 6   | -0.4       |
| 7   | 0.9        |
| 8   | -0.2       |
| 9   | 0.5        |
| 10  | -0.8       |

### Exercise 3.12
20-day return series (%):
0.5, -0.3, 0.8, -0.6, 0.2, -0.9, 1.1, -0.4, 0.6, -0.5,
0.3, -0.7, 0.9, -0.2, 0.4, -0.8, 0.7, -0.1, 0.5, -0.6

Calculate the 20-day volatility.

### Exercise 3.13
Given these statistics, calculate the standard deviation:
- Sum of returns: 1.5%
- Sum of squared returns: 4.28%²
- Number of observations: 15

### Exercise 3.14
A stock's returns over 5 days average 0.2% with sum of squared deviations = 8.5%²

Calculate the standard deviation.

### Exercise 3.15
Complete volatility analysis:

| Week | Mon | Tue | Wed | Thu | Fri |
|------|-----|-----|-----|-----|-----|
| Returns (%)| 0.6 | -1.1| 0.8 | -0.5| 0.4 |

Calculate: Mean, Variance, σ

---

## Part D: Annualized Volatility

### Exercise 3.16
Daily σ = 1.2%
Calculate: a) Weekly σ, b) Monthly σ, c) Annual σ

### Exercise 3.17
You calculated 20-day volatility = 1.5%
What is the annualized volatility?

### Exercise 3.18
Monthly σ = 4.5%
What is: a) Daily σ, b) Annual σ

### Exercise 3.19
A stock has annual volatility of 30%. Calculate daily volatility.

### Exercise 3.20
Complete this conversion table:

| Daily σ | Weekly σ | Monthly σ | Annual σ |
|---------|----------|-----------|----------|
| 1.0%    |          |           |          |
|         | 3.5%     |           |          |
|         |          | 6.0%      |          |
|         |          |           | 40%      |

---

## Part E: Comparing Volatilities

### Exercise 3.21
Two stocks:
- Stock A: Daily σ = 2.0%
- Stock B: Daily σ = 1.5%

Which is more volatile? By what percentage?

### Exercise 3.22
Portfolio A has annual σ = 18%
Portfolio B has daily σ = 1.3%

Which is more volatile?

### Exercise 3.23
Historical data:
- Stock X: 30-day σ = 2.2%
- Stock Y: 60-day σ = 1.9%

Can you directly compare these? Why or why not?

### Exercise 3.24
Pre-earnings σ = 1.5% (based on 20 days)
Post-earnings σ = 2.8% (based on 5 days)

Volatility increased by what factor? What caution should you have?

### Exercise 3.25
Index volatility = 1.0%
Stock volatility = 2.5%

The stock is how many times more volatile than the index?

---

## Part F: Advanced Calculations

### Exercise 3.26
Calculate rolling 5-day σ for days 5, 6, 7:

| Day | Return (%) |
|-----|------------|
| 1   | 0.5        |
| 2   | -0.8       |
| 3   | 1.0        |
| 4   | -0.3       |
| 5   | 0.6        |
| 6   | -1.2       |
| 7   | 0.8        |

### Exercise 3.27
EWMA calculation with λ = 0.94:
- Previous σ² = 0.0001 (σ = 1%)
- Day 1 return: -2%
- Day 2 return: +1.5%

Calculate σ after each day.

### Exercise 3.28
Parkinson volatility calculation:

| Day | High | Low |
|-----|------|-----|
| 1   | 55   | 52  |
| 2   | 54   | 51  |
| 3   | 56   | 53  |
| 4   | 55   | 52  |
| 5   | 57   | 54  |

### Exercise 3.29
Compare close-to-close vs Parkinson volatility:

| Day | Close | High | Low |
|-----|-------|------|-----|
| 0   | 100   | -    | -   |
| 1   | 102   | 104  | 99  |
| 2   | 100   | 103  | 98  |
| 3   | 103   | 105  | 99  |
| 4   | 101   | 104  | 100 |
| 5   | 104   | 106  | 100 |

### Exercise 3.30
GARCH(1,1) with ω=0.00001, α=0.05, β=0.94:
Starting σ² = 0.0001

Calculate σ after a -3% return.

---

## Answers

### Part A
3.1: 7.91
3.2: 0.749%
3.3: Mean=12, Sum sq dev=40, σ=3.16
3.4: Mean=6, Sum x²=220, σ=3.16
3.5: 1.037%

### Part B
3.6: a) 3.35, b) 3.87
3.7: Pop=0.500%, Samp=0.548%, Diff=0.048%
3.8: 14.4 (multiply by (n-1)/n = 9/10)
3.9: Use n for complete population, n-1 for sample (Bessel's correction)
3.10: ≈2.5% (sample s estimates population σ)

### Part C
3.11: 0.823%
3.12: 0.603%
3.13: Mean=0.1%, s²=(4.28-15×0.01)/14=0.304, σ=0.551%
3.14: σ=√(8.5/4)=1.46%
3.15: Mean=0.04%, Var=0.547, σ=0.74%

### Part D
3.16: a) 2.68%, b) 5.50%, c) 19.05%
3.17: 1.5% × √252 = 23.8%
3.18: a) 0.98%, b) 15.6%
3.19: 30%/√252 = 1.89%
3.20:
| Daily | Weekly | Monthly | Annual |
|-------|--------|---------|--------|
| 1.0%  | 2.24%  | 4.58%   | 15.9%  |
| 1.57% | 3.5%   | 7.17%   | 24.9%  |
| 1.31% | 2.93%  | 6.0%    | 20.8%  |
| 2.52% | 5.63%  | 11.5%   | 40%    |

### Part E
3.21: A is more volatile by 33% (2.0/1.5 = 1.33)
3.22: B: 1.3%×√252=20.6%, so B is more volatile
3.23: Not directly - different lookbacks capture different regimes
3.24: Factor of 1.87; caution: small sample for post-earnings
3.25: 2.5× more volatile

### Part F
3.26: Day 5: 0.65%, Day 6: 0.82%, Day 7: 0.83%
3.27: Day 1: σ=1.17%, Day 2: σ=1.13%
3.28: σ_P ≈ 3.3%
3.29: Close-to-close σ ≈ 1.6%, Parkinson σ ≈ 3.1%
3.30: σ²=0.00001+0.05(0.0009)+0.94(0.0001)=0.00015, σ=1.22%

---

#exercises #standard-deviation #volatility
