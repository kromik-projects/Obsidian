# LNG Trading Strategies

This chapter provides detailed coverage of trading strategies employed by institutional participants in the LNG market.

---

## Strategy Categories

### 1. Physical Arbitrage Strategies

#### Geographic Arbitrage

**Concept:** Exploit price differences between regions

**Atlantic-Pacific Arbitrage:**
```
Opportunity Identification:
JKM (Asia): $16.00/MMBtu
TTF (Europe): $12.00/MMBtu
Gross Spread: $4.00/MMBtu

Cost Analysis (US Gulf cargo to Asia vs Europe):
Route to Asia:
- Shipping: $1.80/MMBtu
- Panama Canal: $0.25/MMBtu
- Total: $2.05/MMBtu

Route to Europe:
- Shipping: $0.80/MMBtu
- Total: $0.80/MMBtu

Net-Back Comparison:
Asia: $16.00 - $2.05 = $13.95/MMBtu
Europe: $12.00 - $0.80 = $11.20/MMBtu
Advantage: Asia by $2.75/MMBtu

Action: Route cargo to Asia
```

**Real-Time Arbitrage Dashboard:**
| Origin | Destination | Price | Shipping | Net-Back | Rank |
|--------|-------------|-------|----------|----------|------|
| US Gulf | Japan | $16.00 | $2.05 | $13.95 | 1 |
| US Gulf | Korea | $15.80 | $2.00 | $13.80 | 2 |
| US Gulf | China | $15.50 | $1.95 | $13.55 | 3 |
| US Gulf | NW Europe | $12.00 | $0.80 | $11.20 | 4 |
| US Gulf | S. Europe | $12.50 | $0.90 | $11.60 | 4 |

**Execution Considerations:**
- Cargo flexibility (destination-free required)
- Shipping availability
- Terminal access at destination
- Timing windows
- Currency considerations

#### Time Arbitrage (Storage Play)

**Concept:** Buy now, store, sell later when contango exists

**Floating Storage Trade:**
```
Market Conditions:
Spot JKM: $10.00/MMBtu
6-month forward JKM: $14.00/MMBtu
Contango: $4.00/MMBtu (40%)

Cost Analysis (6-month floating storage):
Vessel charter: $80,000/day × 180 days = $14.4M
Insurance/other: $0.5M
Boil-off loss: 70,000t × 0.10% × 180 = 12,600t
Boil-off cost: 12,600t × 48.7 × $10 = $6.1M
Financing cost: $50M cargo × 5% × 0.5yr = $1.25M
Total costs: ~$22.25M

Revenue:
Sell forward: 57,400t × 48.7 × $14 = $39.1M
Buy spot: 70,000t × 48.7 × $10 = $34.1M
Gross spread: $5.0M

Net P&L: $5.0M - $22.25M + $34.1M - $39.1M = -$22.25M + $5.0M
Wait... let me recalculate properly:

Buy: 70,000t × 48.7 = 3,409,000 MMBtu × $10 = $34.09M
Sell: (70,000-12,600)t × 48.7 = 2,795,380 MMBtu × $14 = $39.14M
Gross gain: $5.05M
Less costs: $14.4M + $0.5M + $1.25M = $16.15M
Net P&L: -$11.1M (unprofitable)

Trade only works if:
- Contango > ~$6/MMBtu, OR
- Shipping costs much lower, OR
- Boil-off rates minimal
```

#### Quality Arbitrage

**Concept:** Exploit price differences based on LNG specifications

**Rich/Lean Blending:**
```
Rich LNG (Qatar): 1,120 Btu/scf, Premium pricing
Lean LNG (Australia): 1,050 Btu/scf, Discount pricing

Buyer Specification: 1,080-1,100 Btu/scf

Strategy:
- Purchase lean cargo at discount
- Blend with rich heel/inventory
- Deliver within spec at standard price
- Capture blending margin
```

---

### 2. Spread Trading Strategies

#### Calendar Spreads

