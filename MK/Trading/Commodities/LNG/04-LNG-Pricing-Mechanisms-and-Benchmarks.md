# LNG Pricing Mechanisms & Benchmarks

Understanding pricing mechanisms is fundamental to LNG trading. This chapter provides comprehensive coverage of how LNG is priced globally.

---

## The Three Pillars of LNG Pricing

### 1. Oil-Linked Pricing (Traditional Asian Model)

**Historical Context:**
- Originated in 1970s Japan
- Natural gas lacked independent benchmark
- Oil seen as competing fuel in power generation
- Long-term contracts required stable, understood reference

**JCC (Japan Crude Cocktail)**

**Definition:** The average CIF (Cost, Insurance, Freight) import price of crude oil into Japan, published monthly by the Japanese government.

**Composition:**
- Weighted average of all crude imports
- Dominated by Middle Eastern grades
- Represents actual delivered cost to Japanese refiners

**Publication:**
- Released monthly by Ministry of Finance
- ~6-week lag (January JCC released mid-February)
- Used in 3-month or 6-month trailing averages for LNG

**Price Formula Structure:**
```
LNG Price ($/MMBtu) = a × JCC ($/bbl) + b

Where:
a = slope coefficient (typically 0.1000-0.1720)
b = constant (typically -$0.50 to +$1.00)
```

**Slope Analysis:**
| Slope | Meaning | Market Context |
|-------|---------|----------------|
| 17.2% | Thermal parity | Oil and gas equal $/energy |
| 15.0% | Historical norm | Pre-2010 long-term contracts |
| 14.0% | Balanced market | 2010-2015 new contracts |
| 12.5% | Buyer-favorable | Post-2015 competition |
| 10-11% | Deep discount | Very competitive/distressed |

**Example Calculations:**
```
Scenario 1 (Standard):
JCC = $80/bbl, Slope = 14.5%, Constant = $0.00
Price = 0.145 × $80 = $11.60/MMBtu

Scenario 2 (With S-Curve):
If JCC < $60: Slope = 12.5%
If $60 ≤ JCC ≤ $100: Slope = 14.5%
If JCC > $100: Slope = 11.0%

JCC = $110/bbl
Price = (0.125 × $60) + (0.145 × $40) + (0.11 × $10) = $14.40/MMBtu
```

**Brent Linkage:**

Some contracts use Brent crude instead of JCC:
- More liquid benchmark
- Closer to real-time pricing
- Common for European/Atlantic Basin contracts

```
Price = 0.14 × Brent + $0.50
```

**Advantages of Oil Indexation:**
- Price stability and predictability
- Bankable for project financing
- Understood by all parties
- Low basis risk for sellers with oil exposure

**Disadvantages:**
- Disconnected from gas supply/demand
- Lagging price adjustment
- Potential for extreme divergence (2014-2015, 2020-2022)

---

### 2. Hub-Based Pricing (Gas-on-Gas Competition)

**Philosophy:** LNG priced against traded gas benchmarks reflecting actual supply/demand

#### JKM (Japan Korea Marker)

**Definition:** Platts assessment of spot LNG delivered to Japan, South Korea, China, and Taiwan

**Assessment Methodology:**
- Assessed daily by S&P Global Platts
- Reflects cargoes arriving 1-2 months forward
- MOC (Market-on-Close) process 4:00-4:30 PM Singapore

**Key Specifications:**
| Parameter | Specification |
|-----------|---------------|
| Basis | DES Northeast Asia |
| Delivery Window | 15-45 days forward |
| Cargo Size | Standard (125,000-174,000 m³) |
| Quality | Standard LNG specs |
| Currency | US Dollars |
| Unit | Per MMBtu |

**JKM Assessment Process:**
1. Platts collects market data throughout day
2. Traders submit bids/offers during MOC window
3. Transactions at market levels confirm price
4. Platts publishes daily assessment post-close

**JKM Variants:**
- **JKM M1, M2, M3**: Specific month assessments
- **JKM Swap**: Forward month assessments
- **JKM Derivative**: Futures settlement reference

