# Physical LNG Trading

Physical LNG trading involves the actual purchase, sale, and delivery of LNG cargoes. This is the foundation of the LNG market upon which all derivative activity is built.

---

## Types of Physical Transactions

### 1. Long-Term Contracts (LTCs)

**Characteristics:**
- Duration: 10-25 years (historically 20+, now trending shorter)
- Volume: Typically 1-5 MTPA per contract
- Pricing: Oil-indexed, hub-indexed, or hybrid
- Flexibility: Limited, with some volume tolerance
- Destination: Historically restricted, now often flexible

**Purpose:**
- Underpin project financing (bankability)
- Secure supply/demand for large investments
- Risk mitigation for both parties

**Key Contract Elements:**
- Annual Contract Quantity (ACQ)
- Take-or-Pay (TOP) obligations (typically 85-95%)
- Delivery schedule (monthly/quarterly nominations)
- Price formula and review mechanisms
- Force majeure provisions
- Arbitration clauses

**Example Structure:**
```
Buyer: Major Asian Utility
Seller: LNG Project Developer
Volume: 2.0 MTPA
Term: 15 years
Pricing: 14.5% × JCC (Japan Crude Cocktail)
Take-or-Pay: 90%
Delivery: DES to Buyer's Terminal
```

### 2. Medium-Term Contracts

**Characteristics:**
- Duration: 3-10 years
- More flexibility on volume/timing
- Often portfolio optimization tools
- Mix of pricing mechanisms

**Use Cases:**
- Bridging between long-term contracts
- Testing new supply sources
- Managing demand uncertainty
- Portfolio balancing

### 3. Spot & Short-Term Trading

**Definition:** Contracts for delivery within 1-2 years, often within 90 days

**Market Share:** ~35-40% of global LNG trade (growing from <10% in 2005)

**Characteristics:**
- Single cargo or small cargo series
- Market-based pricing (typically JKM, TTF-linked)
- High flexibility on delivery window
- Quick execution (days to weeks)

**Spot Trading Cycle:**
1. Cargo becomes available (production surplus, cargo diversion, resale)
2. Seller markets cargo (direct, broker)
3. Buyer evaluates fit (terminal slot, demand, price)
4. Negotiation and term sheet
5. Contract execution (often on industry templates)
6. Nomination and scheduling
7. Loading, shipping, discharge
8. Payment and title transfer

---

## FOB vs. DES Transactions

### FOB (Free On Board)

**Seller Responsibilities:**
- Deliver LNG to loading port
- Load onto vessel at loadport
- Risk transfers at ship's rail

**Buyer Responsibilities:**
- Charter/provide vessel
- All shipping costs and risks
- Insurance during voyage
- Unloading at destination

**Advantages for Buyer:**
- Full destination flexibility
- Control over shipping
- Arbitrage opportunities
- Timing flexibility

**Common FOB Sources:**
- US Gulf Coast (most US projects)
- Some Australian projects
- Portfolio player sales

### DES/DAP (Delivered Ex-Ship / Delivered At Place)

**Seller Responsibilities:**
- All logistics to destination
- Shipping costs and risks
- Deliver to buyer's terminal

**Buyer Responsibilities:**
- Accept cargo at terminal
- Unloading operations
- Risk transfers at discharge

**Advantages for Buyer:**
- Simpler logistics
- No shipping exposure
- Known delivered cost

**Common DES Sources:**
- Qatar (historically)
- Asian project-to-utility trades
- New market entrants preferring simplicity

---

## Contract Pricing Mechanisms

### Oil-Indexed Pricing

**Formula Structure:**
```
LNG Price ($/MMBtu) = Slope × Oil Price Index + Constant
```

**Common Indices:**
- **JCC (Japan Crude Cocktail)**: Average CIF import price to Japan
- **Brent**: ICE Brent crude benchmark
- **WTI**: Less common for LNG

**Typical Slopes:**
| Slope | Approximate Ratio | Context |
|-------|-------------------|---------|
| 17.2% | Full oil parity | Historical baseline |
| 14-15% | Standard range | Most traditional contracts |
| 12-13% | Discount to oil | Buyer-favorable |
| 10-11% | Significant discount | Competitive markets |

**Example Calculation:**
```
JCC = $80/bbl
Slope = 14.5%
Constant = $0.50

Price = 0.145 × $80 + $0.50 = $12.10/MMBtu
```

**S-Curve Mechanism:**
- Price caps and floors to limit exposure
- Slope varies at different oil price ranges
```
If JCC < $50: Slope = 12%
If $50 ≤ JCC ≤ $100: Slope = 14%
If JCC > $100: Slope = 11%
```

