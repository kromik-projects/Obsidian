# Exercise Set 05: Volatility Analysis

Practice advanced volatility estimation and analysis techniques.

---

## Instructions

- λ = 0.94 for EWMA unless specified
- Use 252 trading days per year for annualization
- Show intermediate calculations

---

## Part A: EWMA Volatility

### Exercise 5.1
EWMA update:
- Previous σ² = 0.0001 (σ = 1%)
- λ = 0.94
- Yesterday's return = -1.5%

Calculate new EWMA variance and σ.

### Exercise 5.2
Track EWMA σ over 5 days:
- Starting σ = 1.2%
- λ = 0.94
- Returns: -2.0%, +1.0%, -0.5%, +1.5%, -0.8%

### Exercise 5.3
Compare λ = 0.90 vs λ = 0.97:
Starting σ = 1.5%, Return = -3.0%

Calculate new σ for each λ.

### Exercise 5.4
EWMA half-life:
a) λ = 0.94, calculate half-life
b) If you want half-life = 20 days, what λ?

### Exercise 5.5
Build EWMA series from scratch (λ = 0.94):
Initial variance estimate from first 5 returns, then track:

Returns (%): 0.5, -0.8, 1.2, -0.4, 0.6, -1.5, 0.8, -0.3, 1.0, -2.5

---

## Part B: Rolling Window Analysis

### Exercise 5.6
Calculate 5-day rolling σ:

| Day | Return (%) |
|-----|------------|
| 1   | 0.8        |
| 2   | -1.2       |
| 3   | 0.5        |
| 4   | -0.6       |
| 5   | 0.9        |
| 6   | -1.8       |
| 7   | 0.4        |
| 8   | -0.3       |

Provide σ for days 5, 6, 7, 8.

### Exercise 5.7
10-day rolling volatility:

Returns (%): 0.5, -0.3, 0.8, -0.6, 0.2, -0.9, 1.1, -0.4, 0.6, -0.5, 0.3, -0.7, 0.9, -0.2

Calculate rolling σ for days 10, 11, 12.

### Exercise 5.8
Rolling sigma move classification:
Using 20-day rolling μ and σ, classify Day 21:

Days 1-20 returns (%):
0.5, -0.3, 0.8, -0.5, 0.2, -0.7, 0.9, -0.4, 0.3, -0.6,
0.6, -0.2, 0.4, -0.8, 0.7, -0.3, 0.5, -0.4, 0.6, -0.5

Day 21 return = -2.8%

### Exercise 5.9
Multi-window comparison:

| Day | Return |
|-----|--------|
| 1-10 | 0.5, -0.3, 0.8, -0.2, 0.4, -0.6, 0.9, -0.1, 0.3, -0.5 |
| 11-20 | 1.2, -0.8, 1.5, -0.5, 0.9, -1.2, 0.7, -0.4, 1.0, -0.6 |
| 21-30 | 0.3, -0.2, 0.5, -0.3, 0.4, -0.5, 0.6, -0.2, 0.3, -0.4 |

Compare 10-day σ (days 21-30) vs 30-day σ (all data).

### Exercise 5.10
Expanding window vs rolling window:

Data: 1.0, -0.5, 0.8, -0.3, 1.2, -0.8, 0.4, -0.6, 0.9, -0.4

Calculate:
a) Final expanding window σ (all 10 points)
b) Final 5-day rolling σ
c) Explain the difference

---

## Part C: Range-Based Volatility

### Exercise 5.11
Parkinson volatility:

| Day | High | Low |
|-----|------|-----|
| 1   | 52   | 50  |
| 2   | 53   | 50  |
| 3   | 52   | 49  |
| 4   | 54   | 51  |
| 5   | 53   | 50  |

### Exercise 5.12
Compare close-to-close vs Parkinson:

| Day | Open | High | Low | Close |
|-----|------|------|-----|-------|
| 0   | -    | -    | -   | 100   |
| 1   | 100  | 104  | 98  | 102   |
| 2   | 102  | 105  | 100 | 103   |
| 3   | 103  | 106  | 101 | 104   |
| 4   | 104  | 107  | 102 | 105   |
| 5   | 105  | 108  | 103 | 106   |

### Exercise 5.13
Garman-Klass volatility estimate:

| Day | O | H | L | C |
|-----|---|---|---|---|
| 1   | 50 | 52 | 49 | 51 |
| 2   | 51 | 53 | 50 | 52 |
| 3   | 52 | 54 | 50 | 51 |

Use: σ²_GK = 0.5(ln H - ln L)² - 0.386(ln C - ln O)²

### Exercise 5.14
Intraday range analysis:

| Day | Range (High-Low) | Close | True Range |
|-----|------------------|-------|------------|
| 1   | $3.50            | $102  |            |
| 2   | $4.20            | $100  |            |
| 3   | $2.80            | $103  |            |
| 4   | $5.10            | $99   |            |
| 5   | $3.00            | $101  |            |

Calculate average true range as % of close.

