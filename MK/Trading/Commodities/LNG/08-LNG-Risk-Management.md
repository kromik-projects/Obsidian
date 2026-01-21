# LNG Risk Management

Comprehensive risk management is essential for all LNG market participants. This chapter covers the risk framework, measurement techniques, and mitigation strategies.

---

## Risk Categories

### 1. Market/Price Risk

**Definition:** Risk of adverse price movements affecting position value or margin

**Sub-categories:**

| Risk Type | Description |
|-----------|-------------|
| Directional | Outright price level changes |
| Basis | Price differential changes (JKM vs TTF, etc.) |
| Curve | Shape of forward curve changes |
| Volatility | Implied volatility changes (option positions) |
| Correlation | Relationship between prices changes |

**Measurement Metrics:**

| Metric | Description | Use |
|--------|-------------|-----|
| **VaR (Value at Risk)** | Max loss at confidence level | Aggregate risk |
| **Delta** | Sensitivity to price change | Directional exposure |
| **Gamma** | Delta sensitivity to price | Non-linear risk |
| **Vega** | Sensitivity to volatility | Option risk |
| **PV01/DV01** | Sensitivity to 1bp change | Curve risk |

**VaR Calculation Example:**
```
Portfolio: Long 100 lots JKM futures (1,000,000 MMBtu)
Daily JKM volatility: 3% ($0.45 at $15/MMBtu)
Confidence level: 95% (1.65 standard deviations)
Holding period: 1 day

1-day 95% VaR = Position × Price × Volatility × Z-score
              = 1,000,000 × $0.45 × 1.65
              = $742,500
```

### 2. Volumetric Risk

**Definition:** Risk from quantity variations vs. expectations

**Sources:**
- Demand uncertainty (weather, economic)
- Supply variability (outages, maintenance)
- Take-or-pay obligations
- Scheduling constraints

**Management Approaches:**
- Volume flexibility in contracts (DQT/UQT)
- Storage utilization
- Balancing through spot market
- Demand forecasting improvements

### 3. Operational Risk

**Definition:** Risk of loss from failed processes, systems, or external events

**Categories:**

| Category | Examples |
|----------|----------|
| Terminal operations | Loading delays, equipment failure |
| Shipping | Vessel breakdown, routing issues |
| Quality | Off-spec cargo, contamination |
| Scheduling | Nomination errors, communication failures |
| Systems | Trading system outages, data errors |
| Human error | Trade entry mistakes, process failures |

### 4. Credit/Counterparty Risk

**Definition:** Risk of counterparty default on obligations

**Exposure Types:**
- **Mark-to-market (MTM)**: Current replacement cost
- **Potential future exposure (PFE)**: Possible future increase in exposure
- **Settlement risk**: Payment timing mismatch
- **Delivery risk**: Physical delivery default

**Credit Exposure Calculation:**
```
Current Exposure = Max(0, Contract Value - Market Value)

Example:
Contracted price: $12/MMBtu (selling)
Current market: $15/MMBtu
Remaining volume: 500,000 MMBtu

Exposure = (15 - 12) × 500,000 = $1,500,000
(Counterparty owes us more than contracted)
```

### 5. Liquidity Risk

**Definition:** Risk of inability to execute transactions at reasonable prices

**Sub-types:**
- **Market liquidity**: Ability to trade without excessive impact
- **Funding liquidity**: Access to cash/credit for margin, collateral

**Indicators:**
- Bid-ask spreads
- Open interest/volume
- Order book depth
- Time to execute

### 6. Geopolitical/Regulatory Risk

**Definition:** Risk from political events or regulatory changes

**Examples:**
- Sanctions (Russia, Iran)
- Trade policy changes
- Tax/royalty regime changes
- Environmental regulations
- Force majeure events

---

## Hedging Strategies

### Basic Hedging Approaches

**1. Forward/Futures Hedge:**
```
Physical Position: Long 1 cargo (70,000t) for March delivery
Risk: JKM price decline

Hedge: Sell JKM March futures
- Quantity: 70,000t × 48.7 = 3,409,000 MMBtu
- Contracts: 340 lots (10,000 MMBtu each)
- Price: $14.00/MMBtu

Outcome:
If JKM falls to $12: Futures gain $2 × 3,409,000 = +$6.82M
Physical loss: $2 × 3,409,000 = -$6.82M
Net: ~$0 (hedge effective)
```

