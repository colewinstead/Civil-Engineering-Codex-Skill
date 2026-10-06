# Engineering software review

Sources: RS-GEO/STA/ORD/CRS/FIELD, GR-QA, VC-QA, QG-TIN/CRS, FP-EXPORT, DR-HYD. The following are **[Safeguard]** recommendations synthesized from those implementations, including observed gaps.

## Review sequence

1. Identify the engineering outputs that can change and trace their calculation paths. Establish the current baseline before editing; presentation-only changes must preserve calculation behavior.
2. Identify units, coordinate systems and dimensionality, assumptions, supported modes, and applicable authority. Separate governing criteria from source-table policy, application defaults, manual overrides, and unknowns.
3. Locate existing validated results and classify the evidence: characterization tests, mathematical invariants, independent calculations, sourced examples, vendor comparisons, runtime interoperability, or field/control measurements. None substitutes automatically for another.
4. Inspect finite/range checks and malformed or contradictory input behavior. Include boolean-as-number coercion, empty-string-to-zero coercion, omitted entities, duplicate IDs/names, and unknown units when relevant. Do not turn an invalid calculation into a plausible zero.
5. Check mathematical singularities, geometry joins/endpoints, alternate solutions, station equations, unsupported geometry, source-unit conversions, and CRS operations. Use domain references only for the affected calculations.
6. Run relevant engineering regressions, then compare changed results with independent or previously validated references. Check every consumer that can reinterpret the result: station lookup, drawing, report, GIS layer, and export.
7. Quantify differences and classify each as expected, numerical precision, implementation defect, changed assumption, or changed engineering behavior. State unresolved authoritative verification and unsupported cases.

## Numerical evidence

- Record input/version, criteria identity, units, reference source, test domain, comparison tolerance and reason, case count, and maximum/representative residuals. Report failed and missing metrics as such.
- Separate station, offset, XY distance, elevation, slope, quantity, and hydraulic residuals. A single “pass” can conceal different error budgets or missing comparisons.
- Use analytical limits and independent implementations when possible. A round trip can pass with the same bug in both directions; an accelerated search should also match exhaustive candidates. Apply round trips only where the mapping is unique.
- Derive tolerances from source precision, numerical methods, geometry scale, transformations, and required output accuracy. Distinguish computational error from modeling/measurement error. Preserve ftUS/ft/m meaning when comparing thresholds.
- Never weaken a tolerance solely to pass. Investigate the reference, units, assumptions, degeneracies, and implementation first. Record the engineering reason and changed acceptance scope if a tolerance is legitimately revised.

## Consistent, reproducible results

- Capture inputs, criteria, overrides, source geometry, coordinate provenance, and derived results together. All outputs should consume that state; recalculate or invalidate it when its engineering context changes.
- Preserve raw source data separately from normalized, transformed, sampled, rounded, or manually adjusted values. Label calculated versus source quantities and preserve diagnostic history.
- Test unsupported-mode gates and failure states, not just happy-path numbers. “Inlet control not evaluated,” “ambiguous station,” and “profile absent here” must not become complete approval, a first arbitrary answer, or zero elevation.
- For public fixtures, replace identifiers and coordinates with synthetic data while retaining the mathematical failure case. Keep confidential validation data outside the skill repository.

Use [provenance](provenance.md) to assess the evidence behind these lessons or resolve a cross-project conflict; do not assume every source already implements every recommended safeguard.
