# Civil Engineering for Codex

A global Codex skill for civil-engineering reasoning, calculation review, and engineering software validation. It captures reusable lessons from six working civil/geospatial software projects without distributing their private datasets or copying their source code.

The skill emphasizes explicit units and spatial references, source-qualified criteria, analytical geometry, useful diagnostics, and preservation of independently validated behavior. It exists to prevent engineering assumptions from disappearing inside otherwise plausible software changes.

## Coverage

- Horizontal geometry, clothoids, station equations, station/offset, and nearest-point calculations.
- Vertical profiles and parabolic curves; LandXML interpretation.
- Superelevation, agency-specific transition methods, and guardrail calculation/output safeguards.
- Culvert hydraulics and explicit limits of simplified drainage calculations.
- CRS/datum handling, GNSS context, geotagged field evidence, and CAD/GIS interoperability.
- TIN/GeoTIFF conversion, elevation preservation, base-section quantities, and engineering regression QA.

Coverage reflects reviewed implementations. It is not a comprehensive design manual: hydrologic design methods, storm-sewer networks, complete roadside compliance, vertical-datum transformations, and survey certification require other evidence and governing references.

## Use and selective loading

Invoke it explicitly in Codex:

```text
$civil-engineering Review this station/offset calculation and its unit handling.
```

Automatic selection is enabled by default. The description targets engineering behavior, analysis, and validation; purely visual UI edits and generic programming should not activate it. Selection is contextual, not a guaranteed keyword match.

Codex first sees the name and description. When selected, it reads the small [SKILL.md](SKILL.md), then only the domain references needed for the task. For example, a superelevation question starts with its single domain reference; a terrain conversion may additionally need coordinate systems. The provenance catalog is loaded for authority/evidence questions, not on every task.

## Install globally from one canonical checkout

Clone this repository to your chosen location, or use an existing checkout. From its root, run:

```sh
skill_repo="$(pwd -P)"
skill_link="$HOME/.codex/skills/civil-engineering"
mkdir -p "$HOME/.codex/skills"
if [ -e "$skill_link" ] || [ -L "$skill_link" ]; then
  printf 'Inspect the existing installation before changing it: %s\n' "$skill_link"
else
  ln -s "$skill_repo" "$skill_link"
fi
ls -ld "$skill_link"
readlink "$skill_link"
```

The repository remains the only copy. The symlink exposes its root `SKILL.md` globally; pulling or editing the checkout changes the installed content immediately. Keep the checkout at a stable path, and reopen the Codex session if its skill catalog has not refreshed. Moving the checkout requires updating the link after inspecting the old installation.

This installation path was verified with the installed Codex build during creation. Skill search locations can differ by release; current [Codex skill documentation](https://developers.openai.com/codex/skills) also documents the user-level `.agents/skills` location and symlink support. Verify discovery in your build before choosing a different location; do not create a second independent copy.

## Evidence and authority

[Provenance](references/provenance.md) records source snapshots, meaningful source locations, classifications, validation scope, disagreements, and intentional exclusions. Domain references use short source IDs and classification labels.

An equation in an application is not automatically a standard. Agency-specific behavior must retain its source, edition, applicability, and verification limits. A passing regression test demonstrates the tested behavior; a software comparison demonstrates agreement for the compared cases. Neither certifies every design, transformation, or field measurement.

This skill does not replace governing standards, engineering judgment, project specifications, or an Engineer of Record. Confirm current requirements before design use.

## Updating and contributing

1. Inspect the relevant calculation and evidence; identify what new knowledge would change future engineering decisions.
2. Classify it and record its source/version in provenance. Describe disagreements instead of silently choosing an implementation.
3. Update the smallest relevant reference. Change the entrypoint only when routing or shared constraints change.
4. Verify equations, dimensions, applicability, and numerical examples. Preserve independently validated baselines and quantify differences.
5. Review the entire Git diff for private data, copied manual content, unsupported authority claims, and unnecessary duplication; then commit the reviewed files.

The Git allowlist admits the entrypoint, README, ignore file, and reference Markdown only. It is a convenience, not a secret scanner: never add private project data, client identifiers, credentials, original photographs, or proprietary source code. Synthetic examples should preserve the relevant failure mode without reproducing a real project.
