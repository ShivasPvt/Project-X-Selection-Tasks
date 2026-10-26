# Problem 4 — Bill of Materials for an RC Aircraft
### IIT Mandi Aeromodelling Team — Techfest 2026, IIT Bombay

**Author:** S Shivas · **Date:** 23/10/2026

**Full BOM, prices, links and calculations:** [P4_RC_plane_BOM.xlsx](P4_RC_plane_BOM.xlsx) — tabs *Component Options*, *Configurations*, *Engineering Checks*.

---

## Aircraft brief

Electric, single-motor, high-wing trainer with a 1.1 m wingspan, flown by a 2.4 GHz radio, built from foam board so it is light and quick to repair, and able to take off from the ground or by hand launch. All-up mass ≈ 1,144 g (weight build-up from P3).

---

## Part A — Components

The spreadsheet lists every part, grouped as:

- **Airframe:** foam board, carbon-fibre wing spar, landing gear wire, wheels
- **Propulsion:** motor, ESC, propeller, battery
- **Control:** transmitter, receiver, 4 servos, pushrods, control horns, servo extension leads
- **Electrical:** XT60 connectors, wiring
- **Assembly:** hot glue, tape
- **Support:** charger, LiPo safety bag

---

## Part B — Options compared

Every major component has two real options with specifications, quantity, price (₹, incl. GST) and a supplier link, checked on 23 Oct 2026. Several items were out of stock on that date, so each major part has a second supplier or product as a fallback.

---

## Part C — Justification

### 1. Motor–propeller match

| Quantity | Formula | Result |
|---|---|---|
| No-load motor speed | RPM = KV × V | 1000 × 11.1 = **11,100 RPM** |
| No-load pitch speed | *V*<sub>pitch</sub> = RPM × pitch(in) × 0.0254 ÷ 60 | **21.1 m/s** |
| Stall speed | *V*<sub>stall</sub> = √(2*W* ÷ *ρ S C*<sub>L,max</sub>) | **7.3 m/s** |
| Ratio | *V*<sub>pitch</sub> ÷ *V*<sub>stall</sub> | **2.9×** (≥ 2 ✓) |
| Thrust-to-weight | *T/W* = 885 g ÷ 1,144 g | **0.77** (≥ 0.5 ✓) |

The 1000 KV motor with a 10-inch, 4.5-inch-pitch propeller spins a large propeller slowly, which gives strong thrust at low speed — what a trainer needs for take-off and climb. A higher-KV motor (1400 KV) would need a smaller propeller and draw more current for less low-speed thrust.

**How to check thrust:** the reference figure (885 g at 15.6 A, 173 W) is from the seller's thrust table for a 1047 propeller at 11.1 V; a 1045 gives slightly less. We verify it by strapping the aircraft to a kitchen scale and reading the change at full throttle: *T* = Δ*m* · *g*.

### 2. ESC rating and margin

| Quantity | Formula | Result |
|---|---|---|
| ESC margin | *I*<sub>ESC</sub> ÷ *I*<sub>max</sub> = 30 A ÷ 15.6 A | **1.9×** (≥ 1.2 ✓) |
| BEC load | *n* · *I*<sub>servo</sub> + *I*<sub>rx</sub> = 4 × 0.25 + 0.1 | **1.1 A** (≤ 3 A ✓) |

A 30 A ESC carries the motor's full-throttle current with almost double margin, so it stays cool even on hot days in Mumbai. Its 5 V / 3 A BEC powers the receiver and all four servos without a separate regulator. The 40 A option adds margin but costs twice as much and was out of stock.

### 3. Battery

| Quantity | Formula | Result |
|---|---|---|
| Maximum safe current | *I*<sub>max</sub> = C × capacity = 40 × 2.2 Ah | **88 A** (≫ 15.6 A ✓) |
| Energy | *E* = *V* × Ah = 11.1 × 2.2 | **24.4 Wh** (≤ 100 Wh airline limit ✓) |
| Flight time at full throttle | *t* = Ah × usable fraction ÷ *I* × 60 | **≥ 6.8 min** |

