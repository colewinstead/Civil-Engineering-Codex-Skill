# Provenance and evidence

Initial review: 2026-10-05. All six source directories were inspected before authoring the skill: documentation, relevant calculation paths, parsers/models, validation/tests, output logic, and available reference/sample evidence. This file is an audit catalog; load it for authority, evidence, or conflicts rather than ordinary domain tasks.

No private dataset, original photograph, manual illustration/table, or proprietary source-code block is redistributed. Source paths below are repository-relative identifiers, not a requirement that future users possess those repositories.

## Classification

| Label | Meaning |
|---|---|
| General | General civil-engineering knowledge; conventions are identified explicitly. |
| Math | Mathematical/geometric principle under stated definitions and assumptions. |
| Safeguard | Engineering software safeguard, including recommendations derived from failures. |
| Validated | Independently checked behavior; read the stated scope and method. Ordinary characterization tests alone are not independent engineering validation. |
| Agency | Identified agency requirement/method or its encoded interpretation; applicability/current edition still requires verification. |
| Project | Project-specific criterion; not automatically an agency requirement. |
| Application | Observable product behavior that may or may not be appropriate elsewhere. |
| Implementation | Mechanism or format detail, not a design criterion. |
| Assumption | Condition adopted by a method or implementation; must be made explicit. |
| Unknown | Insufficiently sourced, unsupported, or unresolved knowledge. |

Combined labels distinguish a source's stated basis from its implementation. Recommendations in this skill are not represented as already present in every source application.

## Source snapshots and locations

| Source | Snapshot | Evidence locations and source IDs |
|---|---|---|
| Drainage | No Git repository; `culvert_sizer.py` SHA-256 `ecc0e1b2f2e45096621ea1fa47b18eb56b9f7911fcc9b50c0c682c7aa546994a` | **DR-HYD:** `culvert_sizer.py`, especially critical-depth, barrel-loss, candidate-evaluation, channel normal-depth, recommendation/report functions; included MDOT Roadway Design Drainage Manual, November 2025, sections 3.6–3.7. |
| Guardrail Program | `fc900bc8a64bff9566b8a4a329b0f98d60760258` | **GR-LON:** `guardrail_V8.5.py` calculation/table paths; included Table 9-6-A excerpt and GR-4/GR-4a drawings. **GR-XML:** `guardrail_landxml.py`. **GR-DRAW:** `guardrail_dxf.py`, report/export paths. **GR-QA:** `guardrail_validation.py`, `test_guardrail_app.py`, `test_guardrail_landxml.py`, `test_guardrail_phase2.py`, `test_guardrail_dxf.py`, and UI snapshot test source. |
| Road-Stationing-App | `1d39d6b8988acd80db8e759be7a8c8b23bcfef16` | **RS-GEO:** `RoadStation/Core/Geometry/`, geometry and tolerance tests. **RS-STA:** `StationingEngine.swift`, `OffsetEngine.swift`, station-equation/inverse tests. **RS-XML:** `RoadStation/Core/LandXML/`. **RS-CRS/FIELD:** `RoadStation/Core/CRS/`, `RoadStationApp/CRSAdapter/Sources/RoadStationAppleCRS/PROJProjectCoordinateTransformer.swift`, `RoadStationFieldPosition/FieldPositionSession.swift` and `LocationTypes.swift` in the same Sources tree. **RS-ORD:** `RoadStation/Core/Validation/`, CLI, private real-ORD validation package and its summary; private identifiers intentionally omitted. |
| field-photo-mapper | `69f52f2f0ae11be0672c16ac7e17d5e358779795` | **FP-META:** `lib/photo.ts`, `standalone/metadata.ts`, `standalone/photo.ts`, record types and map consumers. **FP-EXPORT:** server/standalone exporters, `standalone/photo.test.ts`, `standalone/exporters.test.ts`, fixture provenance, README/public-beta limitations. |
| Landxml Qgis Plugin | `9bd1542dccf2cd75831d2fb1ecdd8f9db858d036` | **QG-XML/GEO:** `landxml/parser.py`, `landxml/geometry.py`, `landxml/sections.py`. **QG-PROFILE:** `landxml/profile.py` and profile output paths. **QG-TIN:** `core.py`. **QG-CRS:** `processing_common.py`. `tests/test_landxml.py`, `tests/test_qgis_processing.py`, `docs/qgis4-audit.md`, `docs/openroads-sample-audit.md`, synthetic fixtures. |
| VeriCivil | `085e04e81f7bab68cdfde27ebc2e9f884844059d` | **VC-SE:** `Super.py`, `criteria_info.py`, `docs/MDOT_TRANSITION_MODEL.md`. **VC-TDOT:** `tdot_criteria.py`, `test_tdot_criteria.py`. **VC-REVERSE:** `super_transition.py`, transition-model documentation. **VC-STA:** station conversion functions in `Super.py`. **VC-XML/CRS:** `super_landxml.py`, `test_landxml_coordinate_system.py`. **VC-QA:** `super_qa.py`, `super_service.py`, `super_exports.py`, export/QA/source tests, browser parity tooling. **VC-BASE:** `calculators/crushed_stone_base/engine.py` and `test_crushed_stone_base.py`. |

