# LNG Contract Structures & Terms

LNG contracts are among the most complex commodity agreements. This chapter provides detailed coverage of contract structures, key terms, and negotiation considerations.

---

## Contract Hierarchy

### Heads of Agreement (HOA)

**Purpose:** Non-binding preliminary agreement establishing framework for negotiations

**Typical Contents:**
- Parties and project description
- Indicative volume and term
- Pricing framework (not final formula)
- Key conditions precedent
- Exclusivity period
- Confidentiality obligations
- Negotiation timeline

**Legal Status:**
- Generally non-binding on commercial terms
- Binding on confidentiality and exclusivity
- "Agreement to negotiate in good faith"

**Duration:** 6-18 months typically

### Memorandum of Understanding (MOU)

**Similar to HOA but often:**
- More preliminary
- Less detailed
- Used for market testing
- Multiple simultaneous MOUs possible

### Sale and Purchase Agreement (SPA)

**Definition:** The binding legal contract for LNG sale

**Key Characteristics:**
- Comprehensive (100-300+ pages)
- Heavily negotiated
- Project-specific annexes
- Industry templates as starting points

---

## SPA Key Commercial Terms

### Volume Terms

**Annual Contract Quantity (ACQ):**
- Base annual volume commitment
- Stated in tonnes or MMBtu
- May be flat or ramped

**Example:**
```
Year 1-2: 1.5 MTPA (ramp-up)
Year 3-15: 2.0 MTPA (plateau)
Year 16-20: 1.5 MTPA (decline)
```

**Downward Quantity Tolerance (DQT):**
- Permitted reduction below ACQ
- Typically 5-15% of ACQ
- May require notice period

**Upward Quantity Tolerance (UQT):**
- Option to take additional volume
- Typically 5-15% of ACQ
- Subject to seller's ability to supply

**Example Flexibility:**
```
ACQ: 2.0 MTPA
DQT: 10% (can reduce to 1.8 MTPA)
UQT: 10% (can increase to 2.2 MTPA)
Effective range: 1.8 - 2.2 MTPA
```

### Take-or-Pay (TOP) Obligations

**Definition:** Buyer must pay for minimum quantity regardless of actual offtake

**Standard Range:** 85-95% of ACQ

**Calculation:**
```
ACQ: 2.0 MTPA
TOP: 90%
Minimum Take: 1.8 MTPA
If buyer takes only 1.5 MTPA:
Shortfall: 0.3 MTPA
TOP Payment: 0.3 MTPA × Contract Price
```

**TOP Payment Rights:**
- Payment gives right to future "make-up"
- Make-up period typically 3-5 years
- Subject to conditions (volume limits, scheduling)

### Make-Up and Carry-Forward

**Make-Up:**
- Recover previously paid-for but untaken volumes
- Typically limited to x% of future ACQ
- May be at reduced price or no additional cost
- Time-limited (expiry if not used)

**Example Make-Up Clause:**
```
Make-up volumes limited to 15% of ACQ per year
Must be taken within 5 years of shortfall year
Make-up taken at no additional charge
Subject to operational scheduling availability
```

**Carry-Forward:**
- Volumes taken above ACQ credited to future years
- Reduces future minimum take obligations
- Typically limited and conditional

### Delivery Terms

**Delivery Point:**
- FOB: Ship's manifold at loading port
- DES/DAP: Ship's manifold at receiving terminal
- Ex-Ship: Similar to DES, delivery at discharge

**Delivery Window:**
- Specified dates for cargo lifting/delivery
- Typically 3-5 day windows
- Demurrage for delays outside window

**Scheduling Process:**
```
Timeline for Annual Scheduling:
Y-1 (Oct): Preliminary Annual Delivery Program
Y-1 (Nov): Final Annual Delivery Program
M-60: Quarterly schedule confirmation
M-30: Monthly schedule confirmation
M-15: Cargo nomination (vessel, dates)
D-7: Final arrival/loading notice
D-3: Notice of Readiness
```

---

## Pricing Clauses (Detailed)

### Price Formula Components

**Basic Structure:**
```
P = (a × I) + b ± Adjustments

Where:
P = Contract price ($/MMBtu)
a = Slope/coefficient
I = Index (JCC, Brent, JKM, HH)
b = Constant
Adjustments = Quality, location, other
```

### Oil-Indexed Formula Examples

**Simple Linear:**
```
P = 0.145 × JCC
At JCC = $80: P = $11.60/MMBtu
```

**With Constant:**
```
P = 0.145 × JCC + $0.50
At JCC = $80: P = $12.10/MMBtu
```

**S-Curve (Kinked):**
```
If JCC ≤ $60: P = 0.125 × JCC + $1.00
If $60 < JCC ≤ $100: P = 0.145 × JCC
If JCC > $100: P = 0.11 × JCC + $3.50

At JCC = $50: P = 0.125 × $50 + $1.00 = $7.25
At JCC = $80: P = 0.145 × $80 = $11.60
At JCC = $120: P = 0.11 × $120 + $3.50 = $16.70
```

