# GIS/CAD and engineering outputs

Sources: GR-DRAW, VC-QA, QG-CRS, QG-TIN, FP-EXPORT.

## Preserve the engineering meaning across formats

- **[Safeguard]** Declare source/target units, coordinate order, station convention, dimensionality, geometry support, and lost attributes. A successful file write proves serialization, not correct interpretation by the receiving software.
- **[Safeguard]** Use one stable calculation snapshot for drawings, PDF, CSV, and GIS layers. Include criteria identity, engine version where available, assumptions, overrides, and diagnostics. A legacy record with unknown criteria remains unknown; do not stamp it with the current standard.
- **[Application; VC-QA]** ORD superelevation CSV uses decimal cross slope and explicit lane/pivot point-type mappings. Verify the mapping for the actual receiver; string-format/export tests alone do not establish a successful ORD import or correct road model.
- **[Safeguard; GR-DRAW]** DXF geometry must satisfy installation feasibility and preserve component/traffic-direction semantics. Dimension actual intended engineering distances. Adaptive drawing samples can approximate a display within a stated budget without redefining the analytical alignment.
- **[Application; QG-CRS]** A station/elevation profile graph has no map CRS. A profile placed beside a road is schematic; a true 3D centerline needs applicable horizontal geometry and actual vertical coverage. Keep feature identifiers and source attributes even if display labels change.
- **[Implementation; FP-EXPORT]** KML/KMZ uses geographic coordinate order and packaged image references; it does not carry arbitrary project coordinates merely because the map displays them. Check coordinate order and derivative-image associations.

## Conversion checks

**[Safeguard]** Inspect the output with an independent reader when practical. Compare units/CRS, entity counts/types, extents, selected coordinates/elevations, station labels, slopes, dimensions, and metadata against the source snapshot. Quantify residuals in meaningful units and inspect geometry boundaries or unsupported entities explicitly.

**[Safeguard]** For rasters, additionally inspect nodata, pixel size/centers, source-triangle elevation agreement, and storage precision using [terrain surfaces](terrain-surfaces.md). For reprojected output, add known-control checks from [coordinate systems](coordinate-systems.md).

**[Safeguard]** Do not overwrite a valid report with partial output after an export failure. Keep diagnostics associated with the attempted result. Tested atomic-write behavior in Guardrail is useful because engineering deliverables must not appear complete when generation failed.

**[Unknown]** LandXML exchange is not native DGN/DWG compatibility. Synthetic Civil 3D/OpenRoads fixtures, runtime loading, numerical comparison, and end-to-end vendor import are separate evidence levels. State exactly which occurred.
