# Exercise Set 02: Returns Calculation

Practice calculating simple and log returns from price data.

---

## Instructions

- Use natural logarithm (ln) for log returns
- Show your work
- Round to 4 decimal places for returns (e.g., 0.0234 = 2.34%)
- ln(1.01) ≈ 0.00995, ln(1.05) ≈ 0.04879, ln(0.95) ≈ -0.05129

---

## Part A: Simple Returns

### Exercise 2.1
Calculate the simple return:
- Yesterday's price: $100
- Today's price: $105

### Exercise 2.2
Calculate the simple return:
- Yesterday's price: $82.50
- Today's price: $79.20

### Exercise 2.3
Stock ABC prices:
- Monday close: $45.00
- Tuesday close: $46.35

Calculate the simple return from Monday to Tuesday.

### Exercise 2.4
Calculate simple returns for each day:

| Day | Close Price |
|-----|-------------|
| 0   | $120.00     |
| 1   | $122.40     |
| 2   | $119.95     |
| 3   | $123.55     |
| 4   | $121.08     |

### Exercise 2.5
A stock dropped from $55.00 to $49.50. What is the simple return?

---

## Part B: Log Returns

### Exercise 2.6
Calculate the log return:
- Yesterday's price: $100
- Today's price: $103

### Exercise 2.7
Calculate the log return:
- Yesterday's price: $75.00
- Today's price: $71.25

### Exercise 2.8
Calculate log returns for this price series:

| Day | Price | Log Return |
|-----|-------|------------|
| 0   | 50.00 | -          |
| 1   | 51.50 |            |
| 2   | 50.25 |            |
| 3   | 52.00 |            |
| 4   | 51.00 |            |

### Exercise 2.9
Stock XYZ closed at $200. The next day it closed at $194.
Calculate: a) Simple return, b) Log return

### Exercise 2.10
Convert these prices to log returns:

| Day | Price |
|-----|-------|
| 0   | 85.00 |
| 1   | 86.70 |
| 2   | 84.20 |
| 3   | 87.55 |
| 4   | 88.30 |
| 5   | 85.65 |

---

## Part C: Simple ↔ Log Conversion

### Exercise 2.11
Convert simple return of +5% to log return.

### Exercise 2.12
Convert simple return of -8% to log return.

### Exercise 2.13
Convert log return of +0.03 (3%) to simple return.

### Exercise 2.14
Convert log return of -0.05 (-5%) to simple return.

### Exercise 2.15
Complete this table:

| Simple Return | Log Return |
|---------------|------------|
| +2%           |            |
| -3%           |            |
|               | +4%        |
|               | -2%        |
| +10%          |            |

---

## Part D: Multi-Period Returns

### Exercise 2.16
Stock goes: $100 → $110 → $99
Calculate: a) Day 1 log return, b) Day 2 log return, c) Total 2-day log return by summing

### Exercise 2.17
Verify the additivity of log returns:
Price series: $50 → $52 → $51 → $54

Calculate individual log returns and show they sum to total return.

### Exercise 2.18
Using simple returns for the same series ($50 → $52 → $51 → $54):
a) Calculate each simple return
b) Calculate total return using (1+R₁)(1+R₂)(1+R₃) - 1
c) Compare to sum of log returns

### Exercise 2.19
A stock has these daily log returns: +2%, -1%, +1.5%, -0.5%
What is the cumulative return over 4 days?

### Exercise 2.20
Weekly prices:
$100 → $98 → $102 → $99 → $104

Calculate total return both ways:
a) Directly from first to last price
b) By summing daily log returns

---

## Part E: Real-World Data

### Exercise 2.21
Calculate all daily log returns:

| Date | AAPL Price |
|------|------------|
| Mon  | $175.50    |
| Tue  | $178.25    |
| Wed  | $176.80    |
| Thu  | $180.40    |
| Fri  | $179.15    |

### Exercise 2.22
Complete analysis for this week:

