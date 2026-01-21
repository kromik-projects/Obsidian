# Exercise Set 04: Sigma Classification

Practice classifying price moves by their sigma magnitude - the core skill!

---

## Instructions

- Use the formula: z = (R - μ) / σ
- Classify moves as: Normal (<1σ), Elevated (1-2σ), Significant (2-3σ), Extreme (3-4σ), Rare (4-5σ), Very Rare (5-6σ), Tail Event (>6σ)
- Show your calculations

---

## Part A: Basic Sigma Classification

### Exercise 4.1
μ = 0.05%, σ = 1.2%
Classify these returns: a) +1.5%, b) -2.8%, c) +0.1%

### Exercise 4.2
μ = 0%, σ = 1.5%
Calculate sigma moves for: a) -3.0%, b) +4.5%, c) -7.5%

### Exercise 4.3
Stock has μ = 0.08%, σ = 1.0%
Today's return = -3.2%
Calculate z-score and classify.

### Exercise 4.4
Index data: μ = 0.03%, σ = 0.9%
Returns to classify: -0.5%, +1.2%, -2.0%, +0.8%, -3.5%

### Exercise 4.5
A stock dropped 5% in one day. Historical σ = 1.8%, μ = 0.1%
What sigma move is this?

---

## Part B: Working Backwards

### Exercise 4.6
If σ = 1.5% and μ = 0%, what return corresponds to:
a) 2σ move up, b) 3σ move down, c) 1.5σ move up

### Exercise 4.7
A -4σ move occurred. If μ = 0.05% and σ = 1.2%, what was the return?

### Exercise 4.8
You want to flag any move exceeding ±2σ.
Given μ = 0.1%, σ = 1.4%
What are the threshold returns?

### Exercise 4.9
Alert system triggers at ±3σ.
μ = 0%, σ = 2.0%
What daily returns trigger an alert?

### Exercise 4.10
If a -5% return is a 4σ event with μ ≈ 0, what is σ?

---

## Part C: Complete Analysis from Raw Data

### Exercise 4.11
Historical data (20 days):

| Day | Return (%) |
|-----|------------|
| 1-5 | 0.5, -0.8, 0.3, -0.5, 0.7 |
| 6-10| -0.4, 0.6, -0.2, 0.4, -0.6 |
| 11-15| 0.8, -0.3, 0.2, -0.7, 0.5 |
| 16-20| -0.1, 0.3, -0.4, 0.6, -0.5 |

Day 21 return = -2.8%

Calculate μ, σ, and classify Day 21.

### Exercise 4.12
Weekly returns for 10 weeks (%):
2.5, -1.8, 1.2, -0.5, 3.1, -2.2, 0.8, -1.5, 1.9, -0.9

Week 11 return = -5.5%

Classify Week 11's move.

### Exercise 4.13
15-day data (%): 1.0, -0.6, 0.4, -0.8, 1.2, -0.5, 0.3, -0.9, 0.7, -0.4, 0.8, -0.3, 0.5, -0.7, 0.6

Day 16 return = +3.2%

Complete analysis and classification.

### Exercise 4.14
Use this data to find and classify the most extreme day:

| Day | Return (%) |
|-----|------------|
| 1   | 0.8        |
| 2   | -1.2       |
| 3   | 0.5        |
| 4   | -3.8       |
| 5   | 0.4        |
| 6   | -0.6       |
| 7   | 0.9        |
| 8   | 2.1        |
| 9   | -0.4       |
| 10  | 0.7        |

### Exercise 4.15
Calculate and classify ALL returns in this series:

| Day | Close | Return | z-score | Class |
|-----|-------|--------|---------|-------|
| 0   | 100   | -      | -       | -     |
| 1   | 101.5 |        |         |       |
| 2   | 99.0  |        |         |       |
| 3   | 102.0 |        |         |       |
| 4   | 98.5  |        |         |       |
| 5   | 103.0 |        |         |       |

First calculate μ and σ from all returns, then classify each.

---

## Part D: Multi-Asset Dashboard

### Exercise 4.16
Create sigma dashboard:

| Stock | Return | μ | σ | z-score | Class |
|-------|--------|---|---|---------|-------|
| AAPL  | -2.5%  | 0.05% | 1.5% | | |
| MSFT  | +1.8%  | 0.06% | 1.3% | | |
| AMZN  | -3.2%  | 0.04% | 2.0% | | |
| GOOGL | +0.5%  | 0.05% | 1.6% | | |
| TSLA  | -6.5%  | 0.10% | 3.2% | | |

### Exercise 4.17
On a market crash day, these returns occurred:

| Index | Return | Historical σ |
|-------|--------|--------------|
| S&P 500 | -4.5% | 1.1% |
| NASDAQ | -5.8% | 1.4% |
| Russell 2000 | -6.2% | 1.6% |
| Dow | -3.8% | 1.0% |

Assume μ ≈ 0. Calculate z-scores and rank by sigma magnitude.

### Exercise 4.18
Currency moves (assume μ = 0):

| Pair | Move | Daily σ | Sigma |
|------|------|---------|-------|
| EUR/USD | -0.8% | 0.5% | |
| GBP/USD | -1.2% | 0.6% | |
| USD/JPY | +1.5% | 0.7% | |
| AUD/USD | -2.0% | 0.8% | |

### Exercise 4.19
Bond vs Equity comparison:

| Asset | Return | σ |
|-------|--------|---|
| 10Y Treasury | -1.5% | 0.4% |
| S&P 500 | -2.0% | 1.0% |

