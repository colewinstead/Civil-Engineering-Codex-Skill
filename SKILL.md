---
name: civil-engineering-codex-skill
description: Review civil-engineering calculations and engineering software for technical correctness. Use for roadway geometry/stationing, superelevation, guardrail calculations, culvert hydraulics, CRS/GNSS, LandXML, terrain/GeoTIFF, and civil CAD/GIS interoperability. Exclude visual UI, Git, prose, and generic code changes with no engineering impact.
---

# Civil engineering

Use the relevant engineering knowledge below while preserving the requested scope. This skill is not a governing standard or a substitute for engineering judgment or the Engineer of Record.

## Core constraints

- Never invent criteria, equations, tolerances, design values, or agency requirements. Distinguish authoritative requirements, recommended practices, mathematical results, conventions, project criteria, assumptions, and implementation decisions. Verify the applicable jurisdiction, edition, and scope before applying criteria.
- Track units explicitly, including US survey feet versus international feet, meters/inches, percent versus decimal slope, and degrees/radians. Never silently assume CRS, EPSG, datum/realization, geoid, projection, axis order, horizontal units, or elevation units.
- Preserve engineering precision internally; round for a stated purpose and avoid false precision in outputs. Select tolerances from an error budget and never weaken them merely to pass a test.
- Prefer analytical geometry where available. Disclose and bound necessary numerical integration or sampling. Unsupported, malformed, contradictory, or ambiguous inputs need useful diagnostics; never silently substitute plausible geometry or criteria.
- Treat independently validated behavior as a regression constraint unless its intended behavior is explicitly changed. Software tests alone do not prove engineering correctness.
- Separate calculation state from presentation. UI-only changes must preserve engineering results; reports, drawings, and exports must describe the same calculation and assumptions.

## Select references

Read only the row matching the task. Add another reference only for an actual dependency; do not load this entire directory.

| Task | Start here | Add only when needed |
|---|---|---|
| Horizontal geometry, tangents/arcs/spirals | [Roadway geometry](references/roadway-geometry.md) | Stationing or LandXML |
| Profiles, grades, vertical curves | [Vertical geometry](references/vertical-geometry.md) | Coordinate systems |
| Station equations, nearest point, LT/RT | [Stationing and offsets](references/stationing-offsets.md) | Roadway geometry |
| Crown, runoff/runout, design tables | [Superelevation](references/superelevation.md) | Roadway geometry |
| Guardrail, terminals, bridge approaches | [Guardrail](references/guardrail.md) | Stationing for alignment placement |
| Culverts, drainage, hydraulics/hydrology | [Drainage](references/drainage.md) | Applicable external method for uncovered topics |
| LandXML import/interpretation | [LandXML](references/landxml.md) | Applicable geometry or terrain reference |
| TIN, raster, GeoTIFF | [Terrain surfaces](references/terrain-surfaces.md) | CRS and GIS/CAD for conversion |
| CRS, EPSG, State Plane, transformations | [Coordinate systems](references/coordinate-systems.md) | Field data for GNSS |
| GPS, geotagged photos, field evidence | [Surveying and field data](references/surveying-field-data.md) | CRS for project coordinates |
| CAD/GIS exports or conversion QA | [GIS/CAD interoperability](references/gis-cad-interoperability.md) | Applicable domain |
| Base-section quantities | [Quantities](references/quantities.md) | Applicable project specification |
| Engineering software change/review | [Engineering QA](references/engineering-software-qa.md) | Only the affected domain |
| Evidence, authority, conflicting implementations | [Provenance](references/provenance.md) | Only the cited source needed |

## Working method

Identify what engineering behavior can change, its units/spatial context, assumptions, criteria, and existing validated baseline. Inspect the current calculation path before editing. Check mathematical edge cases, geometry boundaries, ambiguity, conversions, and malformed inputs. Validate against analytical solutions, round trips within their valid domain, independent implementations, known software/data, or authoritative examples as available.

Report numerical differences with units and classify them as expected changes, precision effects, implementation errors, changed assumptions, or changed engineering behavior. State remaining authoritative verification needs and the limits of the evidence. Reference labels distinguish general/math knowledge, safeguards, validated behavior, agency/project criteria, application/implementation behavior, assumptions, and unknown authority; definitions and source IDs are in provenance.
