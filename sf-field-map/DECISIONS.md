# SF Field Conditions Map — Decision Log

**Date:** 2026-09-27

Consequential project choices are recorded here rather than silently changed.

| ID | Status | Decision | Rationale |
|---|---|---|---|
| D001 | APPROVED | Scope is San Francisco only. | The intended field use is SF-specific. |
| D002 | APPROVED | Use reliable public data only. | No voter file, private canvasser observations, or proprietary campaign data. |
| D003 | APPROVED | Prefer official SF / DataSF sources. | Most authoritative for precincts, land use, incidents, closures, and permits. |
| D004 | APPROVED | Precincts are neutral reference boundaries, not the forced aggregation unit for every condition. | Precinct-level proportions can hide where a condition actually occurs. |
| D005 | APPROVED | Preserve the natural geography of each layer. | Parcels/buildings, streets, points, and precincts answer different operational questions. |
| D006 | APPROVED | Large multifamily is a proxy for possible apartment-access friction, not confirmed inaccessibility. | Public unit-count data cannot establish lobby/door access. |
| D007 | APPROVED | Show large multifamily at parcel/property geometry rather than primarily shading precincts by density. | More intuitive spatial understanding. |
| D008 | OPEN / TEST | Test 20–49, 50–99, 100–199, and 200+ unit buckets before locking thresholds. | SF's actual distribution should determine the most useful cutoffs. |
| D009 | APPROVED | Hills should be shown on street segments, not as average precinct elevation. | Walking difficulty occurs on streets. |
| D010 | OPEN / TEST | Prefer continuous/derived street grade with official slope data used as a cross-check. | Continuous grade is more informative but needs validation. |
| D011 | APPROVED | SFPD layer is labeled “reported incidents,” not an exact crime-risk score. | SFPD incident geography is privacy-masked and counts have interpretation limits. |
| D012 | OPEN / TEST | Test 30/90/180/365-day incident windows. | No default window has been approved yet. |
| D013 | APPROVED | Temporary street closures render as affected street lines and respond to selected date/time. | This reflects the source geometry and temporal nature of closures. |
| D014 | APPROVED | Public Works permits/construction are visually distinct from confirmed SFMTA closures. | A permit does not necessarily imply a full closure. |
| D015 | APPROVED | Every visible feature gets a plain-language hover explanation. | The user wants to know what a visual feature means and why it appears. |
| D016 | APPROVED | Hover = quick explanation; click = persistent richer detail. | Supports scanning and inspection. |
| D017 | APPROVED | No single blended canvassing-difficulty score in v1. | Different conditions imply different operational responses. |
| D018 | APPROVED | Keep sources, transformations, and version history traceable. | User wants to review how each layer was produced. |
| D019 | APPROVED | Final product must be shareable by normal URL as a static web app. | Others should not need Python, a local server, or this ChatGPT conversation. |
| D020 | APPROVED | No private data, secrets, API keys, or machine-specific paths in the deployable app. | Required for safe portable sharing. |
| D021 | APPROVED | Data freshness/source status should be visible in-product. | Shared users need to understand whether a layer is current. |
| D022 | APPROVED | Static layers may ship as versioned snapshots; time-sensitive layers should prefer official live data with a labeled fallback. | Improves reliability without hiding freshness. |
| D023 | APPROVED / IMPLEMENTED | Review build is self-contained HTML with inline CSS/JS and a dependency-free SVG renderer. | Fixes the first preview's sibling-file/CDN failure. |
| D024 | APPROVED / IMPLEMENTED | Precinct loading uses official DataSF first, with a versioned public fallback only if visibly disclosed. | Avoids silent substitution. |
| D025 | APPROVED / IMPLEMENTED | Current SF Planning Land Use `c5ge-t6pj` uses `resunits` for the large-multifamily query. | Current public source consumers and the 2026 snapshot confirm the field. |
| D026 | REJECTED SOURCE | Do not use the surfaced `PARCEL_GEO` / `NR_UNITS` ArcGIS service. | Validation showed it was Seattle/King County, not San Francisco. |

## Change-control rule

If an approved decision is reversed, add a new decision that explicitly supersedes the prior one. Do not erase the old rationale.
