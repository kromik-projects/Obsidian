# LNG Derivatives & Speculative Trading

The LNG derivatives market has evolved dramatically, enabling sophisticated risk management and speculative opportunities beyond physical trading.

---

## Evolution of LNG Derivatives

### Historical Context
- **Pre-2010**: Minimal derivatives, illiquid OTC swaps
- **2010-2015**: Growing OTC activity, emergence of JKM
- **2015-2020**: CME, ICE launch futures; liquidity builds
- **2020-Present**: Mature derivative complex, active spec participation

### Market Maturity Indicators
| Year | JKM Futures Open Interest | Monthly Volume |
|------|---------------------------|----------------|
| 2016 | ~5,000 lots | ~10,000 lots |
| 2018 | ~20,000 lots | ~50,000 lots |
| 2020 | ~50,000 lots | ~150,000 lots |
| 2022 | ~100,000+ lots | ~300,000+ lots |
| 2024 | ~150,000+ lots | ~500,000+ lots |

---

## Key LNG Derivative Instruments

### 1. JKM Futures (Platts JKM)

**Contract Specifications (CME):**
| Attribute | Specification |
|-----------|---------------|
| Contract Size | 10,000 MMBtu (~205 tonnes LNG) |
| Quotation | $/MMBtu |
| Tick Size | $0.001/MMBtu ($10 per contract) |
| Settlement | Cash settled to Platts JKM average |
| Trading Hours | Nearly 24/5 |
| Expiry | Monthly, up to 72 months forward |

**ICE JKM Futures:**
- Similar specs, ICE platform
- Slightly different liquidity profile
- Cross-margining benefits

**Liquidity Characteristics:**
- Most liquid: Prompt month and M+1 to M+3
- Good liquidity: M+4 to M+12
- Moderate liquidity: Q+5 to Q+8 (quarterly)
- Thin liquidity: Beyond 2 years (Cal strips)

### 2. TTF Natural Gas Futures

**Relevance to LNG:**
- European gas benchmark
- LNG deliveries compete with pipeline gas
- Major arbitrage reference point

**Contract Specifications (ICE):**
| Attribute | Specification |
|-----------|---------------|
| Contract Size | 1 Therm (or MW depending on contract) |
| Quotation | €/MWh or p/therm |
| Settlement | Cash settled or physical |
| Liquidity | Highest in global gas markets |

**TTF Conversion Notes:**
- 1 MWh ≈ 3.412 MMBtu
- €40/MWh ≈ $12.80/MMBtu (at €1 = $1.10)

### 3. Henry Hub Natural Gas Futures

**Primary Use:**
- US domestic gas benchmark
- US LNG export cost basis
- Arbitrage calculations

**Contract Specifications (CME/NYMEX):**
| Attribute | Specification |
|-----------|---------------|
| Contract Size | 10,000 MMBtu |
| Quotation | $/MMBtu |
| Settlement | Physical delivery at Henry Hub |
| Liquidity | Extremely high, global benchmark |

### 4. JKM-TTF Spread (Intercontinental Spread)

**Purpose:** Trade the Asia-Europe price differential

**Structure:**
```
Long JKM / Short TTF = Bullish Asia vs. Europe
Short JKM / Long TTF = Bearish Asia vs. Europe
```

**Key Drivers:**
- Relative demand in Asia vs. Europe
- Shipping economics (Atlantic vs. Pacific routes)
- Seasonal patterns in both regions
- Supply disruptions affecting one region

**Typical Range:**
- Contango: JKM $2-5 premium to TTF (normal)
- Extreme: JKM $10-30+ premium (2022 crisis)
- Inverted: TTF premium to JKM (unusual, late 2022)

### 5. JKM-Henry Hub Spread

**Purpose:** Trade Asian price vs. US export economics

**Structure:**
```
Net-back calculation:
JKM - Henry Hub - Liquefaction - Shipping = Margin
```