**Winter-Summer Spread:**
```
Thesis: Winter demand creates predictable seasonal premium

Historical Analysis:
| Year | Jan JKM | Jul JKM | Spread |
|------|---------|---------|--------|
| 2019 | $9.50 | $5.50 | $4.00 |
| 2020 | $5.00 | $2.50 | $2.50 |
| 2021 | $12.00 | $8.00 | $4.00 |
| 2022 | $35.00 | $25.00 | $10.00 |
| 2023 | $25.00 | $12.00 | $13.00 |
| 2024 | $14.00 | $10.00 | $4.00 |

Average spread: ~$6/MMBtu (varies widely)

Entry (September):
Jan JKM: $12.00
Jul JKM: $9.00
Spread: $3.00 (below average)

Position: Buy Jan / Sell Jul (long spread)
Size: 100 lots each leg
Cost: Margin only (spread margin ~$2,500/lot)

Target: $5.00 spread (+$2.00)
Stop: $1.50 spread (-$1.50)
Risk/Reward: 1.3:1

Exit (November):
Jan JKM: $15.00
Jul JKM: $10.50
Spread: $4.50

P&L: ($4.50 - $3.00) × 10,000 × 100 = $1,500,000
```

**Roll Strategy:**
```
Objective: Maintain consistent seasonal exposure

Q1 Entry:
Long Sep (next winter) / Short Mar (current shoulder)

As time passes:
Roll: Close Sep/Mar, open Dec/Jun

Continuous roll captures:
- Seasonal patterns
- Contango/backwardation shifts
- Avoiding delivery
```

#### Geographic Spreads

**JKM-TTF Spread:**
```
Fundamental Drivers:
- Relative demand (Asia vs Europe)
- Shipping costs/availability
- New supply allocations
- Weather differentials

Technical Trading:
Historical spread range: $1-$8/MMBtu (normal)
Extreme range: -$5 to +$30/MMBtu

Mean Reversion Strategy:
Entry: When spread > 2 standard deviations
Direction: Fade extreme
Size: Based on conviction and liquidity
Stop: Technical level or time-based

Example:
Normal spread: $3.00/MMBtu
Current spread: $8.00/MMBtu (2.5 std devs)
Entry: Short JKM / Long TTF (normalized)
Target: $4.00 spread
Stop: $10.00 spread
```

**JKM-HH Spread (Net-back):**
```
US Export Economics Spread:
JKM - HH - $5.00 (liquefaction + shipping) = Margin

Historical Margin Range:
Profitable: > $0 (exports flow)
Marginal: $0-$2 (selective cargoes)
Unprofitable: < $0 (cancellations possible)

Trading Logic:
If margin very high (>$10):
- Expect more US exports
- Eventually pressures JKM down, HH up
- Trade: Short spread (expecting compression)

If margin negative:
- Expect cargo cancellations
- Eventual price adjustment
- Trade: Long spread (expecting widening)
```

---

### 3. Relative Value Strategies

#### Oil-Gas Ratio Trading

**JKM vs JCC Relationship:**
```
Traditional Parity: JKM ≈ 14.5% × JCC

Calculate Fair Value:
JCC = $80/bbl
Fair JKM = 0.145 × $80 = $11.60/MMBtu

Current JKM: $14.00/MMBtu
Premium to oil-parity: $2.40 (20.7%)

Trade Analysis:
If expecting mean reversion to oil parity:
- Short JKM / Long crude exposure (Brent proxy)
- Ratio: Energy-equivalent basis

Risks:
- Gas-oil decoupling (structural shift)
- LNG-specific factors (supply/demand)
- Different seasonal patterns
```

#### Cross-Hub Relative Value

**TTF vs NBP:**
```
Normally highly correlated (both European hubs)

Divergence Drivers:
- UK isolation (storage, interconnector issues)
- Seasonal UK demand differences
- Currency (EUR vs GBP)

Mean Reversion Trade:
Historical TTF-NBP spread: €0-3/MWh
Current spread: €6/MWh (unusual)

Trade: Short TTF / Long NBP (expect convergence)
```

**TTF vs JKM vs HH Triangular:**
```
Monitor three-way relationship:
TTF/HH ratio: Historical ~3-4x
JKM/TTF ratio: Historical ~1.1-1.5x

If ratios diverge significantly:
- Identify the outlier
- Trade against the outlier
- Use pairwise positions
```

---

### 4. Volatility Strategies

#### Long Volatility (Straddles/Strangles)

**When to Use:**
- Expecting large price move, direction uncertain
- Before major events (weather, geopolitical)
- Implied volatility appears low