**Floor and Ceiling:**
```
P = Max(Min(0.145 × JCC, $18.00), $6.00)
Floor: $6.00/MMBtu
Ceiling: $18.00/MMBtu
```

### Hub-Indexed Formula Examples

**JKM Linkage:**
```
P = JKM (M) + Adjustment
Where M = delivery month
Adjustment may be premium/discount
```

**TTF Linkage (European delivery):**
```
P = TTF (M) × EUR/USD / 3.412
Converts €/MWh to $/MMBtu
```

**Henry Hub + Cost Stack:**
```
P = HH (M) + $2.50 (liquefaction) + $0.15 (other)
Often for tolling-style arrangements
```

### Hybrid Formulas

**Weighted Average:**
```
P = 0.5 × (0.145 × JCC) + 0.5 × JKM
Equal weighting oil and hub
```

**Oil with Hub Collar:**
```
Base = 0.145 × JCC
Floor = JKM - $2.00
Ceiling = JKM + $2.00
P = Max(Min(Base, Ceiling), Floor)
```

### Price Adjustment Mechanisms

**Quality Adjustment:**
```
Base price for 1,100 Btu/scf GHV
Adjustment: ±$0.01 per 10 Btu/scf deviation
```

**Currency Adjustment:**
- For contracts priced in non-USD
- Typically using specified exchange rates

**Inflation Adjustment:**
- Annual escalation of constants
- Based on CPI or other indices

---

## Term and Duration

### Contract Length Trends

| Era | Typical Term | Rationale |
|-----|--------------|-----------|
| 1970s-1990s | 20-25 years | Project finance requirements |
| 2000s | 15-20 years | Balanced approach |
| 2010s | 10-15 years | Buyer flexibility demands |
| 2020s | 5-15 years | Market maturation, varied |

### Extension Options

**Buyer Extension:**
```
Buyer may extend term by 5 years with 24 months notice
Extension price: Market-based renegotiation or formula
```

**Seller Extension:**
```
Less common
May be mutual option
```

### Early Termination

**Termination for Cause:**
- Material breach uncured
- Force majeure exceeding threshold
- Insolvency events
- Sanctions/illegality

**Termination for Convenience:**
- Rare in traditional LTCs
- May exist with penalties
- More common in shorter-term deals

---

## Quality Specifications

### LNG Quality Parameters

| Parameter | Typical Spec | Purpose |
|-----------|--------------|---------|
| Gross Heating Value | 1,050-1,150 Btu/scf | Energy content |
| Wobbe Index | 1,250-1,400 Btu/scf | Interchangeability |
| Methane | ≥85 mol% | Primary component |
| Ethane | ≤8 mol% | Secondary component |
| Propane | ≤3 mol% | Heavier component |
| Butanes | ≤2 mol% | Heavy ends |
| Pentanes+ | ≤0.1 mol% | Heavy ends limit |
| Nitrogen | ≤1.5 mol% | Diluent |
| CO₂ | ≤50 ppmv | Corrosion/freeze |
| H₂S | ≤4 ppmv | Toxicity/corrosion |
| Total Sulfur | ≤30 ppmv | Environmental |
| Mercury | ≤10 ng/Nm³ | Equipment damage |

### Rich vs. Lean LNG

**Rich LNG:**
- Higher heating value (>1,100 Btu/scf)
- More ethane, propane, butane
- Sources: Middle East, some US Gulf

**Lean LNG:**
- Lower heating value (<1,070 Btu/scf)
- Higher methane percentage
- Sources: Australia (some), Atlantic

**Quality Issues:**
- Buyer specifications may limit rich/lean
- Blending may be required
- Off-spec rejection or price adjustment

### Off-Spec Consequences

**Options:**
1. Rejection (seller must remedy)
2. Acceptance with price adjustment
3. Blending with other cargoes
4. Alternate disposition

**Price Adjustment Formula (Example):**
```
If GHV < 1,050 Btu/scf:
Adjustment = (1,050 - Actual GHV) × $0.01/MMBtu per Btu shortfall
```

---

## Force Majeure

### Definition

**Typical FM Events:**
- Natural disasters (earthquakes, typhoons, floods)
- Acts of war, terrorism, civil unrest
- Government actions (embargoes, sanctions)
- Labor disputes (beyond party control)
- Equipment failure (unforeseeable)
- Epidemic/pandemic (increasingly relevant)

**Exclusions:**
- Economic hardship
- Market price changes
- Failure to obtain financing
- Negligence of claiming party

### FM Consequences

**Relief:**
- Suspension of affected obligations
- No liability for non-performance
- Time extensions

**Limitations:**
- Duty to mitigate
- Notice requirements
- Maximum duration (then termination rights)

### FM Duration Thresholds

**Example Clause:**
```
If FM continues for more than 180 consecutive days:
- Either party may terminate affected portion
- If FM exceeds 365 days: Full termination rights
- Termination without liability
```

---

## Destination Clauses

### Traditional Destination Restrictions

**Fixed Destination:**
```
"All LNG shall be delivered to and regasified at
[Named Terminal], [Country] and shall not be
resold or diverted without Seller's prior consent."
```

