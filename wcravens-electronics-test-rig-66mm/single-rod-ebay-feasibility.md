# Single-Threaded-Rod Dual-Deploy Ebay — 66 mm / 2.6" Airframe

Feasibility study for a mid-power dual-deployment avionics bay using **one** central threaded
rod instead of the conventional two-rod design.

**Target vehicle:** 66 mm (2.6") airframe, ≤ 700 g liftoff mass
**Bay:** LOC Precision 2.56" tube coupler, 6" long — ID 2.479" (62.97 mm), OD 2.56" (65.0 mm)
**Electronics:** dual-redundant, Eggtimer Quark or Apogee class (each ≈ 45 × 20–23 mm, 5 g)

---

## Verdict

**Feasible, and for this size vehicle it is arguably the better design — but only with three
non-negotiable details.** The single rod is not the weak link. The things that will bite you are
the bulkhead, the charge size, and rotation.

1. **Use M5, not M4.** Buckling — not tension — sizes the rod, and a 6" coupler is a long column.
2. **Give the bulkheads a bearing shoulder inside the coupler.** Without one, a 1/8" ply bulkhead
   on a single central rod fails at ordinary ejection pressures. With one, it passes easily.
3. **Positively key the sled against rotation.** One rod cannot do this by itself.

Get those three right and the single-rod bay is lighter, simpler to drill, and leaves *more*
usable bulkhead area for terminal blocks and charge wells than a two-rod bay does.

---

## 1. Geometry and load cases

| Item | Value |
|---|---|
| Coupler ID | 62.97 mm |
| Bulkhead area | 3 114 mm² = **4.83 in²** |
| Coupler length | 152.4 mm |
| Rod free length between bulkhead inner faces | ≈ 146 mm — **use 150 mm** |
| Rod cut length (incl. nuts/washers outboard) | ≈ 175 mm |

### 1.1 Ejection pressure — this is the driving load

Assuming a 250 mm parachute compartment (**47.5 in³**), Rouse formula
`P = m·266·3307 / V`:

| BP charge | Chamber pressure | Force on one bulkhead |
|---|---|---|
| 0.25 g | 10.2 psi | 219 N (49 lbf) |
| 0.40 g | 16.3 psi | 351 N (79 lbf) |
| **0.50 g** | **20.4 psi** | **438 N (99 lbf)** |
| 0.75 g | 30.6 psi | 657 N (148 lbf) |
| 1.00 g | 40.8 psi | 876 N (197 lbf) |
| 1.50 g | 61.2 psi | 1 315 N (296 lbf) |

Cross-checked against shear-pin sizing: 2 × #2-56 nylon pins (30 lbf each) shear at 12.4 psi;
with 50 % margin you want ~19 psi, i.e. **0.45–0.5 g**. So **20 psi / 440 N is the design load
and 30 psi / 660 N is the sensible worst case.**

> ⚠ The dangerous number is 1.0 g. That is a charge size people reach for casually on a 2.6"
> bay, and it doubles the design load. Size charges by calculation and ground-test them.

### 1.2 Everything else is small

| Load case | Magnitude |
|---|---|
| Deployment shock, 0.7 kg @ 20 g | 137 N |
| Deployment shock, 0.7 kg @ 50 g (hard main) | 343 N |
| Boost inertia on a 40 g sled @ 20 g | 8 N |

Ejection pressure dominates by 2–5×. Design to it and the rest is free.

---

## 2. Rod sizing — buckling governs, not tension

### 2.1 Tension is a non-issue

| Rod | Stress area | Steel 4.8 UTS | A2-70 stainless UTS |
|---|---|---|---|
| M4 | 8.78 mm² | 3 688 N | 6 146 N |
| M5 | 14.2 mm² | 5 964 N | 9 940 N |

Against a 440 N design load, even M4 has a **safety factor of 8**. Tension never sizes this rod.

### 2.2 Compression does

When the fore charge fires, pressure pushes the fore bulkhead aft and the rod carries it in
**compression** to the aft bulkhead nut. A 150 mm M4 rod is a very slender column (L/r = 185).

Euler critical load, 150 mm free length, steel:

| End condition | M4 | M5 | M6 |
|---|---|---|---|
| Pinned–pinned *(conservative)* | **476 N** | **1 124 N** | 2 235 N |
| One end fixed | 971 N | 2 293 N | 4 561 N |
| Fixed–fixed (nuts properly clamped) | 1 903 N | 4 494 N | 8 940 N |
| Braced at midspan by the sled | 1 903 N | 4 494 N | 8 940 N |

**M4 at 150 mm pinned–pinned buckles at 476 N — below a 30 psi charge and barely above a
0.5 g charge.** That is not enough margin for a flight article.

**M5 gives 1 124 N pinned–pinned = SF 2.6 at design load, SF 1.7 at worst case.** Acceptable.
With clamped ends or a midspan brace it goes to SF > 10.

Slenderness check confirms elastic Euler applies (σ_cr = 58 MPa for M4, 89 MPa for M5, both far
below yield), so the Johnson correction is not needed and these numbers are not optimistic.

### 2.3 Material

| Material | Effect on buckling |
|---|---|
| Steel 4.8 / A2-70 stainless (E ≈ 193–200 GPa) | baseline — **use this** |
| 6061-T6 aluminium (E = 69 GPa) | × 0.345 → M5 drops to **388 N. Fails.** Only viable if braced at midspan. |
| Nylon | Not viable in compression at this length. |

**Recommendation: M5 × 175 mm A2-70 stainless threaded rod.** Stainless for corrosion and because
you will be firing black powder next to it.

---

## 3. The bulkhead is the real problem — and the real fix

This is where the single-rod design genuinely differs from two rods, and where 1/8" ply gets you
into trouble.

**If the bulkhead is retained only by the central rod**, ejection pressure loads it as a disc with
uniform pressure supported at a single central point. Bending stress at the washer (25 mm OD
fender washer assumed):

| Bulkhead | 15 psi | 20 psi | 30 psi | 41 psi | Allowable |
|---|---|---|---|---|---|
| 1/8" birch ply | 50.0 | 66.6 | 99.9 | 136.6 MPa | ~45 MPa → **FAIL at every pressure** |
| 2 × 1/8" ply laminated (1/4") | 12.5 | 16.7 | 25.1 | 34.3 MPa | ~45 MPa → OK |
| 1/8" G10 | 50.0 | 66.6 | 99.9 | 136.6 MPa | ~300 MPa → OK |
| 3D-printed PETG, 3.2 mm | 50.0 | 66.6 | 99.9 | 136.6 MPa | ~40 MPa → **FAIL** |