**2. Swap Hedge:**
```
Exposure: Receive oil-indexed price, exposed to hub price
Formula: 14.5% × JCC

Hedge: Enter JKM-JCC basis swap
- Pay: 14.5% × JCC
- Receive: JKM flat
- Converts oil exposure to JKM exposure

Then hedge JKM with futures if desired
```

**3. Option Hedge:**
```
Exposure: Buying cargo at JKM
Risk: Price spike

Hedge: Buy JKM call option
- Strike: $16/MMBtu
- Premium: $0.50/MMBtu
- Expiry: Delivery month

Outcome:
If JKM = $20: Exercise call, effective purchase at $16.50
If JKM = $12: Option expires, purchase at $12.50 (incl. premium)
```

### Complex Hedging Strategies

**1. Cross-Commodity Hedge:**
When direct hedge unavailable, use correlated markets

```
Exposure: DES India LNG price
Liquid hedge: JKM (different location)
Basis risk: JKM-India differential

Execute:
- Hedge with JKM futures (imperfect but liquid)
- Monitor basis risk
- Adjust hedge ratio based on correlation
```

**2. Time Spread Hedge:**
```
Exposure: Contracted to deliver in Q1 at fixed price
Risk: Need to purchase Q1 supply; price curve may shift

Hedge: Enter calendar spread
- Buy Q1 futures
- Sell Q4 (or other month) futures
- Locks in relative pricing
```

**3. Portfolio Hedge:**
```
Multiple exposures:
- Long Q1 cargo (+3M MMBtu at JKM)
- Short Q2 contract (-2M MMBtu at 14% JCC)
- Long Q3 cargo (+2M MMBtu at JKM)

Hedge design:
1. Calculate net JKM delta: +3M - 0 + 2M = +5M
2. Calculate JCC/oil delta: -2M × 14% × conversion
3. Execute:
   - Sell 500 lots JKM futures (5M/10K)
   - Buy oil or JCC swaps for remaining exposure
```

### Hedge Effectiveness

**Measurement:**
```
Hedge Effectiveness = Change in Hedge Value / Change in Exposure Value

Target: 80-125% effectiveness for accounting hedge qualification
```

**Basis Risk Impact:**
```
Perfect hedge: Exposure matches hedge instrument exactly
Basis risk sources:
- Location (JKM vs. actual delivery point)
- Timing (futures month vs. delivery date)
- Quality (specification differences)
- Volume (rounding, cargo size vs. lots)
```

---

## Risk Measurement Framework

### Position Reporting

**Daily Position Report:**
```
Position Summary - Date: XX/XX/XXXX

Physical Positions:
| Contract | Buy/Sell | Volume (t) | Delivery | Price | MTM |
|----------|----------|------------|----------|-------|-----|
| ABC Corp | Buy | 70,000 | Mar | JKM | +$1.2M |
| XYZ Ltd | Sell | 65,000 | Mar | $14.50 | -$0.5M |

Derivative Positions:
| Instrument | Long/Short | Quantity | Month | Price | MTM |
|------------|------------|----------|-------|-------|-----|
| JKM Futures| Short | 340 lots | Mar | $14.00| +$0.3M |
| TTF Swap | Long | 500 lots | Q2 | €42 | -$0.2M |

Net MTM: +$0.8M
Delta (JKM): +50 lots equivalent
Delta (TTF): +500 lots equivalent
```

### Value at Risk (VaR) Framework

**VaR Methodologies:**

| Method | Description | Pros | Cons |
|--------|-------------|------|------|
| **Historical** | Use actual past returns | Captures fat tails | Limited by history |
| **Parametric** | Assume normal distribution | Simple, fast | May underestimate tail risk |
| **Monte Carlo** | Simulate many scenarios | Flexible, comprehensive | Computationally intensive |

**VaR Parameters:**
- Confidence level: 95% (1.65σ), 99% (2.33σ)
- Holding period: 1-day, 10-day, 1-month
- Look-back period: 1 year, 3 years