#### TTF (Title Transfer Facility)

**Definition:** Dutch natural gas trading hub, the most liquid in Europe

**Market Characteristics:**
| Metric | Value |
|--------|-------|
| Annual Volume Traded | ~40,000 TWh (notional) |
| Physical Throughput | ~800-1,000 TWh/year |
| Churn Rate | ~40-50x |
| Forward Curve | Out to 5+ years liquid |

**TTF Relevance to LNG:**
- European destination benchmark
- LNG competes with pipeline gas at TTF
- Northwest Europe regas terminals price vs. TTF
- Key arbitrage reference

**Quote Convention:**
- €/MWh (primary)
- Convert to $/MMBtu: (€/MWh ÷ 3.412) × EUR/USD

#### NBP (National Balancing Point)

**Definition:** UK virtual gas trading hub

**Characteristics:**
- Historically primary European benchmark
- Declining relevance vs. TTF
- Still referenced in legacy contracts
- Quoted in pence/therm

**Conversion:**
```
p/therm to $/MMBtu = (p/therm × 10 ÷ 100) × GBP/USD
Example: 100 p/therm = £1.00/therm = $1.25/therm = $12.50/MMBtu (at 1.25 GBP/USD)
```

#### Henry Hub

**Definition:** Louisiana-based physical delivery point for NYMEX natural gas futures

**Role in LNG:**
- US domestic gas price
- Base for US LNG export pricing
- FOB Gulf Coast reference

**US LNG Export Pricing Model:**
```
Delivered Price = Henry Hub + Liquefaction Fee + Shipping

Example (to Asia):
Henry Hub: $3.50/MMBtu
Liquefaction: $2.50/MMBtu
Shipping: $1.80/MMBtu (US Gulf to Japan)
Delivered Cost: $7.80/MMBtu
```

---

### 3. Hybrid Pricing

**Definition:** Combinations of oil-indexed and hub-indexed components

**Common Structures:**

**Structure 1: Weighted Average**
```
Price = 50% × (0.145 × JCC) + 50% × JKM
```

**Structure 2: Collar with Hub Floor/Cap**
```
Base: 14.5% × JCC
Floor: Max(Base, JKM - $1.00)
Cap: Min(Base, JKM + $1.00)
```

**Structure 3: Oil with Hub Reopener**
```
Base: 14.5% × JCC
If JKM diverges >$3 from Base for 3 months: Price review triggered
```

**Purpose:**
- Risk diversification
- Transition mechanism
- Reflecting mixed cost structure

---

## Benchmark Deep Dive: JKM

### JKM Price Discovery

**Information Sources:**
1. Physical cargo fixtures
2. Paper swap/futures trades
3. Broker indications
4. Market participant inquiries
5. Platts editorial assessment

**Quality of Information Hierarchy:**
```
Confirmed trade > Firm bid/offer > Indicative quote > Editorial assessment
```

**Factors Affecting JKM:**

| Category | Factor | Impact on JKM |
|----------|--------|---------------|
| Demand | Cold weather Asia | ↑ |
| Demand | Nuclear restart Japan | ↓ |
| Demand | China LNG demand | ↑ |
| Supply | US Gulf hurricane | ↑ |
| Supply | New project startup | ↓ |
| Supply | Unplanned outage | ↑ |
| Shipping | Freight rates up | ↑ |
| Shipping | Panama Canal congestion | ↑ (Atlantic cargoes) |
| Arb | TTF spike | ↓ (cargoes diverted to Europe) |
| Inventory | Asian tank levels low | ↑ |

### JKM Seasonality

**Monthly Patterns (Historical Averages):**

| Month | Pattern | Driver |
|-------|---------|--------|
| Jan | Peak prices | Winter heating demand |
| Feb | High, declining | Late winter, shoulder approaching |
| Mar | Declining | Heating demand waning |
| Apr-May | Lows | Shoulder season, maintenance |
| Jun | Rising | Pre-summer stocking |
| Jul-Aug | Elevated | Summer cooling (Japan AC demand) |
| Sep | Declining | Summer end |
| Oct-Nov | Rising | Pre-winter preparation |
| Dec | High | Early winter, holiday stocking |