| Day | Open | High | Low | Close | Log Return |
|-----|------|------|-----|-------|------------|
| Mon | 52.00| 53.50| 51.50| 52.75 | -          |
| Tue | 52.80| 54.00| 52.00| 53.20 |            |
| Wed | 53.10| 53.80| 51.90| 52.10 |            |
| Thu | 52.00| 52.75| 50.50| 51.25 |            |
| Fri | 51.40| 53.00| 51.00| 52.50 |            |

### Exercise 2.23
Stock with dividend:
- Day 0 close: $80.00
- Day 1 close: $78.50
- Day 1 dividend: $0.50

Calculate total return including dividend.

### Exercise 2.24
Adjusted vs unadjusted prices:

A 2:1 stock split occurs. Pre-split price: $200, Post-split price: $102

a) What is the raw price return?
b) What should the adjusted return be?

### Exercise 2.25
Calculate returns for portfolio with these holdings:

| Stock | Weight | Daily Return |
|-------|--------|--------------|
| A     | 40%    | +1.5%        |
| B     | 35%    | -0.8%        |
| C     | 25%    | +2.2%        |

What is the portfolio return?

---

## Part F: Annualization

### Exercise 2.26
Daily return = 0.04%. Calculate annualized return.

### Exercise 2.27
Weekly return = 0.3%. Calculate annualized return.

### Exercise 2.28
Monthly return = 1.2%. Calculate annualized return.

### Exercise 2.29
Daily volatility = 1.5%. Calculate annualized volatility.

### Exercise 2.30
You observe annual volatility of 25%. What is the implied daily volatility?

---

## Answers

### Part A
2.1: 5.00%
2.2: -4.00%
2.3: 3.00%
2.4: Day 1: 2.00%, Day 2: -2.00%, Day 3: 3.00%, Day 4: -2.00%
2.5: -10.00%

### Part B
2.6: 2.96%
2.7: -5.13%
2.8: Day 1: 2.96%, Day 2: -2.46%, Day 3: 3.42%, Day 4: -1.94%
2.9: a) -3.00%, b) -3.05%
2.10: Day 1: 1.98%, Day 2: -2.92%, Day 3: 3.90%, Day 4: 0.85%, Day 5: -3.05%

### Part C
2.11: ln(1.05) = 4.88%
2.12: ln(0.92) = -8.34%
2.13: e^0.03 - 1 = 3.05%
2.14: e^-0.05 - 1 = -4.88%
2.15:
| Simple | Log |
|--------|-----|
| 2% | 1.98% |
| -3% | -3.05% |
| 4.08% | 4% |
| -1.98% | -2% |
| 10% | 9.53% |

### Part D
2.16: a) 9.53%, b) -10.54%, c) -1.01% (matches ln(99/100))
2.17: 3.92% + (-1.94%) + 5.72% = 7.70% = ln(54/50)
2.18: a) 4%, -1.92%, 5.88%; b) (1.04)(0.9808)(1.0588)-1 = 8%; c) Log sum = 7.70% → simple 8%
2.19: 2% - 1% + 1.5% - 0.5% = 2%
2.20: a) ln(104/100) = 3.92%; b) Sum daily = 3.92%

### Part E
2.21: Tue: 1.56%, Wed: -0.82%, Thu: 2.02%, Fri: -0.70%
2.22: Tue: 0.85%, Wed: -2.09%, Thu: -1.65%, Fri: 2.41%
2.23: ln((78.50 + 0.50)/80.00) = ln(79/80) = -1.26%
2.24: a) Raw: -49%, b) Adjusted: ~1% (should reflect true gain)
2.25: 0.40(1.5%) + 0.35(-0.8%) + 0.25(2.2%) = 0.60 - 0.28 + 0.55 = 0.87%

### Part F
2.26: 0.04% × 252 = 10.08%
2.27: 0.3% × 52 = 15.6%
2.28: 1.2% × 12 = 14.4%
2.29: 1.5% × √252 = 1.5% × 15.87 = 23.8%
2.30: 25% / √252 = 25% / 15.87 = 1.58%

---

## Self-Assessment

| Score | Level |
|-------|-------|
| 25-30 | Excellent |
| 20-24 | Good |
| 15-19 | Fair |
| < 15  | Review [[02-Understanding-Returns]] |

---

#exercises #returns #log-returns
