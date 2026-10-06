# Superelevation and cross slopes

Sources: VC-SE, VC-TDOT, VC-REVERSE, VC-QA. Agency behavior below describes identified repository profiles; confirm the actual governing edition before design use.

## Physical states and dimensions

- **[General/convention]** Normal crown drains away from the crown. Adverse crown falls away from the intended bank on the outside lane; full superelevation banks the section through the curve. Identify zero slope and reverse crown from actual lane slopes, not a legacy label. VeriCivil's `reverse_crown_ft` can denote the zero-slope location.
- **[General]** Tangent runout removes the outside lane's normal adverse crown; runoff develops the bank from zero to the design rate. Specify pivot, lane width, lanes rotated, and the inner-lane policy. The term “runout length” also occurs in roadside guardrail work with an unrelated meaning.
- **[Math, unit-qualified]** The conventional US-unit lateral balance is `e + f = V²/(15R)` with mph, feet, and decimal e/f. This relationship does not supply a permissible friction table, emax, minimum radius, or agency design policy.
- **[Agency/application; VC-SE]** Relative-gradient calculations use `Lr = w*n1*b*e/Delta`; applicable lane factors and relative gradient come from the selected criteria. With consistent assumptions, `Lt = Lr*NC/e` for nonzero e. Resolve zero or small e through the criterion's defined case, not a division patch.
- **[Convention]** VeriCivil measures each lane's slope outward from its pivot: both lanes are negative at normal crown, the outside becomes positive at full bank, and the inside remains negative. Left/right turn, outside/inside lane, and LT/RT station offsets are separate conventions.

## Preserve criteria differences

| Classification/source | Reviewed behavior | Boundary |
|---|---|---|
| **Agency/application; VC-SE MDOT** | Places 70% of runoff before PC and 30% after; total transition also includes runout. Inside lane holds normal crown until the model's `X1=Lr*NC/e`, then rotates. | Do not call this a universal 70/30 split of the entire transition. |
| **Agency/application; VC-TDOT** | Places half of total `Lr+Lt` on either side of PC/PT; runoff rounding and rate-row selection follow its TDOT implementation. | Does not inherit MDOT placement or interpolation. |
| **Agency/application; VC-TDOT** | Separate urban 4% and rural 8% emax profiles; exact supported speeds/lane counts and conservative rate selection. | Cataloged divided-roadway sources do not mean divided-lane geometry is implemented. |
| **Project; VC-REVERSE** | Coordinates eligible opposite-direction disjoint pairs with `Tmin=0.7*Lr_exit+0.7*Lr_entry`, preserving full-super stations and rates. | Repository explicitly labels this a project rule, not an agency reverse-curve diagram. |

**[Safeguard]** Record source/edition, table domain, rounding, interpolation or next-row selection, out-of-range behavior, and overrides. MDOT interpolation/clamping, nearest-row choices, and TDOT exact-speed selection are not interchangeable. Returning emax with a warning below a minimum radius is not a compliant design result.

**[Unknown]** The friction-scaled “AASHTO-style” fallback lacks sufficient authority for promotion as an AASHTO requirement. Do not export its name as evidence of compliance.

## Transitions and QA

- **[Safeguard]** Derive station slope, diagrams, reports, and exports from the same lane profiles. Preserve breakpoints for runout, zero slope, crown changes, and full bank. Sampling at PC/PT must not introduce an artificial kink.
- **[Project/application]** Reverse-pair rate intersections need not occur at a tangent midpoint or even within the intervening tangent. Equal/unequal runoff and normal-crown holds require separate checks. A failed pairing must retain independent results and clearly block the claimed coordinated output.
- **[Application]** Same-direction/compound overlap diagnostics are not a complete compound-curve design solver. Imported spirals are not implemented spiral transitions; preserve unsupported-mode gates.
- **[Safeguard]** Verify lane signs, exact control stations, continuity, peak gradient, minimum length, table limits, reverse/compound adjacency, and output agreement against sourced examples. Review drainage near zero cross slope; a mathematically continuous profile does not establish adequate surface drainage.
