# Guardrail and roadside calculations

Sources: GR-LON, GR-DRAW, GR-QA. These are calculation and output lessons, not a complete roadside-design standard.

## Sourced formula versus complete installation design

**[Agency/application; GR-LON]** The reviewed MDOT Table 9-6-A excerpt supports length-of-need forms using runout length `LR`, hazard extent `LA`, barrier offset `L2`, tangent length `L1`, and flare ratio `q=b/a`:

- Nonflared: `X = LR*(LA-L2)/LA`.
- Flared: `X = (LA + q*L1 - L2)/(q + LA/LR)`.

Confirm variable definitions, traffic exposure, valid geometry, units, selected table, and source applicability before use. A nonpositive computed value does not approve an installation; the site's protection need and terminal/deflection constraints remain separate.

**[Application]** The program subtracts selected terminal/tangent components, applies a minimum body length and rounds to 12.5-ft increments. Those values and assembly conventions are characterized behavior, not independently established universal minimums. Simplified speed/ADT/foreslope clear-zone choices do not cover every roadside condition.

**[Safeguard]** Identify traffic direction, roadway side, alignment direction, bridge end, opposing exposure, median and lane widths separately. Divided-roadway offsets must correspond to actual geometry. Do not use a custom opposing distance in calculations while quietly drawing a different distance.

## Feasibility and output consistency

- **[Safeguard; GR-QA]** Reject nonfinite values, invalid counts, negative widths, and impossible component lengths. Check that installed totals equal their constituent body, tangent, and terminal lengths. Treat short installations and bridge proximity as geometry constraints, not formatting issues.
- **[Application; GR-DRAW]** The DXF path imposes additional terminal, taper, and approach-space checks. A valid numerical result can lack enough physical space for its selected drawing. Expose this distinction; do not reduce a taper or terminal merely to fit.
- **[Unknown/source mismatch]** Reviewed GR-4/GR-4a drawings define W as shoulder plus foreslope width. The application's use of a hazard-related distance for a W-labeled graphic is not proof that those quantities are interchangeable. Verify source definitions before reusing the graphic's dimensions.
- **[Safeguard]** Capture one stable engineering snapshot before export, including inputs, results, alignment, station region, assumptions, and criteria. UI changes during file selection must not alter only part of the drawing/report. A mutable result requires equivalent protection; calling it a snapshot does not make it immutable.
- **[Safeguard]** Dimension the intended alignment/component distance, not an incidental sampled chord or curved offset-path length. Drawing sampling must preserve engineering breakpoints and have a declared representation error budget.

## Verification and limits

**[Application regression; GR-QA]** Selected tests characterize calculations, LandXML ambiguity, geometry validation, export snapshots, and report-write failure handling. They are explicitly not independent engineering validation or engineering approval.

**[Unknown]** Terminal acceptance, manufacturer installation details, dynamic deflection, working width, crashworthiness, all clear-zone conditions, and agency applicability are not established by these tests. Verify governing references for these decisions rather than extrapolating from the application. Read [GIS/CAD interoperability](gis-cad-interoperability.md) for export checks.