### Exercise 5.15
Efficiency comparison:

A stock has:
- Close-to-close σ = 1.8% (calculated from 30 days)
- Parkinson σ = 2.1% (from same 30 days)

a) Which is likely more accurate?
b) What might explain the difference?

---

## Part D: Volatility Regimes

### Exercise 5.16
Identify regime change:

| Period | Days | Avg Return | σ |
|--------|------|------------|---|
| Pre-event | 1-20 | 0.1% | 0.8% |
| During | 21-30 | -0.5% | 2.5% |
| Post | 31-50 | 0.0% | 1.2% |

a) Volatility multiplier during event?
b) How long until return to normal?

### Exercise 5.17
VIX vs realized volatility:

| Week | VIX Level | Realized σ (annualized) |
|------|-----------|------------------------|
| 1    | 15        | 12%                    |
| 2    | 18        | 14%                    |
| 3    | 25        | 22%                    |
| 4    | 35        | 38%                    |
| 5    | 28        | 30%                    |

Plot mentally and describe the relationship.

### Exercise 5.18
Volatility mean reversion:
Long-term σ = 20% (annual)
Current σ = 35% (annual)

If vol reverts 10% per month toward mean, project σ for next 3 months.

### Exercise 5.19
GARCH long-run variance:
ω = 0.000005, α = 0.08, β = 0.90

a) Calculate long-run variance
b) Calculate long-run daily σ
c) Calculate long-run annual σ

### Exercise 5.20
Conditional vs unconditional volatility:

After a -4% day, EWMA σ jumps to 2.5%.
Long-run average σ = 1.5%.

a) How many days until σ is within 0.1% of long-run? (λ = 0.94)
b) What does this tell you about vol persistence?

---

## Part E: Practical Applications

### Exercise 5.21
Position sizing with volatility:
- Target daily risk = $1000
- Stock price = $50
- Daily σ = 2%

How many shares can you hold?

### Exercise 5.22
VaR calculation:
- Portfolio value = $100,000
- Daily σ = 1.5%
- 99% confidence

Calculate 1-day VaR.

### Exercise 5.23
Volatility-adjusted returns:

| Stock | Return | σ | Risk-Adj Return |
|-------|--------|---|-----------------|
| A     | 15%    | 25% |                |
| B     | 10%    | 12% |                |
| C     | 20%    | 40% |                |

Calculate Sharpe-like ratio (Return/σ).

### Exercise 5.24
Volatility targeting:
Target portfolio σ = 15% annual
Stock σ = 25% annual

What weight in stock (remainder in cash) achieves target?

### Exercise 5.25
Options pricing input:
Current stock price = $100
You calculated 30-day realized σ = 1.5% daily

What annualized volatility should you input for options pricing?

---

## Answers

### Part A
5.1: σ² = 0.94(0.0001) + 0.06(0.000225) = 0.0001075, σ = 1.04%
5.2: Day 1: 1.31%, Day 2: 1.27%, Day 3: 1.23%, Day 4: 1.21%, Day 5: 1.17%
5.3: λ=0.90: σ=1.68%, λ=0.97: σ=1.53%
5.4: a) 11.0 days, b) λ = 0.966
5.5: Initial σ = 0.76%, final σ ≈ 1.4% (spikes after -2.5%)

### Part B
5.6: Day 5: 0.84%, Day 6: 1.05%, Day 7: 1.06%, Day 8: 0.88%
5.7: Day 10: 0.61%, Day 11: 0.62%, Day 12: 0.63%
5.8: μ = 0.04%, σ = 0.52%, z = -5.46σ (Very Rare)
5.9: 10-day σ = 0.34%, 30-day σ = 0.66%; Recent period calmer
5.10: a) 0.71%, b) 0.56%, c) Rolling adapts to recent, expanding uses all

### Part C
5.11: σ_P ≈ 2.9%
5.12: Close-to-close σ ≈ 0.95%, Parkinson σ ≈ 3.5%
5.13: σ_GK ≈ 3.2%
5.14: ATR% = 3.5%, 4.2%, 2.7%, 5.2%, 3.0% → Avg ≈ 3.7%
5.15: a) Parkinson (uses more info), b) Intraday vol not captured by close

### Part D
5.16: a) 3.1x, b) ~20 days
5.17: VIX leads/overestimates, converge during high vol
5.18: Month 1: 33.5%, Month 2: 32.2%, Month 3: 31.0%
5.19: a) 0.00025, b) 1.58%, c) 25.1%
5.20: a) ~30 days, b) Vol is highly persistent

### Part E
5.21: 1000 shares ($1000 / ($50 × 0.02))
5.22: VaR = $100,000 × 1.5% × 2.33 = $3,495
5.23: A: 0.60, B: 0.83, C: 0.50; B best risk-adjusted
5.24: 60% in stock (0.6 × 25% = 15%)
5.25: 1.5% × √252 = 23.8%

---

#exercises #volatility #EWMA #rolling-window