### Hub-Based Pricing

**Key Benchmarks:**
| Hub | Region | Unit | Characteristics |
|-----|--------|------|-----------------|
| JKM (Japan Korea Marker) | Asia | $/MMBtu | Platts-assessed, spot reference |
| TTF (Title Transfer Facility) | Europe | €/MWh | Netherlands hub, most liquid |
| NBP (National Balancing Point) | UK | p/therm | Historic European benchmark |
| Henry Hub | US | $/MMBtu | US domestic gas, LNG export base |

**US LNG Export Pricing:**
```
Delivered Price = Henry Hub + Liquefaction Fee + Shipping
Example: $3.50 + $2.50 + $1.50 = $7.50/MMBtu to Europe
```

**Tolling Arrangements:**
- Buyer provides feed gas (or buys at Henry Hub)
- Pays fixed liquefaction fee (~$2.00-3.50/MMBtu)
- Takes title to LNG
- Responsible for shipping and marketing

### Hybrid Pricing

**Structure:** Combination of oil-indexed and hub-indexed components

**Example:**
```
50% × (14.5% × JCC) + 50% × JKM
```

**Purpose:**
- Risk diversification
- Transition from oil to hub pricing
- Reflecting cost structure

---

## Trading Documentation

### Heads of Agreement (HOA)

**Purpose:** Non-binding preliminary agreement outlining key terms

**Typical Contents:**
- Volume and term
- Pricing framework
- Delivery basis
- Key conditions precedent
- Exclusivity period
- Confidentiality

### Sale and Purchase Agreement (SPA)

**Purpose:** Binding commercial contract for LNG sale

**Key Sections:**
1. **Definitions**: Precise terminology
2. **Quantity**: ACQ, downward/upward flexibility, make-up/carry-forward
3. **Quality**: Specifications, heating value, Wobbe Index
4. **Scheduling**: Nomination procedures, delivery windows
5. **Pricing**: Formula, adjustments, review mechanisms
6. **Delivery**: FOB/DES terms, title/risk transfer
7. **Measurement**: Procedures, disputes
8. **Invoicing & Payment**: Timing, currency, security
9. **Force Majeure**: Definition, consequences
10. **Default & Termination**: Events, remedies
11. **Liability**: Limitations, indemnities
12. **Dispute Resolution**: Arbitration rules, venue
13. **Governing Law**: Typically English or New York
14. **Amendments & Assignments**: Change mechanisms

### Master Sales Agreements (MSAs)

**Purpose:** Framework for multiple transactions

**Benefit:** Streamlined execution for repeat trading

**Common Templates:**
- GIIGNL General Terms and Conditions
- EFET (European Federation of Energy Traders)
- Customized bilateral masters

### Confirmation/Trade Capture

**For Spot Trades:**
- Simplified documentation referencing MSA
- Key terms: cargo, dates, price, delivery point
- Often via email exchange with legal confirmation

---

## Physical Trading Operations

### Nomination Process

**Timeline (Typical):**
| Stage | Timing | Action |
|-------|--------|--------|
| Annual Program | Year ahead | Preliminary delivery schedule |
| Quarterly Nomination | 90 days prior | Confirm quarterly volumes |
| Monthly Nomination | 45-60 days prior | Specify lifting windows |
| Cargo Nomination | 20-30 days prior | Name vessel, precise dates |
| Arrival Notice | 72-96 hours | ETA confirmation |

### Scheduling Coordination

**Stakeholders:**
- Seller's scheduling team
- Buyer's scheduling team
- Terminal operators (load/discharge)
- Shipping company
- Ship master
- Port authorities

**Key Documents:**
- Notice of Readiness (NOR)
- Loading/Discharge Port Schedule
- Ship-Shore Compatibility Assessment
- Cargo Documentation Package

### Quality Management

**LNG Specifications (Typical Ranges):**
| Parameter | Typical Spec |
|-----------|--------------|
| Gross Heating Value | 1,050-1,150 Btu/scf |
| Wobbe Index | 1,250-1,400 Btu/scf |
| Methane Content | >85% |
| CO₂ | <50 ppm |
| H₂S | <4 ppm |
| Nitrogen | <1.5% |
| C5+ | <0.1% |

**Quality Issues:**
- Rich vs. lean LNG (heating value differences)
- Nitrogen content (refrigeration compatibility)
- Heavy hydrocarbon content (flammability, storage)
- Off-spec consequences: rejection, price adjustment, blending

### Measurement & Title Transfer

**Custody Transfer:**
- Occurs at ship's manifold (FOB) or receiving terminal (DES)
- Based on tank measurements before/after
- Independent surveyor verification
- Adjustments for heel, boil-off, density