**Purpose (Historical):**
- Prevent arbitrage against seller
- Protect regional pricing
- Ensure security of supply for buyer

### Modern Destination Flexibility

**Full Destination Flexibility:**
```
"Buyer may direct delivery to any terminal worldwide
capable of receiving the cargo, subject only to
operational and safety requirements."
```

**Partial Flexibility (Profit Sharing):**
```
"Buyer may divert cargoes to alternative destinations.
Net profit from diversion shall be shared:
- 50% to Buyer
- 50% to Seller"
```

**Profit Calculation:**
```
Diversion Profit = (Alt Destination Price - Contract Price)
                   × Volume - Additional Costs

Shared 50/50 between parties
```

### Regulatory Considerations

**EU/Competition Authority Views:**
- Destination clauses may violate competition law
- EU has challenged restrictions in gas contracts
- Trend toward greater flexibility

**US DOE Export Authorizations:**
- FTA vs. Non-FTA country authorizations
- Public interest determinations
- Influence on destination options

---

## Shipping Terms (Detailed)

### FOB Contracts

**Seller Provides:**
- LNG at loading port
- Loading operations
- Custody transfer at manifold

**Buyer Provides:**
- Vessel
- Shipping arrangements
- Insurance (hull, cargo)
- Canal/port fees

**Vessel Approval:**
- Seller approves buyer's vessels
- Compatibility assessment
- Operating standards

### DES Contracts

**Seller Provides:**
- End-to-end logistics
- Vessel and shipping
- All transit costs
- Delivery to receiving terminal

**Buyer Provides:**
- Terminal acceptance
- Unloading operations
- Send-out arrangements

### Shipping Documentation

**Key Documents:**
| Document | Purpose |
|----------|---------|
| Bill of Lading | Title document, receipt |
| Certificate of Origin | Source verification |
| Certificate of Quality | Specifications confirmation |
| Certificate of Quantity | Volume verification |
| Ship's Ullage Report | Tank measurements |
| Notice of Readiness | Arrival notification |

---

## Default and Termination

### Events of Default

**Buyer Default:**
- Failure to take cargo without excuse
- Failure to pay within grace period
- Insolvency
- Material breach of other obligations

**Seller Default:**
- Failure to deliver without excuse
- Delivery of off-spec cargo (repeated)
- Insolvency
- Material breach of other obligations

### Cure Periods

**Typical Cure Rights:**
```
Payment default: 10-30 days to cure
Operational breach: 60-90 days to cure
Notice of default required
Opportunity to dispute
```

### Termination Remedies

**Non-Defaulting Party Rights:**
- Terminate contract
- Claim damages (cover costs)
- Enforce guarantees/security
- Retain TOP payments

**Damages Calculation:**
```
Seller's damages (buyer default):
= (Contract Price - Market Price) × Remaining Volume
+ Costs of finding alternative buyer

Buyer's damages (seller default):
= (Cover Price - Contract Price) × Remaining Volume
+ Incremental procurement costs
```

---

## Dispute Resolution

### Negotiation

**First Stage:**
- Good faith discussions
- Escalation to senior management
- Time-limited (30-60 days typically)

### Expert Determination

**Use Cases:**
- Technical disputes (quality, quantity)
- Price review calculations
- Accounting matters

**Process:**
- Agreed expert or appointed
- Binding determination
- Limited appeal rights

### Arbitration

**Preferred Forum for LNG:**
- International arbitration standard
- Neutral venue
- Enforceable awards (NY Convention)

**Common Rules:**
| Institution | Characteristics |
|-------------|-----------------|
| ICC | Paris-based, comprehensive |
| LCIA | London, expedited options |
| SIAC | Singapore, Asia-focused |
| HKIAC | Hong Kong, regional |
| UNCITRAL | Ad hoc rules |

**Typical Clause:**
```
"Any dispute arising out of or in connection with
this Agreement shall be finally resolved by
arbitration under the ICC Rules by three arbitrators
appointed in accordance with said Rules. The seat
of arbitration shall be London, England. The
language of arbitration shall be English."
```

### Governing Law

**Common Choices:**
- English law (most common for LNG)
- New York law
- Singapore law

**Considerations:**
- Legal certainty
- Precedent availability
- Neutrality
- Enforceability

---

## Key Negotiation Points

### Buyer Priorities

1. Volume flexibility (lower TOP)
2. Destination flexibility
3. Competitive pricing
4. Price review rights
5. Force majeure protections
6. Make-up rights
7. Quality flexibility

### Seller Priorities

1. Revenue certainty (higher TOP)
2. Price formula protection
3. Scheduling predictability
4. Credit security
5. Liability limitations
6. Destination visibility (profit sharing)
7. Termination protections

### Negotiation Outcomes by Market Conditions

| Market Condition | Likely Outcomes |
|------------------|-----------------|
| Tight supply | Seller-favorable (higher prices, stricter terms) |
| Oversupply | Buyer-favorable (flexibility, lower prices) |
| Project seeking FID | Balanced (need for bankable contracts) |
| Established project | More flexibility possible |

---

**Next**: [[06-LNG-Shipping-and-Logistics]] - Maritime operations and logistics