**Example VaR Report:**
```
Portfolio VaR Summary (95%, 1-day)

By Risk Factor:
JKM: $1.2M
TTF: $0.8M
Brent: $0.3M
FX: $0.1M
Diversification benefit: -$0.6M
Total VaR: $1.8M

By Business Unit:
Physical trading: $1.0M
Paper trading: $0.6M
Options: $0.2M
Total: $1.8M
```

### Stress Testing

**Historical Scenarios:**
| Scenario | Description | Portfolio Impact |
|----------|-------------|------------------|
| 2021 Asia spike | JKM +$20, TTF +$15 | -$5.2M |
| 2020 COVID crash | JKM -$6, TTF -$4 | +$2.1M |
| 2022 EU crisis | TTF +€200, JKM +$30 | -$8.5M |

**Hypothetical Scenarios:**
| Scenario | Assumptions | Portfolio Impact |
|----------|-------------|------------------|
| Cold winter | JKM +50%, TTF +40% | -$4.0M |
| Supply disruption | JKM +30%, shipping +100% | -$2.5M |
| Demand shock | JKM -40%, TTF -35% | +$3.2M |

### Greeks Management

**Delta Limits:**
```
JKM Delta Limit: ± 500 lots (5M MMBtu)
TTF Delta Limit: ± 300 lots
Aggregate Delta: ± 600 lots

Current Position:
JKM: +450 lots (90% of limit)
TTF: +280 lots (93% of limit)
Aggregate: +650 lots → LIMIT BREACH
Action required: Reduce delta
```

**Gamma/Vega Limits (for option books):**
```
Gamma: Max $50,000 P&L per $1 move
Vega: Max $100,000 P&L per 1% vol move
```

---

## Credit Risk Management

### Credit Assessment Process

**Step 1: Quantitative Analysis**
```
Financial Metrics:
- Revenue: $XXB
- EBITDA: $XXB
- Net Debt: $XXB
- Debt/EBITDA: X.Xx
- Interest Coverage: X.Xx
- Current Ratio: X.Xx

Credit Rating: [S&P/Moody's/Fitch]
```

**Step 2: Qualitative Assessment**
- Industry position
- Management quality
- Business model sustainability
- Geographic/political risks
- Historical payment behavior

**Step 3: Limit Setting**
```
Credit Score: [1-10 scale or letter grade]
Unsecured Limit: $XXM
Secured Limit: $XXM
Maximum Tenor: X years
Special Conditions: [LC required over $XM, etc.]
```

### Exposure Monitoring

**Daily Credit Report:**
```
Counterparty: ABC Energy Inc.
Credit Limit: $50M (unsecured)

Current Exposure:
- Physical contracts MTM: $32M
- Derivatives MTM: $8M
- Receivables outstanding: $5M
Total: $45M (90% of limit)

Potential Future Exposure (95%, 30-day): $12M
Peak Exposure (95%): $57M → EXCEEDS LIMIT

Action: Request credit support or reduce exposure
```

### Credit Mitigation Tools

**1. Letters of Credit:**
```
Structure:
- Beneficiary: Our Company
- Applicant: Counterparty
- Amount: $30M
- Bank: [Acceptable issuing bank]
- Tenor: Rolling, matches contract
- Drawing conditions: Payment default, insolvency

Effect: Converts credit risk to bank credit risk
Cost: Typically 0.5-2% per annum (borne by counterparty)
```

**2. Parent Guarantee:**
```
Guarantor: Parent Corporation (IG rated)
Guaranteed Party: Subsidiary/Affiliate counterparty
Scope: All obligations under Agreement
Cap: Unlimited or specified amount
```

**3. Collateral/Margin:**
```
Initial Margin: Posted at trade inception
Variation Margin: Daily settlement of MTM changes
Threshold: Exposure level before margin required
Minimum Transfer: Smallest margin call amount

Example:
Threshold: $5M
Exposure: $12M
Margin Call: $7M
```

### Netting Agreements

**Master Netting:**
- Aggregate exposures across transactions
- Net settlement on termination
- Reduces gross exposure significantly

