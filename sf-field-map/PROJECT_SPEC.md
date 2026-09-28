# SF Field Conditions Map — Project Spec

**Version:** 0.2  
**Date:** 2026-09-27

## Purpose

Build an interactive San Francisco field-conditions map for canvassing logistics using only reliable public data. Precincts are used for orientation; other phenomena remain at their most natural geography whenever possible.

## Scope and data policy

- San Francisco only.
- Current SF election precinct boundaries are the base reference geography.
- Reliable public data only.
- Prefer official City and County of San Francisco / DataSF sources.
- No voter files, person-level political targeting, private canvasser observations, or proprietary campaign data.
- Do not claim a condition the source cannot establish. Example: a 100-unit property may be a proxy for possible access friction but is not “confirmed inaccessible.”

## Required layers

### Precinct boundaries
- Thin neutral outlines.
- Hover/click shows precinct ID and neighborhood if available.
- Visually subordinate to operational layers.

### Large multifamily
- Primary geography: parcel/property or official grouped-parcel geometry.
- Display actual location rather than precinct-level density shading.
- Candidate buckets: 20–49, 50–99, 100–199, 200+ residential units.
- Hover explains unit count, why the feature is shown, source, and access-friction caveat.

### Hills / steep streets
- Primary geography: street segments.
- Prefer continuous or derived street grade.
- Official SF slope/elevation data used for validation.
- Hover explains street/segment, grade, category, source, and derivation.

### Reported incidents
- Primary geography: SFPD-provided approximate incident point/location.
- User-selectable recent period; test 30/90/180/365-day windows.
- Use “reported incidents” terminology, not an exact crime-risk score.
- Hover explains category, date/time, approximate location, privacy-masking caveat, and source.

### Temporary street closures
- Primary geography: affected street-segment geometry from SFMTA.
- Date/time controls filter to closures whose intervals overlap the selected window.
- Hover shows type/reason, street/cross streets, start/end, vehicle impact, case/project, and source.
- Do not shade whole precincts merely because a closure intersects them.

### Construction / ROW disruptions
- Public Works permit/location geometry or best source-supported representation.
- Visually distinct from confirmed closures.
- Hover explains permit purpose/status/location/date and that a permit does not necessarily mean a full closure.

## Interaction requirements

- Toggle every major layer independently.
- Hover = immediate plain-language explanation.
- Click = persistent detail panel.
- Pan and zoom.
- Date + start time + end time controls for time-sensitive overlays.
- Legend covers every symbol/line/fill and uses language that matches what the data actually prove.

## Visual principles

- Avoid a single blended “difficulty” score.
- Preserve different visual grammars: parcels for multifamily, lines for hills/closures, points/heat for incidents.
- Use progressive emphasis rather than alarm colors where practical.
- Keep map legible when multiple layers are active.

## Traceability requirements

Every derived feature must be traceable to:
1. source dataset;
2. source fields;
3. transformation/version;
4. derivation rule;
5. source check/retrieval date.

Core project files:

```text
sf-field-map/
├── README.md
├── PROJECT_SPEC.md
├── DECISIONS.md
├── SOURCES.md
├── DEPLOYMENT.md
├── app/
└── validation/
```

## Shareability

The final deliverable is a static web application shareable by a normal URL.

- End users should not need Python, a cloned repo, or ChatGPT.
- No secrets/private data/API keys embedded in browser code.
- Production assets should be bundled or self-contained.
- Public-data source and freshness metadata should be visible.
- Mostly static layers may ship as versioned snapshots.
- Time-sensitive layers should prefer official live public data when practical and retain a clearly labeled fallback snapshot.
- Desktop field-planning use is primary; tablet/mobile should remain reasonably usable.

## Current checkpoint acceptance criteria

Checkpoint 3B is accepted when:
- the app shell renders without sibling CSS/JS or mapping-library CDN dependencies;
- precinct outlines load from current official/public SF geography;
- current SF Planning multifamily records load using public residential-unit counts;
- 20+/50+/100+/200+ thresholds can be compared;
- hover/click explanations work;
- source/fallback status is visible rather than silent.

## Still open

- Final multifamily thresholds.
- Final hill-grade derivation and thresholds.
- Incident point vs cluster vs heat behavior at different zooms.
- Default incident time window.
- Best Public Works source for live construction/ROW disruption.
- Final colors, line weights, and basemap treatment.
