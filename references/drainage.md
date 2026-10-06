# Drainage and culvert hydraulics

Source: DR-HYD. Reviewed coverage is culvert sizing with prescribed discharge and optional channel-derived tailwater. No implemented Rational Method, IDF, time-of-concentration, gutter/inlet-spread, storm-sewer-network, or HGL solver was found. Those tasks require their own applicable method and criteria.

## Reusable calculation methods

- **[General/math]** Manning normal-flow calculations require area `A`, wetted perimeter `P`, hydraulic radius `Rh=A/P`, roughness `n`, and energy slope `S`. The US-customary implementation uses `Q=(1.486/n)*A*Rh^(2/3)*sqrt(S)` for feet/cfs. Do not carry its unit-dependent coefficient into SI. Uniform normal flow is an assumption, not a general backwater solution.
- **[Math]** A trapezoid with bottom width `b`, depth `y`, and side slope `z` horizontal to one vertical has `A=y*(b+z*y)` and `P=b+2*y*sqrt(1+z²)`. Rectangle and triangle are constrained cases. Require a physically meaningful section and positive roughness/slope for this normal-depth method.
- **[Math]** Critical flow satisfies `Q²*T/(g*A³)=1`, where T is top width. A rectangle gives `yc=((Q/b)²/g)^(1/3)`. Circular sections require depth-dependent area and top width. Bracket the physical solution and report residual/convergence; returning zero for invalid input is not a valid hydraulic diagnosis.
- **[Agency/application]** The reviewed culvert model uses full-barrel velocity and losses: `H=(1+Ke+29*n²*L/Rh^1.33)*V²/(2g)` in its US-customary form. It estimates outlet-control headwater using tailwater or a critical-depth-based outlet depth, then subtracts barrel fall. The formula's assumptions and coefficients must remain attached to its manual method.

## Conditions that prevent a complete conclusion

- **[Safeguard]** Check inlet and outlet control for each candidate, entrance configuration, and discharge; controlling headwater is the greater applicable result. Missing inlet control means incomplete assessment. The source application can still mark such a candidate “OK”; do not promote that status to design acceptance.
- **[Assumption/application]** Equal flow among barrels is assumed. A single optional inlet HW/D ratio is reused across candidates, although inlet-control evaluation depends on candidate geometry and flow. Require an applicable calculation or nomograph for each candidate.
- **[Agency, method-specific]** The included MDOT manual's approximate outlet-control procedure flags partial-flow concerns below headwater about 1.2D and directs a backwater calculation when its computed headwater is below 0.75D. These are limits of that described method, not universal thresholds for all hydraulic models. Merely labeling output “partial” does not perform the required analysis.
- **[Project/assumption]** Allowable headwater, recurrence interval, tailwater, roughness, entrance losses, allowable velocities, blockage, and road overtopping need explicit project/source support. Crest elevation minus inlet invert is a headwater allowance only when that is the chosen design constraint.
- **[Application]** First-passing candidate order, trial-area/width heuristics, and fallback from one material/roughness to another are search choices. A material fallback changes the engineering scenario and must be disclosed; first passing is not necessarily optimum.

## Validation

**[Safeguard]** Check finite positive dimensions, barrel count, compatible units, depth domain, bracketing, discharge residuals, loss/head balance, and sensitivity to tailwater and roughness. Compare against manual examples or an independent applicable hydraulic solver before relying on a design. The reviewed script has no independent hydraulic regression dataset.

**[Unknown/not implemented]** Scour, debris, stream stability, fish passage, outlet protection, flood risk, overtopping routing, and environmental constraints are not established by a headwater pass or report placeholders.