**Documentation:**
- Certificate of Origin
- Certificate of Quality
- Bill of Lading
- Quantity Certificate
- Surveyor's Report

---

## Portfolio Management

### Portfolio Player Strategies

**Major Portfolio Players:**
- Shell
- TotalEnergies
- BP
- Chevron
- ExxonMobil
- Trafigura
- Vitol
- Gunvor

**Portfolio Activities:**
1. **Aggregation**: Combining multiple supply sources
2. **Disaggregation**: Breaking large volumes into smaller sales
3. **Geographic arbitrage**: Directing cargoes to highest value markets
4. **Time arbitrage**: Optimizing delivery timing
5. **Quality blending**: Mixing rich/lean cargoes
6. **Logistics optimization**: Fleet/terminal efficiency
7. **Derivative hedging**: Managing price exposure

### Optimization Decisions

**Daily/Weekly:**
- Cargo destination decisions
- Shipping route optimization
- Spot market participation
- Derivative position adjustments

**Monthly/Quarterly:**
- Contract nomination optimization
- Storage strategy
- Forward hedging updates
- Fleet positioning

**Annual:**
- Portfolio composition review
- New contract negotiations
- Project participation decisions
- Long-term strategy adjustments

---

## Physical Trading Risks

### Operational Risks

| Risk | Description | Mitigation |
|------|-------------|------------|
| Terminal unavailability | Maintenance, weather, congestion | Schedule flexibility, alternative ports |
| Vessel delays | Mechanical issues, weather, canal queues | Buffer time, alternative vessels |
| Quality rejection | Off-spec cargo | Pre-shipment testing, blending |
| Force majeure | Natural disasters, political events | Contractual protections, insurance |
| Counterparty default | Non-payment, non-delivery | Credit analysis, security, guarantees |

### Market Risks

| Risk | Description | Mitigation |
|------|-------------|------------|
| Price risk | Adverse price movements | Hedging with derivatives |
| Basis risk | Price differential changes | Basis swaps, spread hedges |
| Volume risk | Take-or-pay obligations | Flexibility, make-up provisions |
| FX risk | Currency exposure | Currency hedges |

### Credit Risk Management

**Assessment Factors:**
- Credit rating (S&P, Moody's, Fitch)
- Financial statements analysis
- Payment history
- Sovereign risk (state-owned entities)
- Market reputation

**Credit Support:**
- Parent company guarantees
- Letters of credit (LC)
- Bank guarantees
- Prepayment
- Credit insurance
- Collateral/margin

---

## Physical Trading Example: Spot Cargo Transaction

### Scenario
**Date:** January 15
**Situation:** Asian utility needs additional cargo for late February due to cold weather forecast

### Step 1: Inquiry
Buyer contacts brokers and direct counterparties:
```
"Looking for 1 DES cargo, Futtsu Terminal, Japan
Delivery window: Feb 20-28
Volume: ~65,000 tonnes
Specs: Standard JCC compatible"
```

### Step 2: Offers Received
| Seller | Source | Price | Delivery |
|--------|--------|-------|----------|
| Shell | Portfolio (US origin) | JKM + $0.15 | Feb 22-26 |
| Trafigura | Atlantic diversion | JKM flat | Feb 24-28 |
| QatarEnergy | Al Khuwair loading | JKM - $0.10 | Feb 20-24 |

### Step 3: Evaluation
- Price comparison at forward JKM (~$14.50/MMBtu)
- Shipping reliability assessment
- Quality compatibility
- Counterparty credit
- Terminal slot availability

### Step 4: Negotiation & Execution
Selected: QatarEnergy offer
- Final price: JKM (Feb) - $0.10/MMBtu
- Volume: 65,500 tonnes ± 5%
- Window: Feb 21-25
- Terms: Standard GIIGNL, English law

### Step 5: Execution to Delivery
- Jan 18: Confirmation signed
- Feb 1: Vessel nominated (Al Hamra)
- Feb 10: Loading at Ras Laffan
- Feb 21: Arrival Futtsu, NOR tendered
- Feb 22: Discharge completed
- Feb 25: Final quantity/quality certificates
- Mar 5: Invoice issued
- Mar 20: Payment received

### Step 6: P&L Calculation
```
Purchase: 65,500 tonnes × 48.7 × ($14.50 - $0.10) = $45.9 million
Sale to downstream: Internal at JKM = $46.2 million
Gross margin: ~$0.3 million
Plus: Delivered cost below alternative supply
```

---

**Next**: [[03-LNG-Derivatives-and-Speculative-Trading]] - Financial instruments and spec trading