**Typical Breakeven:**
- Liquefaction: $2.00-3.50/MMBtu
- Shipping (US Gulf to Asia): $1.00-3.00/MMBtu
- Total cost: $3.50-6.50/MMBtu

**Trade Logic:**
- If JKM > HH + $6: US exports profitable, support for HH
- If JKM < HH + $4: Exports marginal, less US LNG to Asia

### 6. LNG Swaps (OTC)

**Types:**
1. **Fixed-for-Floating Swaps**: Exchange fixed price for JKM/TTF floating
2. **Basis Swaps**: JKM vs. TTF, JKM vs. Brent, etc.
3. **Index Swaps**: JCC-linked vs. hub-linked
4. **Location Swaps**: Different delivery point pricing

**OTC Swap Terms (Example):**
```
Notional: 500,000 MMBtu/month
Term: 6 months (Jan-Jun)
Fixed leg: $12.50/MMBtu
Floating leg: Platts JKM (monthly average)
Settlement: Cash, 5 business days after month-end
```

### 7. LNG Options

**Types:**
1. **Calls**: Right to buy at strike price
2. **Puts**: Right to sell at strike price
3. **Collars**: Simultaneous call sale/put purchase (or vice versa)
4. **Spreads**: Combination strategies

**Option Uses in LNG:**
- Upside protection for buyers (calls)
- Downside protection for sellers (puts)
- Premium reduction strategies (collars)
- Volatility trading
- Structured contract hedging

**Example Collar:**
```
Buyer Protection Collar:
- Buy JKM call at $15/MMBtu (Q1 expiry)
- Sell JKM put at $10/MMBtu (Q1 expiry)
- Net premium: ~$0.30/MMBtu paid
- Outcome: Protected above $15, exposed below $10
```

---

## Speculative Trading Strategies

### 1. Directional Trading

**Long JKM (Bullish Asia):**
- Conviction: Asian prices will rise
- Catalysts: Cold weather, supply outages, demand surge
- Execution: Buy JKM futures, hold for appreciation
- Risk: Prices decline, margin calls

**Short JKM (Bearish Asia):**
- Conviction: Asian prices will fall
- Catalysts: Mild weather, new supply, demand destruction
- Execution: Sell JKM futures
- Risk: Prices spike, unlimited loss potential

**Position Sizing:**
```
Risk Budget: $500,000
Max Loss per Trade: 2% = $10,000
JKM Volatility (daily): ~$0.50/MMBtu
Contract Risk: $5,000/lot (10,000 MMBtu × $0.50)
Max Position: 2 lots per $10,000 risk budget
```

### 2. Spread Trading

**Calendar Spreads (Time Spreads):**
```
Winter-Summer Spread:
Long Jan JKM / Short Jul JKM
Thesis: Winter demand creates seasonal premium

Execution:
Buy Jan JKM @ $14.50
Sell Jul JKM @ $11.00
Spread Entry: $3.50

Exit Target: $4.50 spread (if winter tightens)
Stop Loss: $2.50 spread (if summer strengthens)
```

**Geographic Spreads:**
```
Atlantic Arb:
Long JKM / Short TTF (units normalized)
Thesis: Asian demand outpaces Europe

Entry: $3.00/MMBtu JKM premium
Target: $5.00/MMBtu
Stop: $1.50/MMBtu
```

**Product Spreads:**
```
Crude-LNG Relationship:
Long JKM / Short Brent (energy-equivalent)
Thesis: Gas decouples from oil (upside)
Risk: Traditional correlation reasserts
```

### 3. Relative Value Trading

**JKM vs. Oil Index Relationship:**
- Traditional: JKM ≈ 14-15% × JCC
- Calculate implied oil parity
- Trade divergences from historical relationship

