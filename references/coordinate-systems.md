# Coordinates, units, and transformations

Sources: RS-CRS, QG-CRS, VC-CRS, FP-META.

## Spatial contract

**[Safeguard]** Record horizontal CRS and datum realization, coordinate order, linear/angular units, vertical units/datum/geoid if relevant, epoch when relevant, and metadata provenance. Distinguish declared, inferred, user-confirmed, and unresolved values. Coordinates, an agency name, or a State Plane zone name alone do not establish the entire contract.

**[Math/unit definitions]** International foot = exactly `0.3048 m`; legacy US survey foot = exactly `1200/3937 m`. Their roughly two-parts-per-million difference matters at large coordinate magnitudes. Preserve the unit of existing data despite retirement of a unit for new work. Do not resolve generic “foot” to ftUS without evidence. Angles and percent/decimal slopes require similarly explicit conversion.

**[General]** Geographic angular coordinates are not projected planar distances. WGS84 and NAD83 realizations are not interchangeable labels. Selecting an EPSG code does not identify missing vertical metadata or establish field accuracy. Assigning a CRS describes existing coordinates; reprojection changes their numeric representation.

## Transformation workflow

1. **[Safeguard]** Confirm source/target CRS, axis order, areas of use, coordinate units, dimensionality, and the desired accuracy before selecting an operation.
2. **[Implementation; RS-CRS]** RoadStation uses explicit longitude/latitude input and PROJ visualization normalization for conventional coordinate order. QGIS/GDAL explicitly requests traditional GIS order. Neither convention can be assumed for arbitrary CRS APIs.
3. **[Safeguard]** Check operation availability, required grids, datum realizations, and epoch support. Reject an unavailable required operation rather than silently substituting a lower-quality one. RoadStation requests no ballpark operation and best-operation availability with network access disabled; this is its explicit operational policy, not proof of geodetic accuracy. See [PROJ operation options](https://proj.org/en/stable/development/reference/functions.html).
4. **[Safeguard]** Check target native units against project units. Convert once at a documented boundary, preserve raw coordinates, and fail a contradictory declaration. Test known control points and forward/inverse closure; closure alone can also pass for a consistently wrong CRS.
5. **[Safeguard]** Treat vertical transformation separately. The reviewed QGIS horizontal reprojection restores the original Z; RoadStation's adapter is horizontal-only. Neither transforms ellipsoidal height into orthometric elevation or resolves an unknown vertical unit/datum.

## Disagreements and failure modes

- **[Application]** RoadStation requires project CRS confirmation before GPS use. QGIS exposes explicit input/output selections; VeriCivil recognizes some authority identifiers, WKT, and agency names. A recognized name remains subject to unit and datum checks.
- **[Safeguard]** Keep source coordinates and metadata available when user choices disagree with declarations. State exactly which override was applied; do not relabel a transform as a harmless display choice.
- **[Unknown]** Undeclared vertical units stay unknown even if XY looks plausible over imagery. An attractive overlay is a gross-error check, not survey control.

For fix uncertainty and timestamp handling, load [surveying and field data](surveying-field-data.md).