**ISDA Master Agreement:**
- Standard derivative documentation
- Close-out netting provisions
- Cross-default triggers
- Credit support annex (CSA)

---

## Operational Risk Management

### Process Controls

**Trade Execution:**
| Control | Description |
|---------|-------------|
| Four-eyes principle | Dual approval for large trades |
| Trade limits | Size/value thresholds by authority |
| Recording | Voice recording, chat archives |
| Confirmation | Written confirmation within 24 hours |

**Trade Capture:**
| Control | Description |
|---------|-------------|
| Same-day entry | Trades booked on execution date |
| Reconciliation | Front-to-back matching |
| Break resolution | Timely investigation of differences |
| System access | Role-based permissions |

### Shipping/Logistics Controls

**Scheduling:**
- Dual verification of nominations
- Confirmation protocols
- Contingency planning

**Operations:**
- Pre-arrival checklists
- Quality verification procedures
- Incident reporting requirements

### Technology Risk

**System Requirements:**
- Trading system availability (99.9%+)
- Market data feeds
- Position management
- Risk calculations
- Reporting

**Disaster Recovery:**
- Backup systems
- Geographic redundancy
- Recovery time objectives
- Business continuity plans

---

## Regulatory Risk Management

### Compliance Framework

**Key Regulations:**

| Regulation | Jurisdiction | Requirements |
|------------|--------------|--------------|
| Dodd-Frank | US | Swap reporting, clearing, position limits |
| EMIR | EU | Derivative reporting, clearing |
| MiFID II | EU | Position limits, reporting |
| MAR | EU | Market abuse prevention |
| REMIT | EU | Wholesale energy market integrity |

### Position Limits

**CFTC (US):**
- Spot month limits
- Single month limits
- All months combined limits
- Exemptions for bona fide hedging

**Example Limits:**
```
JKM (CME) Position Limits:
Spot month: 1,000 contracts (accountability)
Single month: 5,000 contracts
All months: 10,000 contracts

Exemption: Bona fide hedge exemption available
Documentation: Hedge details, underlying exposure
```

### Sanctions Compliance

**Key Considerations:**
- Counterparty screening
- Country/territory restrictions
- Vessel/shipping restrictions
- Payment routing

**Russia-Related Restrictions:**
- Export/import prohibitions
- Price caps on petroleum products
- Shipping/insurance restrictions
- Individual/entity sanctions

---

## Risk Governance

### Three Lines of Defense

**First Line: Business**
- Risk owners
- Day-to-day risk management
- Policy adherence

**Second Line: Risk/Compliance**
- Independent oversight
- Policy development
- Monitoring and reporting

**Third Line: Internal Audit**
- Independent assurance
- Control testing
- Process review

### Risk Committee Structure

**Board Risk Committee:**
- Risk appetite setting
- Major policy approval
- Strategic risk oversight

**Management Risk Committee:**
- Policy implementation
- Limit monitoring
- Exception approval

**Trading Risk Committee:**
- Daily risk review
- Position limits
- New product approval

### Risk Appetite Statement

**Example:**
```
LNG Trading Risk Appetite

Market Risk:
- 95% 1-day VaR shall not exceed $5M
- Stress test losses shall not exceed $25M
- No single position > 10% of portfolio delta

Credit Risk:
- Maximum single counterparty exposure: $100M
- Average portfolio credit quality: BBB or better
- Unsecured exposure to sub-IG: < 15% of total

Operational Risk:
- System availability target: 99.9%
- Trade confirmation within 24 hours: 100%
- Break resolution within 48 hours: 95%
```

---

## Risk Reporting

### Daily Reports

**Contents:**
- Position summary
- P&L (realized and unrealized)
- VaR and limit utilization
- Credit exposure summary
- Key risk metrics
- Limit breaches

### Weekly Reports

**Contents:**
- Detailed position analysis
- Hedge effectiveness review
- Credit portfolio review
- Market outlook impact
- Stress test results

### Monthly Reports

**Contents:**
- Comprehensive risk review
- Performance attribution
- Limit breach summary
- Risk appetite metrics
- Regulatory reporting status

---

**Next**: [[09-LNG-Trading-Strategies]] - Advanced trading approaches
