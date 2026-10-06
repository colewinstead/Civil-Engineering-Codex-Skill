# Horizontal roadway geometry

Sources: RS-GEO, RS-ORD, GR-XML, QG-GEO, VC-XML; see [provenance](provenance.md). Coordinate order and units belong in [coordinate systems](coordinate-systems.md).

## Geometry that must survive implementation changes

- **[Math]** A finite tangent projects a query by the dot product onto its unit direction, clamped to the segment interval. Include both endpoints in nearest-point comparisons; a projection beyond an endpoint has a longitudinal residual, not just a perpendicular offset.
- **[Math]** A circular arc needs a center/radius and a directed sweep, or enough consistent constraints to determine them uniquely. Check endpoint radii, arc length `L = R |sweep|`, direction, and minor/major/full-circle cases. Endpoint coordinates alone do not identify the intended arc. A point at the center has nonunique nearest locations on the arc.
- **[Math]** For a clothoid, `k(s) = k0 + (k1-k0)s/L` and `theta(s) = theta0 + k0 s + (k1-k0)s²/(2L)`. Integrate `(cos(theta), sin(theta))` to obtain coordinates. Numerical quadrature of this defined curve is different from replacing it with chords or an arbitrary fitted curve.
- **[Safeguard; RS-GEO]** Bound quadrature error and phase change, detect nonconvergence, and test zero/constant curvature, reversed traversal, and entry/exit spirals. RoadStation compares independent Fresnel-series cases and circle limits. Preserve derivatives and tangent continuity when checking endpoints; do not move endpoints merely to satisfy imported coordinates.
- **[Safeguard]** Search the full eligible alignment, preserve equally valid nearest candidates, and test accelerated searches against exhaustive evaluation. Dense samples are useful checks but are not automatically an independent exact solution.

## Controls and boundaries

- **[General/convention]** PI is the intersection of tangents and generally is not on the circular curve. PC/PT bound a tangent–circular-curve–tangent sequence. TS/SC/CS/ST identify tangent–spiral, spiral–curve, curve–spiral, and spiral–tangent controls. Treat station equations separately from these geometric controls.
- **[Safeguard]** Test just before, exactly at, and just after each join. Check position, tangent, curvature, and station ownership as applicable; a compound circular join can be tangent-continuous without curvature continuity.
- **[Application]** RoadStation retains geometry-gap diagnostics without bridging the gap; Guardrail and QGIS reject disconnected chains in relevant paths. Neither policy authorizes a silent connecting segment. Explain whether partial import is allowed and what operations remain valid.
- **[Application/design intent; maintainer-confirmed]** RoadStation seeks the highest practical numerical accuracy for station/offset calculations: it evaluates the defined clothoid and rejects inconsistent endpoints without warping. The QGIS plugin's alignment workflow serves visualization and spatial context rather than precise engineering measurements; it samples clothoids and can smooth an endpoint residual within a local allowance. This difference reflects their intended uses. The plugin's correction allowance is not an engineering tolerance, and sampled/adjusted output is not exact chainage. Preserve the unmodified mathematical curve for precise station/offset work and report inconsistent source geometry.

## Evidence limits

**[Validated; RS-ORD]** The private ORD benchmark covers lines, arcs, spirals, and station equations within a stated 0.001 ftUS comparison tolerance. This constrains changes to that behavior; it does not certify every LandXML export or GNSS position. Import and computational tolerances remain application parameters in stated units, not universal design criteria.

Read [stationing and offsets](stationing-offsets.md) for inverse-query ambiguity and round-trip limits; read [LandXML](landxml.md) for direction attributes and axis handedness.
