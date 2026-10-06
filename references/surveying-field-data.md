# GNSS and field evidence

Sources: RS-FIELD, RS-CRS, FP-META, FP-EXPORT.

## Position is a measurement with context

- **[Safeguard]** Keep coordinates, timestamp, horizontal accuracy, source, CRS/operation provenance, selected alignment, and computed result in one consistent observation. Do not combine a previous station result with a newer fix's accuracy. Preserve raw observations separately from derived project coordinates.
- **[Application; RS-FIELD]** RoadStation rejects invalid/future/stale fixes, ignores out-of-order updates, and invalidates computations when alignment or coordinate context changes. Last-known results remain distinguishable from live results. Its age/accuracy thresholds are product policy, not a GNSS specification.
- **[Safeguard]** Report fix age and uncertainty in explicit units; geographic source accuracy in meters remains meters even when the project uses feet. Transformation availability and good numerical closure do not remove sensor error, datum mismatch, multipath, or control uncertainty.
- **[General]** A phone GPS station/offset is approximate unless an actual measurement/control process proves otherwise. Decimal places, a precise geometry engine, successful app installation, and an attractive map overlay do not establish survey-grade field accuracy.
- **[Safeguard]** Keep ellipsoidal height, orthometric elevation, vertical datum, geoid, and vertical uncertainty distinct. Neither reviewed phone workflow nor photo KML export establishes a vertical transformation.

## Photograph/location associations

- **[Safeguard; FP-META]** Preserve the original file association, extraction status, and available time/location metadata. A failed image preview need not invalidate successfully extracted coordinates. A missing geotag must not become `(0,0)`; conversely, legitimate zero latitude or longitude must not be treated as absent.
- **[Safeguard]** Validate finite latitude/longitude and their geographic ranges. Do not coerce empty strings into zero. The reviewed photo normalizers do not provide comprehensive range checks or measured accuracy metadata; treat these as gaps, not established safeguards.
- **[Assumption]** EXIF timestamps may lack time zones. Keep that uncertainty and distinguish original capture time from create/modify fallbacks. Do not silently convert an unzoned local timestamp into an asserted UTC capture time.
- **[Implementation; FP-EXPORT]** Leaflet receives latitude/longitude; KML coordinates are longitude/latitude/altitude. The application's KML zero altitude is a placeholder, not a measured elevation. It is not evidence of a project vertical datum.
- **[Safeguard; FP-EXPORT]** Preserve missing-GPS and error rows in audit-friendly tabular exports; omit unlocated map placemarks. Escape CSV/XML data and retain stable record/image associations. Exported resized JPEGs are derivatives, not originals retaining all source evidence.
- **[Safeguard]** Location-bearing photographs and metadata can expose sites and people. Public regression fixtures should use synthetic/sanitized data. Do not claim “fully offline” solely because photo processing is local when background map tiles still require network access.

Read [coordinate systems](coordinate-systems.md) only when converting observations to a project CRS; the photo application itself does not implement that workflow.