**Seasonal Spread History:**
- Q1-Q3 spread typically $3-6/MMBtu
- Can collapse in mild winters
- Can explode to $10+ in cold winters

### JKM Forward Curve Dynamics

**Contango (Upward Sloping):**
- Future prices higher than prompt
- Normal in shoulder seasons
- Reflects storage costs, time value

**Backwardation (Downward Sloping):**
- Prompt premium to forward
- Indicates tight current supply
- Common in demand peaks

**Curve Shape Signals:**
```
Steep Contango: Market expects future tightness
Steep Backwardation: Current crisis, future relief expected
Flat Curve: Balanced market, stable outlook
```

---

## Benchmark Deep Dive: TTF

### TTF Market Structure

**Participants:**
- Producers (Equinor, Shell, Gazprom historically)
- Utilities (E.ON, RWE, EDF)
- Industrial consumers
- Portfolio players/traders
- Financial participants

**Trading Venues:**
- ICE Endex (primary)
- EEX (European Energy Exchange)
- OTC bilateral

### TTF Price Drivers

| Factor | Impact |
|--------|--------|
| Russian pipeline flows | Major historical driver |
| Norwegian production | Key alternative supply |
| LNG arrivals | Balancing flow |
| Wind/solar generation | Reduces gas demand |
| Temperature | Heating demand |
| Industrial activity | Baseline demand |
| Storage levels | Buffer/pressure indicator |

### TTF Forward Curve

**Characteristics:**
- Most liquid gas curve globally
- Trades out 5+ years with reasonable liquidity
- Quarterly and calendar year strips common

**Curve Products:**
| Product | Description |
|---------|-------------|
| DA (Day Ahead) | Next gas day |
| Weekend | Friday-Sunday |
| WD (Within Day) | Same day trading |
| Month Ahead | M+1, M+2, etc. |
| Quarter | Q+1, Q+2, etc. |
| Season | Summer/Winter strips |
| Calendar Year | Cal 25, Cal 26, etc. |

---

## Arbitrage Pricing Relationships

### JKM-TTF Arbitrage

**Physical Arbitrage Logic:**
```
If JKM > TTF + Shipping (to Asia) + Transaction costs:
  → Cargoes flow from Atlantic to Asia
  → TTF rises (less supply)
  → JKM falls (more supply)
  → Spread compresses

If TTF > JKM + Shipping (to Europe) + Transaction costs:
  → Asian cargoes diverted to Europe
  → JKM rises (less supply)
  → TTF falls (more supply)
  → Spread compresses
```

**Arbitrage Cost Components:**
| Route | Shipping | Canal | Total (~days) |
|-------|----------|-------|---------------|
| US Gulf to NW Europe | $0.50-1.00 | - | ~10-14 days |
| US Gulf to Japan | $1.50-2.50 | Panama (~$1M) | ~25-35 days |
| Qatar to NW Europe | $1.00-1.50 | Suez (~$0.5M) | ~12-15 days |
| Qatar to Japan | $0.50-1.00 | - | ~10-14 days |

### JKM-Henry Hub Arbitrage

**Net-Back Calculation:**
```
Asian Net-Back to US Producer:
JKM - Shipping - Regas costs - Liquefaction = Net-Back

If Net-Back > Henry Hub:
  → US exports attractive
  → Henry Hub supported
  → Arbitrage window open

If Net-Back < Henry Hub:
  → US exports marginal/unprofitable
  → Cargo cancellations possible
  → Henry Hub pressured
```

**US LNG Export Economics (Example):**
```
JKM: $12.00/MMBtu
Shipping: $1.50
Panama Canal: $0.30
Regas/port: $0.20
Liquefaction (variable): $1.00
Total cost: $3.00

Net-Back: $12.00 - $3.00 = $9.00/MMBtu

Henry Hub: $3.50/MMBtu
Spread to Net-Back: $5.50/MMBtu
Less fixed liq fee: $2.50/MMBtu
Margin: $3.00/MMBtu ✓ Profitable
```