**Example:**
```
JCC (3-month avg): $85/bbl
Implied JKM at 14.5%: $12.33/MMBtu
Actual JKM: $14.00/MMBtu
Premium: $1.67 (13.5% above fair value)

Trade: Short JKM if expecting mean reversion
Risk: Premium expands further (demand shock)
```

### 4. Event-Driven Trading

**Weather Events:**
- Cold snaps in Northeast Asia (Jan-Feb)
- Hurricanes in US Gulf (Aug-Oct)
- Heat waves in Japan/Korea (Jul-Aug)

**Supply Events:**
- Unplanned outages (Gorgon, Sabine, Freeport incidents)
- Maintenance schedules
- Project delays/startups

**Demand Events:**
- Nuclear outages in Japan/Korea
- Economic data (industrial production)
- Policy changes (coal bans, emission rules)

**Geopolitical Events:**
- Sanctions (Russia)
- Middle East tensions (Qatar)
- Trade policy (US-China)

### 5. Volatility Trading

**Implied vs. Realized Vol:**
- Buy options when IV < realized
- Sell options when IV > realized

**Straddles/Strangles:**
```
Long Straddle:
Buy JKM $13 Call @ $0.80
Buy JKM $13 Put @ $0.70
Total Premium: $1.50
Breakeven: $11.50 or $14.50
Profit: Large moves in either direction
```

**Vol Surface Trading:**
- Trade skew (put vs. call IV)
- Trade term structure (front vs. back IV)

---

## Market Microstructure

### Liquidity Providers

**Market Makers:**
- Banks: Goldman Sachs, Morgan Stanley, Citi, Macquarie
- Trading houses: Trafigura, Vitol, Gunvor
- Integrated majors: Shell, BP, TotalEnergies

**Providing:**
- Two-way prices (bid/offer)
- Execution against customer flow
- Delta hedging of structured products

### Order Flow Dynamics

**Typical Flow:**
- Hedgers: Physical players managing exposure
- Specs: Funds, CTAs, prop traders
- Structured desks: Banks hedging client products
- Arbitrageurs: Cross-market relative value

**Information Sources:**
| Source | Timing | Use |
|--------|--------|-----|
| Platts Window | Daily 4-4:30pm Singapore | Settlement reference, flow signals |
| ICIS Assessments | Daily | Alternative price reference |
| Ship tracking | Real-time | Physical flow indicators |
| Weather | Daily/weekly | Demand forecasting |
| Exchange data | Real-time | Positioning, liquidity |

### Trading Venues

**Exchanges:**
| Exchange | Products | Characteristics |
|----------|----------|-----------------|
| CME/NYMEX | JKM, HH, spreads | Primary US venue |
| ICE | JKM, TTF, NBP | Primary European venue |
| SGX | JKM | Asian time zone liquidity |
| EEX | TTF | European competition |

**OTC Markets:**
- Broker voice markets (ICAP, Tullett, BGC)
- Electronic OTC platforms
- Direct bilateral trades

### Execution Considerations

**Slippage:**
- Front months: 1-2 ticks typical
- Deferred months: 3-10 ticks possible
- Large orders: TWAP/VWAP algorithms recommended

**Market Impact:**
```
Small order (<20 lots): Minimal impact
Medium order (20-100 lots): 2-5% price impact
Large order (100+ lots): Work order, 5-15% impact
```

---

## Risk Management for Speculative Trading

### Position Limits

**Exchange Limits:**
- Accountability levels trigger reporting
- Position limits cap single-entity holdings
- Vary by contract, month, aggregate

**Internal Limits:**
| Metric | Typical Limit |
|--------|---------------|
| Delta (directional) | $X per $0.10 move |
| Vega (volatility) | $X per 1% IV move |
| Gamma (convexity) | $X for 1% underlying move |
| Concentration | Max % in single contract |
| Liquidity | Max % of open interest |

### Greeks Management

**Delta (Δ):**
- Price sensitivity
- Primary directional risk
- Managed by futures position