**Straddle Example:**
```
Current JKM: $13.00/MMBtu
Q1 Expiry: 60 days

Position:
Buy $13 Call @ $1.20
Buy $13 Put @ $1.10
Total Premium: $2.30/MMBtu

Breakeven:
Upper: $15.30 ($13 + $2.30)
Lower: $10.70 ($13 - $2.30)
Range: $4.60 (35% of current price)

P&L Scenarios:
If JKM = $18: Call value $5, Put $0, Net +$2.70
If JKM = $8: Put value $5, Call $0, Net +$2.70
If JKM = $13: Both expire worthless, Net -$2.30
```

**Strangle (Wider Strikes):**
```
Buy $15 Call @ $0.50
Buy $11 Put @ $0.45
Total Premium: $0.95/MMBtu

Lower cost, but needs larger move:
Breakeven: >$15.95 or <$10.05
```

#### Short Volatility (Premium Collection)

**When to Use:**
- Range-bound market expected
- Implied volatility appears high
- Comfortable with potential assignment

**Iron Condor Example:**
```
Current JKM: $13.00/MMBtu
Q1 Expiry: 45 days

Position:
Sell $15 Call @ $0.60
Buy $17 Call @ $0.20 (protection)
Sell $11 Put @ $0.55
Buy $9 Put @ $0.15 (protection)

Net Premium Collected:
(0.60 - 0.20) + (0.55 - 0.15) = $0.80/MMBtu

Max Profit: $0.80/MMBtu (if $11 < JKM < $15 at expiry)
Max Loss: $2.00 - $0.80 = $1.20/MMBtu (if beyond wings)
Probability of Profit: ~60-70% (depending on vol)
```

#### Volatility Surface Trading

**Skew Trading:**
```
Observation: Put volatility >> Call volatility

Interpretation:
- Market pricing crash risk high
- Downside protection expensive

Trade (if view skew excessive):
- Sell put, buy call (risk reversal)
- Collect skew premium
- Risk: Market actually crashes
```

---

### 5. Event-Driven Strategies

#### Weather Trading

**Setup Phase:**
1. Monitor long-range forecasts (10-15 day)
2. Identify significant deviations from normal
3. Assess supply/demand impact
4. Position ahead of market recognition

**Cold Snap Trade:**
```
Scenario: Week 2 forecast shows severe cold in Northeast Asia

Analysis:
- Japan heating demand: +15-20% vs normal
- Korea similar
- Spot LNG demand spike expected
- Current JKM: $12.00/MMBtu

Position:
- Buy JKM Jan futures (cold month)
- Size: Based on confidence and risk budget
- Entry: Before forecast widely recognized

Execution:
Day 1: Buy 100 lots @ $12.00
Day 3: Forecast gains attention, JKM rises to $13.50
Day 7: Cold snap confirmed, JKM at $15.00
Exit: Sell 100 lots @ $15.00

P&L: ($15 - $12) × 10,000 × 100 = $3,000,000
```

#### Supply Disruption Trading

**Unplanned Outage Response:**
```
Event: Major facility announces emergency shutdown

Immediate Actions:
1. Assess outage scope (duration, volume impact)
2. Evaluate market position
3. Execute direction trades (typically buy)
4. Consider spread implications

Example - Freeport LNG Outage (2022):
- Capacity: ~15 MTPA
- Initial estimate: Weeks
- Actual: Months

Market Impact:
- JKM: Initially spiked on supply concern
- TTF: Rose (more cargoes diverted to Europe)
- HH: Dropped (reduced export demand)

Trade:
- Long JKM/TTF (supply tightness)
- Short HH (demand destruction)
```

#### Geopolitical Event Trading

**Sanctions/Policy Events:**
```
Framework:
1. Monitor policy announcements, elections, diplomacy
2. Scenario analysis for potential outcomes
3. Pre-position for likely scenarios
4. Hedge tail risks with options

Example - Russia Tensions:
Base case: Continued uncertainty
Bull case (LNG): Escalation, supply disruption
Bear case (LNG): De-escalation, demand shift

Position:
- Core: Modest long LNG
- Tail hedge: Deep OTM calls (black swan)
```

---

### 6. Structured Trading Strategies

#### Portfolio Optimization