---

## Price Assessments & Reporting Agencies

### S&P Global Platts

**Key Assessments:**
| Assessment | Description |
|------------|-------------|
| JKM | Northeast Asia spot |
| DES Japan | Japan-specific |
| DES China | China-specific |
| FOB Atlantic | US Gulf, Trinidad |
| FOB Middle East | Qatar, UAE |

**Methodology:**
- Market-on-Close (MOC) process
- eWindow electronic platform
- Editor-assessed based on market activity
- Transparency through published methodology

### Argus

**Key Assessments:**
| Assessment | Description |
|------------|-------------|
| Argus NE Asia | Alternative to JKM |
| Argus DES S. Europe | Mediterranean focus |
| Argus FOB assessments | Various origins |

### ICIS

**Key Products:**
| Product | Description |
|---------|-------------|
| ICIS East Asia Index | JKM alternative |
| ICIS assessments | Various regional |
| ICIS LNG Edge | Analytics platform |

### Price Reporting Considerations

**Assessment vs. Index:**
- Assessment: Editorial judgment from market data
- Index: Mathematical calculation from transactions

**Benchmark Integrity:**
- IOSCO principles compliance
- Audit trails
- Conflicts management
- Stakeholder oversight

---

## Contract Pricing Clauses

### Price Review Mechanisms

**Purpose:** Adjust pricing when market conditions change materially

**Triggers:**
- Calendar-based (every 3-5 years)
- Market-based (if prices diverge from threshold)
- Economic hardship claims

**Process:**
1. Notice of review request
2. Good faith negotiation period (60-90 days)
3. Expert determination option
4. Arbitration as backstop

**Typical Review Clause:**
```
"Either party may request a price review if:
(a) 3 years have elapsed since last review, OR
(b) The Contract Price has diverged from the Market Reference
    by more than 15% for 3 consecutive months."
```

### Price Reopener Outcomes

**Historical Examples:**
- 2014-2016: Asian buyers renegotiated slopes downward
- 2018-2019: Some sellers sought increases
- 2021-2022: Buyers with oil linkage benefited during spike

### Price Floor/Ceiling Mechanisms

**Floor (Seller Protection):**
```
Price = Max(Formula Price, $6.00/MMBtu)
```

**Ceiling (Buyer Protection):**
```
Price = Min(Formula Price, $20.00/MMBtu)
```

**S-Curve (Both):**
```
Base Slope: 14.5%

Oil Price Ranges:
$0-60: Slope = 12% (protects buyer at high prices)
$60-100: Slope = 14.5% (normal range)
$100+: Slope = 11% (caps buyer upside)
```

---

## Pricing Trends & Market Evolution

### Shift from Oil to Hub Pricing

**Market Share Evolution:**
| Year | Oil-Indexed | Hub/Hybrid | Spot/Short-Term |
|------|-------------|------------|-----------------|
| 2005 | ~85% | ~5% | ~10% |
| 2010 | ~75% | ~10% | ~15% |
| 2015 | ~65% | ~15% | ~20% |
| 2020 | ~50% | ~20% | ~30% |
| 2024 | ~40% | ~25% | ~35% |

### Drivers of Hub-Based Growth

1. **US LNG exports**: Henry Hub-based pricing introduced FOB flexibility
2. **Portfolio players**: Prefer market-based pricing for optimization
3. **Asian buyer sophistication**: Seeking to capture gas market fundamentals
4. **Derivatives development**: JKM liquidity enables hedging
5. **European crisis**: Demonstrated relevance of hub pricing

### Future Pricing Outlook

**Expected Developments:**
- Continued growth of hub-linked contracts
- Asian hub development (potential Shanghai index)
- Hybrid structures becoming standard
- Oil linkage remaining for project finance
- Increased derivatives liquidity

---

**Next**: [[05-LNG-Contract-Structures-and-Terms]] - Detailed contract mechanics
