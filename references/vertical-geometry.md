# Vertical profiles

Sources: QG-PROFILE, RS-GEO.

- **[General/convention]** PVI/VPI is a tangent intersection; VPC/BVC and VPT/EVC are the beginning and end of a vertical curve. A tangent-intersection elevation is not generally the curve elevation at that station.
- **[Math]** For a symmetric parabolic vertical curve of horizontal length `L`, beginning at `(s0,z0)`, with decimal grades `g1,g2`, use `x=s-s0`, `z=z0+g1*x+(g2-g1)*x²/(2L)`, and `g(x)=g1+(g2-g1)*x/L`. The curve boundaries are at PVI station ±`L/2`. These relations require consistent horizontal/vertical length units.
- **[Math/convention]** With the grade difference measured in percentage points, `K=L/|G2-G1|`. If grades are decimals, the denominator is `100*|g2-g1|`. A zero grade difference has no finite K; do not divide by zero or confuse K with a required sight-distance criterion.
- **[Safeguard]** Before deriving tangent grades from adjacent PVIs, validate station order, curve length, available neighboring tangents, and overlapping curve extents. Confirm that imported curve lengths are horizontal lengths and that symmetric parabolas are actually intended.
- **[Application; QG-PROFILE]** The reviewed parser supports PVI/ParaCurve profiles and rejects unsupported circular vertical curves. It does not justify converting a circular profile into a parabola. RoadStation's horizontal geometry and interpolated endpoint Z do not implement a designed vertical profile.
- **[Safeguard]** Evaluate elevation only within actual profile coverage. A partially covered centerline remains partial; never fill unknown elevations with zero or extend tangents without an explicit design instruction.
- **[Application; QG-PROFILE]** A station/elevation graph has plotting axes, not map coordinates. Vertical exaggeration affects graphic coordinates while source station/elevation attributes remain unchanged. An offset profile drawn beside an alignment is schematic, not the physical road location.
- **[Safeguard]** Validate end elevations, end grades, PVI relationships, interior extrema when `g(x)=0` lies inside the curve, coverage gaps, and unit conversions. Separate geometric correctness from compliance with agency minimum K, sight distance, drainage, or comfort criteria; those requirements need their own source.
