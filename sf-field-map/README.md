# SF Field Conditions Map

Traceable prototype of an interactive San Francisco field-conditions map using reliable public data.

## Product principles

- San Francisco only.
- Public/reliable data only; official SF/DataSF sources first.
- Precincts are neutral reference boundaries, not the forced aggregation unit for every layer.
- Operational conditions stay at their natural geography: parcels/properties for large multifamily, streets for hills/closures, points for reported incidents.
- Every visible feature gets a plain-language hover explanation and click-to-pin detail.
- Large multifamily is a proxy for possible apartment-access friction, not a claim that a building is inaccessible.
- No single blended canvassing-difficulty score in v1.

## Current checkpoint

Checkpoint 3B implements:

- current 2022-defined SF election precinct boundaries;
- current SF Planning land-use query for properties with 20+ residential units;
- switchable 20+/50+/100+/200+ thresholds;
- hover and click explanations;
- visible source/load status;
- a self-contained HTML/CSS/JS app shell with a dependency-free SVG map renderer.

The app tries official DataSF sources first and only uses a documented fallback visibly if a source request fails.

## Next layers

1. street-grade / hills;
2. time-filtered SFMTA temporary closures;
3. recent SFPD reported incidents;
4. Public Works construction / right-of-way disruptions.

## Data sources used at this checkpoint

- Precincts: SF Department of Elections / DataSF `d6x4-hefw`.
- Large multifamily: SF Planning San Francisco Land Use `c5ge-t6pj`, using public residential-unit count `resunits`.

The current Planning dataset is a snapshot of parcel/parcel-group land use first published and updated August 17, 2026. Public metadata notes that some major projects/buildings are represented as groups of parcels and that the dataset is not guaranteed error-free.

## Shareability

The intended final product is a static web application shareable by URL. No voter file, private campaign data, API secrets, or local-machine paths are required.