A 3S pack matches the ESC's 2–3S range and the motor's rated voltage. 2200 mAh is the trade-off point: a 1800 mAh pack saves only 7 g but flies about 18% less, while a 3000 mAh pack adds weight, which raises stall speed (*V*<sub>stall</sub> ∝ √*W*). Cruise uses part throttle, so real flights last longer than the full-throttle minimum above.

### 4. Servos and control surfaces

Four 9 g servos: **2 ailerons** (roll), **1 elevator** (pitch), **1 rudder** (yaw). The motor uses a fifth channel through the ESC, so a 6-channel radio leaves one spare.

### 5. Structural material

| Material | Strength | Mass | Cost | Repairability |
|---|---|---|---|---|
| **Foam board (chosen)** | Moderate; stiffened by carbon spar | Low | Very low | Excellent — hot glue and tape |
| Depron | Moderate | Very low | Hard to source in India | Good |
| Balsa | High | Low | Higher; slow to build | Poor after crashes |
| EPP foam | Very tough | Moderate | Imported, expensive | Excellent |

Foam board wins because the first prototype is expected to crash: parts can be re-cut and glued in minutes at the field. It must be paper-faced foam board, not PVC "sunboard", which is several times heavier.

### 6. Compatibility checks

- **Transmitter–receiver:** the FS-i6 and FS-iA6B both use FlySky's AFHDS 2A protocol and are sold as a bound pair. A receiver from another brand would not work with it.
- **Channels:** 5 needed, 6 available.
- **Voltage:** 3S battery (12.6 V when full) is within the ESC's 2–3S limit; the BEC's 5 V suits the servos (4.8–6 V).
- **Current:** motor 15.6 A < ESC 30 A < battery 88 A.
- **Connectors:** XT60 between battery and ESC; 3.5 mm bullet connectors between ESC and motor; JST-XH balance plug fits both chargers.
- **Mechanical:** the propeller's centre hole fits the motor shaft (3.17 mm) with the supplied adapter; the servo horns line up with the pushrods and control horns.

---

## Part D — Budget

| Configuration | Total |
|---|---|
| Budget (CT6B radio, B3 charger, SG90 servos, one battery) | **₹8,915** |
| Performance (FS-i6 radio, B6AC charger, metal-gear servos, Emax motor, 40 A ESC, two batteries) | **₹18,550** |
| **Chosen: Budget build with the FS-i6 radio** | **₹11,501** |

**Safe cost savings:** borrow the club's radio and charger if available; build from foam board instead of balsa; use plastic-gear servos while learning. **Not safe to cut:** the battery, charger, ESC and LiPo bag — a cheap or damaged LiPo is a fire risk.

**Why this choice:** the budget build already passes every engineering check, and its parts are cheap to replace after crashes. The one upgrade is the radio: the FS-i6 lets us set a failsafe (throttle to zero on signal loss) directly on the transmitter, while the CT6B has no screen and must be set up from a computer. For the price difference of ₹2,586, that is the most important safety improvement.

**Upgrade order if more money is available:** a second battery (more flights per session), then the B6AC charger (≈ 1 h charging instead of ≈ 3 h), then metal-gear servos.

---

## Bonus — Take-off mass and propulsion check

- **Take-off mass:** ≈ 1,144 g (≈ 844 g empty + 300 g payload), from the weight build-up.
- **Thrust:** *T/W* = 0.77, above the 0.5 needed for a trainer to climb comfortably.
- **Power:** 173 W ÷ 1.144 kg = **151 W/kg**, enough for a trainer.
- **Conclusion:** the A2212 1000 KV + 1045 propeller on 3S is sufficient, with spare thrust for a heavier-than-planned build.

---

## References

1. Component prices and specifications: Probots (probots.co.in), Robu (robu.in), Zbotic (zbotic.in), checked 23 Oct 2026 — links in the spreadsheet.
2. A2212 1000 KV thrust table: Thingbits — https://thingbits.in/products/a2212-brushless-fpv-drone-motor
3. Club learning playlist — https://youtube.com/playlist?list=PLpdZAunkELHiN85JpFReHTf-5X-gh6MhV
4. AI use: AI tools were used to support research on component prices and specifications, build the BOM spreadsheet and structure this report. All content was reviewed by the author.