**If the bulkhead instead bears on a shoulder ring epoxied inside the coupler**, the load path goes
straight into the coupler wall and the plate is edge-supported:

| Bulkhead | 15 psi | 20 psi | 30 psi | 41 psi |
|---|---|---|---|---|
| 1/8" birch ply | 12.5 | **16.7** | 25.1 | 34.3 MPa → **OK, SF 2.7 at design load** |
| 1/4" ply | 3.1 | 4.2 | 6.3 | 8.6 MPa |

**A 4× stress reduction for the cost of two plywood rings and some epoxy.** This single change is
what makes 1/8" ply — your stated preference — work, and it simultaneously removes the compression
load from the rod, which kills the buckling concern entirely.

### Recommendation

- **Two 1/8" ply rings epoxied inside the coupler**, ID ~50 mm, positioned so the bulkheads seat
  flush-to-5 mm-recessed at each end. Bulkheads drop against the shoulders; the rod's only job
  becomes retaining them against recovery shock (≤ 343 N — trivial for M5).
- Bulkheads: **1/8" birch ply, or 1/8" G10 if you want the margin.** Laminating two 1/8" plies
  with the grain crossed is the cheap way to buy a 4× margin if you skip the shoulders.
- **Do not 3D-print the bulkheads.** PETG fails at every pressure in the center-supported case,
  layer adhesion in Z is far worse than the bulk number, and it sits directly in the hot BP gas
  path. **The sled is fine to print** — it carries almost no load.

### Washer size matters more than you'd think

| Washer | Bearing area | Ply crush limit @ 10 MPa | σ at 440 N |
|---|---|---|---|
| M5 DIN 125 plain (10 mm OD) | 91 mm² | 910 N | 4.8 MPa |
| M5 DIN 9021 (15 mm OD) | 157 mm² | 1 570 N | 2.8 MPa |
| **M5 × 25 mm fender/repair** | **467 mm²** | **4 671 N** | **0.9 MPa** |

Use the 25 mm fender washer. Note DIN 9021 in M5 is only 15 mm OD — you need a **repair/fender
washer**, specified as M5 × 25 mm × 1.5 mm, not a standard form-G penny washer.

### Preload

