# Stationing and offsets

Sources: RS-STA, RS-ORD, GR-XML, VC-STA, QG-GEO.

## Separate the coordinate systems along a road

- **[General/convention]** Distinguish geometric distance along the alignment, any internal station origin, and displayed civil station. Adding a station equation changes labels, not physical length or coordinates. Confirm the station-format convention; a `+` separator alone does not identify feet or meters.
- **[Math]** Within a station region, displayed station is continuous distance plus that region's shift. Back and ahead labels refer to the same physical equation location. Forward jumps leave label gaps; backward jumps create overlapping labels with multiple physical solutions.
- **[Safeguard]** Inverse station lookup must return candidates or request an explicit region/branch. Deduplicate candidates only if they identify the same physical point. A range resolves ambiguity only when exactly one distinct candidate remains.
- **[Application/conflict]** RoadStation uses explicit branches and defined ahead/back boundary selection; Guardrail supports region suffixes. VeriCivil's range-filtered lookup currently returns its first candidate even if multiple candidates survive. Synthetic demonstration: an equation at internal 100 with back 100/ahead 50 gives displayed 75 at both internal 75 and 125; range 0–200 does not resolve it. Do not promote the first-result behavior.
- **[Application]** QGIS's reviewed station placement uses sampled distances without station-equation semantics. Labels and sampled chainage must not be represented as exact displayed engineering stationing.

## Offset sign and inverse geometry

**[Math/convention; RS-STA]** In an east/north plane, with unit tangent `t=(tx,ty)` in increasing alignment direction and displacement `v=q-p`, `cross(t,v)` is positive to the left. The left normal is `(-ty,tx)`; a signed-left offset `o` gives `q=p+o*(-ty,tx)`.

**[Safeguard]** State the convention at interfaces. Some CAD results use negative LT/positive RT. Convert explicit side and magnitude once rather than guessing from a sign. Traffic direction, alignment direction, roadway side, and outward lane cross-slope signs are different concepts.

**[Math]** A nearest point can be nonunique at self-intersections, symmetrical geometry, corners, or a circle center. Offset normals may cross. Beyond a finite endpoint, station plus perpendicular offset alone cannot reconstruct an arbitrary query because it omits the longitudinal residual.

**[Safeguard]** Round-trip tests are appropriate within a unique normal neighborhood. Elsewhere test candidate sets, residuals, and explicit ambiguity. Define deterministic ownership at shared endpoints without hiding genuinely different solutions.

## Regression checks

**[Safeguard]** Cover nonzero alignment start, multiple equations, label gaps/overlaps, exact equation locations, tiny values on each side, endpoints, joins, signed LT/RT, large projected coordinates, and nonfinite inputs. Preserve geometric position when only labels change. Choose tolerances in project length units and distinguish station error, offset error, coordinate error, and nearest-distance error.

**[Validated; RS-ORD]** ORD comparisons explicitly normalize offset convention and report these metrics separately. The numerical bounds and coverage are in [provenance](provenance.md); load that record when assessing a regression claim.