**Gamma (Γ):**
- Delta sensitivity to price
- Higher near option expiry
- Managed by option positions

**Vega (ν):**
- Sensitivity to implied volatility
- Long options = long vega
- Managed by option spreads

**Theta (θ):**
- Time decay
- Costs for long option positions
- Income for short option positions

**Rho (ρ):**
- Interest rate sensitivity
- Generally minor for LNG derivatives

### P&L Attribution

**Daily P&L Breakdown:**
```
Delta P&L: Position × Price Change
Vega P&L: Vega × IV Change
Theta P&L: Theta × Days
Gamma P&L: 0.5 × Gamma × (Price Change)²
Residual: Explained by model adjustments
```

### Stress Testing

**Scenarios:**
| Scenario | JKM Move | TTF Move | Vol Change |
|----------|----------|----------|------------|
| Cold snap (Asia) | +$5 | +$2 | +20% |
| Supply outage | +$3 | +$1 | +15% |
| Demand shock | -$4 | -$2 | +10% |
| Market crash | -$6 | -$4 | +30% |
| Vol spike | ±$2 | ±$1 | +50% |

---

## Practical Trading Examples

### Example 1: Seasonal Spread Trade

**Setup (August):**
- Winter (Jan) JKM: $14.00
- Summer (Jul) JKM: $10.50
- Spread: $3.50

**Thesis:** Spread will widen as winter approaches and demand builds

**Execution:**
- Buy 50 lots Jan JKM @ $14.00
- Sell 50 lots Jul JKM @ $10.50
- Net position: Long 50 lots winter spread

**Management:**
- Initial margin: ~$2,500/lot × 50 = $125,000
- Target: Spread widens to $5.00
- Stop: Spread narrows to $2.50

**Outcome (November):**
- Jan JKM: $17.50
- Jul JKM: $11.50
- Spread: $6.00

**P&L:**
```
Entry spread: $3.50
Exit spread: $6.00
Gain: $2.50/MMBtu × 10,000 × 50 = $1,250,000
```

### Example 2: Arbitrage-Based Directional Trade

**Setup:**
- JKM: $15.00/MMBtu
- Henry Hub: $3.00/MMBtu
- US-Asia shipping: $1.50/MMBtu
- Liquefaction: $2.50/MMBtu
- Net-back: $15.00 - $1.50 - $2.50 = $11.00
- Premium over HH: $8.00/MMBtu

**Thesis:** Premium unsustainably high; arbitrage flow will compress

**Execution:**
- Short JKM futures
- Long Henry Hub futures (ratio-adjusted)

**Risk:** Asian demand spike maintains premium

### Example 3: Event-Driven Trade

**Event:** Major Australian LNG facility announces 2-week unplanned outage

**Analysis:**
- ~5 MTPA capacity offline
- ~2 cargoes worth per week affected
- Spot market tight pre-event
- Northern Hemisphere winter approaching

**Execution:**
- Buy JKM front-month futures immediately
- Size: Based on event probability and impact estimate

**Outcome:**
- JKM jumps $1.50 on news
- Held for additional $0.50 appreciation
- Exit on repair timeline clarity

---

## Regulatory Considerations

### Position Reporting

**CFTC (US):**
- Large trader reporting thresholds
- Commitment of Traders (COT) reports
- Spec position limits

**ESMA/FCA (Europe):**
- MiFID II position reporting
- Ancillary activity exemptions
- Position limits for commodity derivatives

### Market Manipulation

**Prohibited Activities:**
- Spoofing (placing orders with intent to cancel)
- Layering (creating false impression of supply/demand)
- Wash trading (self-dealing)
- Benchmark manipulation (Platts window gaming)

**Compliance:**
- Trade surveillance systems
- Communication monitoring
- Separation of physical and financial trading info

---

**Next**: [[04-LNG-Pricing-Mechanisms-and-Benchmarks]] - Deep dive into pricing