M5 at 1.5 N·m gives ~1 500 N preload (K = 0.2). Preload above the applied load means the joint
never separates and the ends behave as fixed, which is exactly what you want for buckling.
**1.5–2.0 N·m on M5 with a 25 mm fender washer** is comfortably below the ply crush limit.

---

## 4. Failure modes specific to one rod

| Mode | Why it matters | Mitigation |
|---|---|---|
| **Sled rotation** | Nothing resists torque about the rod axis. The sled spins during handling, boost vibration, and ejection — wires chafe, batteries shift, arming switch misaligns with the switch band hole. | Print the sled with an **arc-shaped back matching the 62.97 mm coupler ID**, or add two small tabs riding the coupler wall. This is easy and free with a printed sled. |
| **Bulkhead rotation** | Bulkhead can spin under the nut, twisting the shock cord and backing off the nut. | Nyloc **plus** a jam nut and threadlocker, and a small anti-rotation dowel from bulkhead into the shoulder ring. |
| **Eccentric rod → bulkhead cocking** | If the rod is offset from centerline, the pressure resultant creates a couple the bulkhead must react against the coupler wall. At **e = 20 mm, 20 psi, 3 mm engagement the wall reaction is ~2 200 N** — enough to blow out a paper coupler. | **Keep the rod on the centerline.** If you must offset it, the bearing shoulder becomes mandatory, not optional. |
| **Eccentric shock cord attachment** | Same problem, driven by the recovery load. | Attach the shock cord **on the rod axis** — an eye nut threaded onto the rod end makes the load path pure tension with zero moment. |
| **Single load path** | One rod, one thread, no redundancy. | Honest assessment: **two rods aren't redundant either** — both are required in a conventional bay too. The real redundancy in DD is two altimeters and two charges, which you already have. Mitigate with stainless, nyloc + jam nut, and threadlocker. |
| **Thread damage** | Stripping the one rod loses both bulkheads and the sled. | Chase the threads after cutting, deburr, don't over-torque. |

---

## 5. Packaging — does a central rod leave room for two altimeters?

The concern with a central rod is that it occupies the axis for the full bay length, so a flat
diametral sled plate would be bisected by it. The fix is to **offset the sled plate slightly off
the diameter** — and the cost of doing so is almost nothing:

| Sled plate offset from centerline | Usable chord width | Depth, near side / far side |
|---|---|---|
| 0 mm | 63.0 mm | 31.5 / 31.5 mm |
| **5 mm** | **62.3 mm** | **26.5 / 36.5 mm** |
| 10 mm | 59.8 mm | 21.5 / 41.5 mm |
| 20 mm | 48.8 mm | 11.5 / 51.5 mm |

**Offsetting the plate 5 mm — just enough to clear an M5 rod — costs 0.7 mm of width.** You keep
essentially the full 62 mm chord, with both faces usable.

Two Quark/Apogee-class boards (45 × 23 mm) mount **one per face**, batteries and terminal blocks
in the remaining depth. Comfortable in a 150 mm bay.

**Where the single rod actually wins:** two rods on a ±20 mm bolt circle eat exactly the bulkhead
real estate where you want charge wells and terminal blocks. With dual-redundant electronics you
need **four charge wells** (two apogee, two main) plus terminal blocks and four e-match feed-
throughs per end. A single central rod leaves the entire annulus free. This is the strongest
argument for the design, and it is a packaging argument, not a weight argument.

---

## 6. Mass

Rod hardware, 150 mm bay, steel:

| Configuration | Mass |
|---|---|
| 1 × M5 + 4 nuts + 2 fender washers | **32.8 g** |
| 2 × M4 + 8 nuts + 4 fender washers | 45.1 g |
| 1 × M4 + 4 nuts + 2 fender washers *(insufficient — buckles)* | 22.5 g |

**Going from two M4 rods to one M5 saves ~12 g** — about 1.7 % of a 700 g rocket. Real, but modest.
**Do not choose this design for the weight.** Choose it for the bulkhead real estate and the
simpler drilling (one hole to align instead of two parallel holes, which is the fiddliest part of
building a two-rod bay).

### Full bay budget