## Authority ledger

- **DR-HYD — Agency method plus application assumptions.** Included November 2025 MDOT drainage manual was read for culvert energy losses and the inlet/outlet-control procedure, including method applicability limits. Candidate ordering, fallback materials, trial heuristics, and a report's “OK” are not established agency approval. Hydrology chapters in the manual do not mean the script implements them.
- **GR-LON — Agency excerpt plus application assembly.** Reviewed MDOT Table 9-6-A formulas and GR-4/GR-4a drawings dated August 1, 2017. On 2026-10-06, the maintainer verified that W (shoulder width plus foreslope width) in these drawings is interchangeable with the manual's recommended clear-zone distance `Lc`; this resolves the earlier W/Lc uncertainty. `LA` remains the separate distance to the back of the hazard. The limited source set does not establish all clear-zone table entries, terminal acceptance, or current applicability; application defaults/minimums still need separate verification.
- **VC-SE — Identified, versioned criteria.** Repository profile `mdot-rdsd-2026-04-22` references the 2020 Roadway Design Manual sections 3-4 and 14-2.04 and SE standard sheets. The repository records sheet and compiled-set dates; the complete set of encoded entries was not independently re-audited against every original sheet.
- **VC-TDOT — Identified, versioned criteria and examples.** Profile `tdot-rd11-2026-04-30` references TDOT Roadway Design Guidelines chapter 2, RD11-LR-1/LR-2, and SE sheets. The public [TDOT Superelevation Design Guide](https://www.tn.gov/content/dam/tn/tdot/engineering-production-support/documents/design-standards/additional-resources/Superelevation%20Design%20Guide.pdf) was inspected as an additional primary reference. Profile labels do not imply all cataloged features are implemented.
- **VC-REVERSE — Project criterion.** Its minimum-tangent/rate-preserving coordination is explicitly not sourced as a complete MDOT/TDOT reverse-curve standard.
- **RS-GEO/STA, QG-PROFILE/TIN — Math plus implementation.** Analytical geometry, parabolic-profile relationships, and triangle interpolation can be evaluated independently; their numerical tolerances and file-support boundaries remain application choices.
- **RS-GEO/QG-GEO — Maintainer-confirmed design intent, 2026-10-06.** RoadStation prioritizes precise station/offset calculations; the QGIS plugin's alignment workflow is intended for visualization and spatial context, not exact engineering measurements. This explains their different clothoid handling without establishing a universal accuracy criterion or relaxing terrain/CRS safeguards.
- **RS-CRS/QG-CRS — Software/geodetic safeguards.** [PROJ operation documentation](https://proj.org/en/stable/development/reference/functions.html) supports the cited transformation options. No vertical-datum or field-survey certification follows from using that API.
- **FP-META/EXPORT — Implementation evidence and documented purpose.** The README describes photo mapping for project documentation and field review, rather than RoadStation's project-coordinate station/offset workflow. This scope difference explains the absence of a project-CRS pipeline, but does not justify missing geographic range checks. File-format handling and field-record preservation supply useful safeguards; no surveying standard or measured positional accuracy was established.
- **Unknown authority:** VeriCivil's scaled-friction “AASHTO-style” fallback, unsourced defaults, and values whose original governing tables were not fully checked must not be presented as verified AASHTO/FHWA/MUTCD/DOT requirements.

## Validation observed during this review

| Source | Evidence | What it does not prove |
|---|---|---|
| RoadStation | Fresh `swift test`: 151 core plus 7 harness tests passed. Real-ORD validator: 30/30 cases at 0.001 ftUS comparison tolerance; line 6, arc 8, spiral 10, station equation 6. Maximum absolute station difference 0.00047010525 ftUS; offset 0.00000010458 ftUS; XY distance 0.00047010521 ftUS. | No universal importer certification, vertical design validation, or phone survey accuracy. The private benchmark is not redistributed. |
| Guardrail | 62 selected calculation, LandXML, validation, drawing/export regression tests passed. UI snapshot test source was inspected; UI suite not executed. | Baseline characterization is not complete roadside compliance or independent approval of every constant. |
| VeriCivil | 101 selected TDOT criteria, QA, exports, coordinate-system, base-quantity, and criteria-source tests passed. Browser parity workflow inspected, not rerun. | No complete audit of every agency table, receiver-side ORD import, browser behavior, or project-specific reverse rule. |
| QGIS plugin | All 32 parser/headless Processing tests passed under installed QGIS 4.2.2 Python. Environment warnings noted missing PROJ/GDAL data configuration; these passes do not clear all transformation cases. Prior documented QGIS 3.44/4.2.2 and private-file runtime checks were read. | No new desktop/manual or survey-control test; prior runtime reports remain reports. |
| Field photos | Metadata and CSV/KML/KMZ test source inspected. Local suite could not run because Vitest was unavailable. | No executed regression claim, EXIF truth verification, or measured positional accuracy. |
| Drainage | Full script and relevant manual method inspected; equations traced through selection/reporting. No independent hydraulic regression suite found. | No hydraulic design certification or implemented hydrologic analysis. |

## Cross-repository synthesis and conflicts

| Issue | Observations | Reusable decision |
|---|---|---|
| Units/CRS | All spatial tools face axis/unit ambiguity; photo mapping lacks a project-CRS pipeline. | Preserve explicit metadata and unknowns; use stronger checks as recommendations, not claims of existing implementation. |
| Arc direction | Raw NE versus normalized EN changes handedness; VeriCivil also infers sweep in some paths. | Trace conversion and declared rotation together; flag contradictions and semicircle ties. |
| Spiral handling and purpose | RoadStation evaluates the defined clothoid for precise stationing; the QGIS plugin samples and can adjust endpoints for visual/spatial context. A synthetic fixture's approximately 0.00517379-unit residual exceeds RoadStation's 0.001-unit import consistency threshold. | Keep these purpose-specific policies separate; adjusted visual geometry is not exact stationing geometry. These are local thresholds, not standards. |
| Station ambiguity | RoadStation/Guardrail preserve explicit branches; VeriCivil can choose first after range filtering; QGIS lacks station equations. | Return distinct candidates and require a truly disambiguating selection. Synthetic review reproduced two candidates at 75 and 125 with a nonresolving 0–200 range. |
| Geometry gaps | Some importers reject chains; RoadStation exposes gaps without bridging; permissive overlay paths can omit entities. | State partial coverage and restrict affected operations; never silently fabricate continuity. |
| Agency transitions | MDOT runoff-based placement and TDOT total-transition placement differ; interpolation/rounding policies also differ. | Retain criteria identity and exact policy; no universal merged table or placement rule. |
| “Pass” versus completeness | Drainage can pass missing inlet-control assessment; Guardrail calculation and drawing have different feasibility gates. | Report precisely what passed and what remains unevaluated or infeasible. |
| Vertical meaning | QGIS preserves source Z during XY reprojection; RoadStation is horizontal-only; photo KML uses placeholder altitude. | Never infer a common vertical datum, unit, or measured elevation. |
| Shared result state | Guardrail export capture, VeriCivil lane profiles, and RoadStation fix/result snapshots prevent divergent output. | Preserve one internally consistent engineering state and provenance across consumers. |
| Documentation drift | Older RoadStation fixture audit lacked newer real-ORD spiral/equation evidence. | Inspect current implementation and actual evidence; qualify stale reports. |

Especially strong evidence: independent ORD comparisons plus mathematical geometry tests. Repeated safeguards: dimensional checks, unambiguous interpretation, stable output state, explicit unsupported modes, and quantified residuals. Gaps: drainage completeness, comprehensive roadside criteria, station-equation parity, vertical transformations, arbitrary vendor geometry, and controlled field accuracy.

## Deliberate exclusions

Private project/client identifiers, project numbers, source coordinates, private dataset filenames, original photographs/EXIF, personal/device paths, credentials, manual text/tables/illustrations, and source-code copies are excluded. Project datasets are referenced only conceptually.

Generic UI/Git/framework/packaging advice, hard-coded sample EPSG codes, arbitrary numerical tolerances as universal requirements, unverified vendor compatibility, and default coefficients/densities as design standards are also excluded. Implementation details appear only when they explain a non-obvious engineering safeguard or failure mode.

## Skill packaging checks

The Skill Creator validator passed; all relative document links resolved. The requested global symlink resolved to the canonical repository and exposed the same entrypoint file. A fresh installed-Codex prompt probe from an unrelated directory included the skill in its available-skills catalog. This verifies discovery in that build, not automatic selection for every future prompt.

Direct scenario review checked incomplete culvert verification, ambiguous station lookup, horizontal-versus-vertical terrain conversion, agency transition placement, and exclusion of a UI-only color change. An attempted independent evaluating agent stopped at an account usage limit; no independent forward-test result is claimed.
