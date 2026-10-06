Human-readable trigger regression cases for v1.1. Try each prompt without explicitly invoking the skill; record actual selection separately. Judge engineering impact, not keywords alone. Explicit invocation remains available.

# Should Trigger

1. Review this station equation implementation.
2. Check this LandXML spiral parser for geometry errors.
3. Why is this State Plane transformation producing the wrong coordinates?
4. Review this guardrail length calculation.
5. Check this culvert headwater calculation.
6. Verify this TDOT superelevation transition.
7. Review this horizontal curve nearest-point algorithm.
8. Check whether this GeoTIFF conversion preserves the source terrain.
9. Review this station/offset regression.
10. Verify units and datum handling in this project-coordinate transformation.
11. Check whether a vertical profile parser is applying the curve correctly.
12. Review engineering output consistency between a calculation, report, and DXF.

# Should Not Trigger

Assume these changes cannot affect engineering inputs, calculations, diagnostics, or outputs.

1. Make this SwiftUI button blue.
2. Change this icon.
3. Fix this navigation animation.
4. Delete a Git branch.
5. Rewrite this README paragraph for clarity without changing technical claims.
6. Rename a variable without changing behavior.
7. Fix generic JSON decoding for account preferences.
8. Refactor unrelated networking code.
9. Update package dependencies unrelated to engineering calculations or spatial data.
10. Change application fonts.
11. Add a generic settings screen.
12. Fix ordinary authentication logic unrelated to engineering results.

# Borderline / Depends on Scope

| Request | Trigger when | No invocation needed when |
|---|---|---|
| Refactor the LandXML importer. | Geometry, units, coordinates, supported entities, or diagnostics may change. | The change is purely structural and provably preserves engineering behavior. |
| Change the field map screen. | GPS/CRS/station calculations or accuracy/freshness meaning may change. | Only visual layout changes. |
| Update a dependency. | PROJ/GDAL, geometry, numerical behavior, or engineering file interpretation may change. | It only affects unrelated application plumbing. |
| Revise a report or README. | Engineering values, unit labels, assumptions, criteria, or validation claims may change. | Only wording or typography changes while technical meaning stays intact. |