| Item | Mass |
|---|---|
| LOC 2.56" coupler, 6" | ~18 g |
| Switch band | ~6 g |
| 2 × 1/8" ply bulkhead | ~11 g |
| 2 × ply shoulder ring | ~6 g |
| M5 rod hardware | 33 g |
| Printed sled | ~12 g |
| 2 × altimeter | 10 g |
| 2 × 1S LiPo (110–400 mAh) | ~12 g |
| 2 × arming switch | ~4 g |
| 2 × terminal block | ~6 g |
| 2 × attachment hardware | 12–50 g *(see note)* |
| **Total** | **≈ 130–170 g = 19–24 % of a 700 g rocket** |

> **Note on attachment hardware:** a DIN 582 M5 eye nut is the elegant on-axis solution but weighs
> ~25 g each in stainless — 50 g for the pair, 7 % of the vehicle. For a 350 N max shock load that
> is enormous overkill. A small stainless U-bolt straddling the rod (~10 g) puts the load ~8 mm off
> axis, producing only a 2.8 N·m moment at worst case — acceptable once the bearing shoulders are
> in. **Weigh the eye nuts before you commit to them.**

---

## 7. Recommended hardware (metric)

| Qty | Item | Spec |
|---|---|---|
| 1 | Threaded rod | **M5 × 175 mm, A2-70 stainless, DIN 975**, cut from 1 m stock |
| 2 | Nyloc nut | M5, DIN 985, A2 |
| 4 | Hex nut (jam / sled positioning) | M5, DIN 934, A2 |
| 2 | Fender / repair washer | **M5 × 25 mm OD × 1.5 mm** — *not* DIN 9021 (only 15 mm) |
| 2–4 | Plain washer | M5 DIN 125, A2 — sled spacing |
| 2 | Bulkhead | 1/8" birch ply or G10, Ø 62.5 mm |
| 2 | Shoulder ring | 1/8" ply, Ø 62.5 mm OD × ~50 mm ID, epoxied inside coupler |
| — | Threadlocker | Medium strength on all jam nuts |
| 2 | Recovery attachment | M5 DIN 582 eye nut *or* small stainless U-bolt — see mass note |

**Torque: 1.5–2.0 N·m on the M5.**

Optional but recommended: brace the rod at midspan by making the sled a snug clamp on the rod
that also bears the coupler wall. This halves the effective column length and takes M5 buckling
margin from SF 2.6 to SF 10+, and costs nothing.

---

## 8. What would change this verdict

The single-rod design stops being a good idea if:

- **The bay gets longer than ~200 mm.** M5 pinned–pinned drops to 632 N at 200 mm. Go M6 or add a
  midspan brace.
- **The airframe gets bigger than ~3".** Bulkhead area scales with D², so a 4" bay at 20 psi is
  ~1 000 N, and the plate bending in the center-supported case gets ugly fast.
- **You cannot fit the bearing shoulders.** Without them the rod carries the full compression and
  the bulkhead is center-loaded — both marginal.
- **Charges creep up.** At 1.0 g of BP the load doubles and the margins evaporate. Ground-test.

---

## 9. Open items before building

- [ ] Confirm actual parachute compartment volume — the 47.5 in³ assumption drives every pressure
      number here. Re-run the charge table with the real value.
- [ ] Ground-test ejection with the real bay and shear-pin count, and measure, don't guess.
- [ ] Static port sizing for a 150 mm bay — check against Eggtimer's guidance for the specific
      board; typical practice for 2.6" is 3–4 equally spaced ~3 mm holes.
- [ ] Weigh the candidate eye nuts / U-bolts before committing.
- [ ] Verify the LOC coupler ID on the actual part — paper couplers vary, and the sled arc and
      shoulder rings need the measured number.

---

## Calculation notes

- Buckling: Euler `Pcr = π²EI/(KL)²` on the **minor** thread diameter (conservative), cross-checked
  via `σ_cr × A_minor`. Slenderness verified in the elastic range, so no Johnson correction.
- Plate bending: Roark's *Formulas for Stress and Strain*, Table 11.2 — case 10a (simply supported
  edge, uniform load) and the center-supported annular case. ν = 0.3.
- Ejection pressure: Rouse `P = m·R·T/V`, R = 266 in·lbf/lb·°R, T = 3307 °R, cross-checked against
  shear-pin shear loads for consistency.
- Allowables: birch aircraft ply MOR ~45–50 MPa (conservative, weak direction governs for a disc);
  G10 flexural ~300 MPa; PETG ~40 MPa (bulk — layer adhesion in Z is materially worse).
- Assumed A2-70 stainless E = 193 GPa; calculations used 200 GPa steel, a ~3.5 % non-conservatism
  on buckling that is inside the noise of the end-fixity assumption.