**Integrated Physical-Paper Strategy:**
```
Physical Portfolio:
- 5 MTPA long-term purchases
- 3 MTPA long-term sales
- Net long: 2 MTPA

Paper Overlay:
- Hedge seasonal risk (sell winter/buy summer)
- Optimize geographic allocation
- Manage basis risk (JKM vs contract pricing)

Continuous Optimization:
1. Daily: Mark-to-market, delta hedge
2. Weekly: Review allocations, rebalance
3. Monthly: Strategy review, position adjustments
4. Quarterly: Portfolio composition review
```

#### Option-Enhanced Strategies

**Covered Call (Against Physical Long):**
```
Physical: Own cargo for February delivery
Current value: JKM $14.00/MMBtu

Strategy: Sell call options against position
Sell Feb $16 Call @ $0.40/MMBtu

Outcomes:
If JKM < $16: Keep premium, sell physical at market
If JKM > $16: Called away at $16.40 effective ($16 + $0.40)

Rationale:
- Generate additional income on inventory
- Willing to cap upside at $16.40
- Reduces effective purchase cost
```

**Protective Put (Downside Protection):**
```
Physical: Own cargo for delivery
Concern: Price decline before sale

Strategy: Buy put options
Buy Feb $12 Put @ $0.30/MMBtu

Outcomes:
If JKM > $12: Put expires, sell physical at market
If JKM < $12: Exercise put, sell at $11.70 effective

Rationale:
- Insurance against significant decline
- Maintains upside participation
- Cost: $0.30/MMBtu (2% of value)
```

---

### 7. Algorithmic/Quantitative Strategies

#### Statistical Arbitrage

**Pairs Trading:**
```
Identify cointegrated pairs:
- JKM vs 14.5% × JCC
- TTF vs NBP
- JKM vs crude oil basket

Model:
Spread = Price_A - β × Price_B
Z-score = (Spread - Mean) / Std_Dev

Trade Rules:
Entry: Z-score > 2 or < -2
Exit: Z-score returns to 0
Stop: Z-score > 3 or < -3

Backtest Results (example):
Win rate: 68%
Avg win: +$0.80/MMBtu
Avg loss: -$1.20/MMBtu
Sharpe: 1.4
```

#### Momentum/Trend Following

**Moving Average System:**
```
Signals:
Fast MA (10-day) crosses above Slow MA (30-day): Buy
Fast MA crosses below Slow MA: Sell

Position Sizing:
Risk budget: 2% of capital per trade
Stop loss: 2 ATR (Average True Range)
Position = Risk Budget / (ATR × 2)

Example:
Capital: $10M
Risk per trade: $200K
ATR: $0.60/MMBtu
Stop distance: $1.20/MMBtu
Position: $200K / $1.20 = 166,666 MMBtu = ~17 lots
```

#### Machine Learning Applications

**Forecasting Models:**
- Weather-price relationships
- Supply/demand pattern recognition
- Sentiment analysis (news, shipping data)
- Volatility prediction

**Trade Generation:**
- Feature engineering from market data
- Model training on historical patterns
- Signal generation with confidence scores
- Risk-adjusted position sizing

---

## Strategy Risk Considerations

### Strategy-Specific Risks

| Strategy | Key Risks | Mitigation |
|----------|-----------|------------|
| Geographic arb | Shipping disruption, terminal access | Multiple routes, backup vessels |
| Calendar spread | Carry cost changes, curve shifts | Stop losses, spread limits |
| Volatility | Theta decay, vol crush | Time management, vol monitoring |
| Event-driven | Wrong direction, timing | Position sizing, options |
| Statistical arb | Regime change, correlation breakdown | Model review, drawdown limits |

### Portfolio Construction

**Diversification Principles:**
- Mix of strategies (arb, directional, relative value)
- Different time horizons
- Multiple market correlations
- Strategy capacity limits

**Example Allocation:**
```
Total Risk Budget: $5M VaR

Allocation:
Geographic arbitrage: 30% ($1.5M)
Calendar spreads: 25% ($1.25M)
Relative value: 20% ($1.0M)
Event-driven: 15% ($0.75M)
Options strategies: 10% ($0.5M)
```

---

**Next**: [[10-LNG-Knowledge-Index]] - Complete knowledge index and reference
