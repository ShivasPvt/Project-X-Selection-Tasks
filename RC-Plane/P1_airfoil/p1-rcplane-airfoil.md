# Technical Report: Airfoil Selection for Two RC Aircraft
### IIT Mandi Aeromodelling Team — Techfest 2026, IIT Bombay

**Author:** S SHIVAS · **Date:** 23/10/2026

**Missions.** **Plane A** must carry the maximum payload while flying steadily. **Plane B** must turn, roll and loop, so its wing works at positive and negative angles and sometimes upside down.

**Assumptions.** Span ≈ 1.1 m, chord *c* ≈ 0.26 m, speed *V* ≈ 12 m/s, sea-level air (*ρ* = 1.225 kg/m³, *μ* = 1.81 × 10⁻⁵ Pa·s). Reynolds number *Re* = *ρVc* ÷ *μ* ≈ 211,000, so all airfoils are compared at **Re = 200,000**. Section data from NeuralFoil (trained on XFOIL): 2D, smooth surface.

---

## 1. Shortlist

| Plane | Candidates | Why shortlisted |
|---|---|---|
| A | **Selig S1223**, Eppler E423, Clark Y | Two dedicated high-lift, low-*Re* airfoils (S1223 is the SAE Aero Design heavy-lift standard) and the classic flat-bottomed trainer airfoil as a baseline |
| B | **NACA 0015**, NACA 0012, NACA 0009 | Symmetric airfoils of 15%, 12% and 9% thickness |

*NACA 4-digit code:* in NACA 2412, 2 = max camber (% chord), 4 = its position (tenths of chord), 12 = thickness (% chord). "00" means symmetric.

## 2. Selection

**Plane A — Selig S1223.** It reaches *C*<sub>L,max</sub> = 2.26, 65% more than Clark Y (1.37). Since *L* = ½*ρV*²*SC*<sub>L</sub>, the same 0.29 m² wing at 10 m/s, using 80% of *C*<sub>L,max</sub> for a stall margin, lifts **32.1 N (≈ 3.3 kg)** with S1223 against **19.5 N (≈ 2.0 kg)** with Clark Y. *Runner-up:* Eppler E423 — slightly better *L/D* (78 vs 72) and gentler stall, but ≈ 10% less lift. *Drawbacks handled:* a strong nose-down moment (*C*<sub>m</sub> ≈ −0.28) needs a larger tailplane; the thin, curved trailing edge is built from printed rib templates; higher drag is acceptable at Plane A's low speed.

**Plane B — NACA 0015.** A symmetric airfoil flies the same upright and inverted and has no pitching moment. Of the three, NACA 0015 has the highest *C*<sub>L,max</sub> (1.20), the latest stall (14.5°) and the gentlest — important because tight turns and loops work close to the stall — and its 15% thickness leaves room for a spar strong enough for loop loads. *Runner-up:* NACA 0012 — 10% less drag but a sharp stall after 13°. NACA 0009 stalls earliest and is too thin for a strong wing.

<p align="center"><img src="P1_selected_profiles.png" width="60%" alt="Selected profiles"></p>

*Figure 1 — Selected profiles with chord line, camber line, maximum thickness and maximum camber.*

## 3. Comparison at Re = 200,000

| Airfoil | Thick. | Camber | *C*<sub>L</sub> at 0° | *C*<sub>L,max</sub> | Stall | *C*<sub>D,min</sub> | (*L/D*)<sub>max</sub> | *C*<sub>m</sub> |
|---|---|---|---|---|---|---|---|---|
| **S1223** | 12.1% | 8.7% | 1.23 | **2.26** | 12.0°, gentle | 0.0178 | 72 | −0.28 |
| E423 | 12.5% | 10.0% | 1.12 | 2.02 | 11.5°, very gentle | 0.0182 | 78 | −0.24 |
| Clark Y | 11.7% | 3.4% | 0.44 | 1.37 | 11.5°, very gentle | 0.0104 | 74 | −0.10 |
| **NACA 0015** | 15.0% | 0 | 0 | **1.20** | 14.5°, gentle | 0.0109 | 50 | 0 |
| NACA 0012 | 12.0% | 0 | 0 | 1.11 | 12.0°, sharp | 0.0098 | 47 | 0 |
| NACA 0009 | 9.0% | 0 | 0 | 0.88 | 9.0°, sharp | 0.0087 | 43 | 0 |

*Stall graded by the loss of C<sub>L</sub> in the 3° after the peak, as % of C<sub>L,max</sub>: very gentle < 6%, gentle 6–20%, sharp > 20%.* Cambered sections lift more (even at 0°) but add drag and nose-down moment; symmetric ones have zero lift and moment at 0°, so they fly the same inverted.

## 4. How geometry affects performance

- **Camber:** bends the airflow down even at 0° → more lift and lower stall speed, but more drag, more nose-down moment and poor inverted flight.
- **Thickness:** gentler flow separation and a deeper spar → softer stall and a stronger wing, at the cost of drag at speed.
- **Leading-edge radius:** a rounded nose keeps the flow attached at high angles → later, gentler stall.
- **Trailing edge:** a thin, upturned edge adds lift but is fragile and harder to build.

## 5. Can one airfoil do both missions?

Not well. Payload wants high camber; aerobatics wants zero camber and zero pitching moment. A semi-symmetric compromise (e.g. NACA 2412, 2% camber) would lift less than S1223 and fly unevenly inverted — average at both. Both missions are better covered by an **aircraft** feature: flaps, which add camber for take-off and heavy loads and retract for aerobatics.

## 6. Airfoil vs whole aircraft

| Set by the **airfoil** (2D section) | Set by the **whole aircraft** |
|---|---|
| *C*<sub>L,max</sub>, *C*<sub>D</sub>, *L/D* | **Wing loading** *W/S* → stall speed, turn radius |
| Stall behaviour | **Aspect ratio** *b*²/*S* → induced drag, roll rate |
| Pitching moment | **Controls** → aileron, elevator, rudder size and travel |
| Room for a spar | **Structure** → can the wing take loop loads? |
| | **Thrust-to-weight** → climb and vertical manoeuvres; **CG** → stability vs agility |

A real wing also loses lift at its tips. The airfoil is necessary but not sufficient: an aerobatic section on a heavy, under-powered plane with small ailerons still will not loop.

## Bonus — Simulation comparison

<p align="center"><img src="P1_airfoil_comparison.png" width="88%" alt="Airfoil comparison"></p>

*Figure 2 — All six airfoils at Re = 200,000: shapes, C<sub>L</sub> vs angle of attack, L/D vs angle of attack (Plane A top, Plane B bottom).* Coordinates from the UIUC Airfoil Coordinates Database; NeuralFoil, α = −12° to +18° in 0.25° steps. *Limitations:* 2D only (no tip losses), perfectly smooth surface, least reliable near the stall; to be cross-checked in XFLR5 (Re = 200,000, Ncrit = 9).

## References

1. Selig, M. S. and Guglielmo, J. J., "High-Lift Low Reynolds Number Airfoil Design", *Journal of Aircraft*, 34(1), 1997.
2. UIUC Airfoil Coordinates Database — https://m-selig.ae.illinois.edu/ads/coord_database.html
3. Sharpe, P., NeuralFoil — https://github.com/peterdsharpe/NeuralFoil
4. Club learning playlist — https://youtube.com/playlist?list=PLpdZAunkELHiN85JpFReHTf-5X-gh6MhV
5. AI use: AI tools supported the research, airfoil analysis and report structure; all content was reviewed by the author.
