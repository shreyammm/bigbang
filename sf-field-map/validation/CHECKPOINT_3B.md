# Checkpoint 3B — Packaging repair + shareable architecture

**Date:** 2026-09-27

## Why this checkpoint exists

The first Checkpoint 3 preview loaded the HTML without its sibling CSS/JS assets, so the map never initialized. This was a packaging failure, not a user or data error.

## Repair

- `app/index.html` is self-contained: CSS and JavaScript are inline.
- The map renderer is dependency-free SVG; no Leaflet or map-library CDN is required.
- Precincts load from official DataSF `d6x4-hefw`; a versioned public snapshot is only a visible fallback.
- Large multifamily loads from current SF Planning Land Use `c5ge-t6pj`, querying `resunits >= 20`; archived 2023 land use is a visible fallback only.
- Thresholds 20+/50+/100+/200+ remain testable and are not yet locked.
- Every implemented precinct/property has hover explanation and click-to-pin detail.
- Source/load status is shown in the UI so source substitution never occurs silently.

## Validation performed

- JavaScript syntax checked with Node (`node --check`).
- Current 2026 land-use field names cross-checked against public source consumers that query `c5ge-t6pj` and expose `resunits`, `mapblklot`, and `data_as_of`.
- Current precinct geometry/public snapshot cross-checked against `d6x4-hefw` and the 514-feature 2022 precinct era.
- Incorrect Seattle/King County parcel source was rejected and documented.

## Remaining limitation

Embedded file previews may block cross-origin public API requests. If that happens, the application shell still renders and reports the fetch failure. The intended final distribution is a normally hosted static site.