Which had the larger sigma move?

### Exercise 4.20
Crypto analysis (μ = 0):

| Coin | Return | Daily σ | Sigma | Class |
|------|--------|---------|-------|-------|
| BTC  | -12%   | 4%      |       |       |
| ETH  | -15%   | 5%      |       |       |
| XRP  | -8%    | 3%      |       |       |

---

## Part E: Probability and Frequency

### Exercise 4.21
A 3σ move occurred. Under normal distribution:
a) What's the probability of this move?
b) How often should it occur?
c) Is this "impossible"?

### Exercise 4.22
You observed a 5σ move.
a) Theoretical probability?
b) Expected frequency?
c) What does this suggest about the distribution?

### Exercise 4.23
In 252 trading days, you observed:
- 85 days within ±1σ
- 25 days between ±1σ and ±2σ
- 5 days between ±2σ and ±3σ
- 2 days beyond ±3σ

Compare to theoretical (normal) expectations.

### Exercise 4.24
Stock had three 4σ+ events in one year.
a) Expected under normal?
b) What does this indicate?

### Exercise 4.25
Calculate probability of at least one 4σ move in:
a) 1 month (21 days)
b) 1 year (252 days)
c) 5 years

---

## Part F: Real Scenarios

### Exercise 4.26
**Flash Crash Scenario**
S&P 500 dropped 5% in 15 minutes.
If 15-minute σ ≈ 0.15% (normal conditions), what sigma move is this?

### Exercise 4.27
**Earnings Surprise**
Stock typically has σ = 1.5%
After bad earnings, it drops 8%.
Classify this move and assess if it's truly "extreme" for an earnings day.

### Exercise 4.28
**Currency Peg Break**
Swiss Franc moved 30% when SNB removed EUR peg.
If daily σ was 0.3%, what sigma move is this?
Why did normal risk models fail?

### Exercise 4.29
**Volatility Regime**
Stock A: Pre-crisis σ = 1.0%, during crisis σ = 3.5%
A -4% day occurs during crisis.
Calculate z using: a) pre-crisis σ, b) crisis σ

### Exercise 4.30
**Historical Event Analysis**
Black Monday (Oct 19, 1987): S&P 500 fell 20.5%
At the time, daily σ ≈ 1%
a) Calculate the sigma move
b) What probability does normal distribution assign?
c) Discuss implications

---

## Answers

### Part A
4.1: a) +1.21σ (Elevated), b) -2.38σ (Significant), c) +0.04σ (Normal)
4.2: a) -2.0σ, b) +3.0σ, c) -5.0σ
4.3: z = -3.28σ (Extreme)
4.4: -0.59σ, +1.30σ, -2.26σ, +0.86σ, -3.92σ
4.5: z = -2.83σ (Significant)

### Part B
4.6: a) +3.0%, b) -4.5%, c) +2.25%
4.7: Return = 0.05% - 4(1.2%) = -4.75%
4.8: Upper: +2.9%, Lower: -2.7%
4.9: Above +6% or below -6%
4.10: σ = 5%/4 = 1.25%

### Part C
4.11: μ = 0.01%, σ = 0.50%, z = -5.62σ (Very Rare)
4.12: μ = 0.26%, σ = 1.80%, z = -3.20σ (Extreme)
4.13: μ = 0.09%, σ = 0.65%, z = +4.79σ (Rare)
4.14: Day 4 (-3.8%): μ = -0.02%, σ = 1.45%, z = -2.61σ (Significant)
4.15: Returns: 1.49%, -2.48%, 2.99%, -3.50%, 4.47%
      μ = 0.59%, σ = 3.18%
      z-scores: +0.28, -0.97, +0.75, -1.29, +1.22 (all Normal to Elevated)

### Part D
4.16:
| Stock | z-score | Class |
|-------|---------|-------|
| AAPL  | -1.70σ  | Elevated |
| MSFT  | +1.34σ  | Elevated |
| AMZN  | -1.62σ  | Elevated |
| GOOGL | +0.28σ  | Normal |
| TSLA  | -2.06σ  | Significant |

4.17: S&P: -4.09σ, NASDAQ: -4.14σ, Russell: -3.88σ, Dow: -3.80σ
      Rank: NASDAQ > S&P > Russell > Dow

4.18: EUR: -1.6σ, GBP: -2.0σ, JPY: +2.14σ, AUD: -2.5σ

4.19: Treasury: -3.75σ, S&P: -2.0σ. Treasury is larger sigma move!

4.20: BTC: -3σ (Extreme), ETH: -3σ (Extreme), XRP: -2.67σ (Significant)

### Part E
4.21: a) 0.27%, b) ~1/year, c) No, it happens
4.22: a) 0.000057%, b) 1 in 7000 years, c) Fat tails exist
4.23: Observed vs Expected: ±1σ (85 vs 172), shows clustering/fat tails
4.24: a) <1 in 60 years, b) Fat tails / vol clustering
4.25: a) 0.13%, b) 1.58%, c) 7.7%

### Part F
4.26: 5%/0.15% = 33σ (theoretically impossible)
4.27: z = -5.3σ; earnings days have higher expected vol
4.28: 100σ; normal models can't handle regime breaks
4.29: a) -4σ, b) -1.14σ; regime matters!
4.30: a) 20.5σ, b) 10^-89, c) Normal distribution inadequate for tail risk

---

#exercises #sigma-moves #classification
