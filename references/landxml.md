# LandXML interpretation

Sources: RS-XML, GR-XML, QG-XML, VC-XML.

## Import without silently changing the engineering

- **[Safeguard]** Inventory namespaces, units, CRS declarations, alignments, station equations, profiles, surfaces, and unsupported entities before claiming coverage. Detect namespace versions from the document where supported; do not equate a vendor label with a particular entity layout.
- **[Convention/application]** Reviewed alignment inputs store points as northing/easting; RoadStation, Guardrail, and VeriCivil normalize to internal easting/northing. QGIS initially retains stored order and offers an explicit swap. Record the chosen mapping exactly once, and confirm it for the actual export.
- **[Math]** Swapping axes reverses handedness. Clockwise sweep signs in raw NE coordinates differ from the usual EN plane. Establish whether rotation and headings are interpreted before or after conversion; never generalize this into “OpenRoads uses the opposite rotation.”
- **[Safeguard]** Validate line lengths, arc radii/length/sweep, endpoints, spiral type/curvature, and consecutive joins. Redundant attributes are consistency checks, not a license to silently pick whichever produces a curve. Direction attributes need an explicit angle unit and bearing convention; unsupported encodings need diagnostics.
- **[Application/conflict]** RoadStation uses explicit direction-convention options; Guardrail rejects unsupported spirals; QGIS samples supported spirals and may correct endpoint residuals. VeriCivil stores spiral metadata but does not implement spiral superelevation transitions. Its overlay parser also has permissive missing-point/skipped-entity paths. Do not claim that “LandXML supported” means every downstream calculation supports every entity.
- **[Application/conflict]** VeriCivil infers some arc sweep choices from endpoint/length consistency rather than enforcing declared rotation. Semicircle ties and contradictory metadata require particular care. Exact import should resolve contradictions explicitly, not inherit this shortcut.
- **[Safeguard]** Station equations map labels, not geometry; preserve back/ahead/internal semantics and ambiguity. Use [stationing and offsets](stationing-offsets.md), especially when an internal origin differs from displayed starting station.

## Terrain, profiles, and partial coverage

**[Safeguard; QG-XML]** Point IDs must be unique and finite; triangle faces must reference existing points. Duplicate surface/alignment names require an unambiguous selection. Keep original topology and feature identifiers rather than reconstructing semantics from display names.

**[Application]** QGIS supports absolute cross-section points; station-relative templates that lack a supported placement model are skipped with diagnostics. Profile coverage may be partial. A 3D centerline must not acquire invented zero elevations outside that coverage.

**[Safeguard]** If partial import is allowed, identify omitted entities and restrict affected operations. Rejecting one entire invalid alignment while retaining another valid alignment is different from dropping a segment inside a supposedly complete alignment.

Read [terrain surfaces](terrain-surfaces.md) or [vertical geometry](vertical-geometry.md) only for those entities. Synthetic vendor-labeled fixtures demonstrate the tested structure; they do not prove compatibility with arbitrary native exports or direct DGN/DWG access.
