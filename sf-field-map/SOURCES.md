# SF Field Conditions Map — Source Manifest

**Date:** 2026-09-27

Official SF/DataSF sources are preferred. A source is not production-approved until its relevant fields, geography, and limitations are understood.

## S001 — Election Precincts — Current, Defined 2022
- **Agency:** San Francisco Department of Elections / DataSF
- **Dataset ID:** `d6x4-hefw`
- **Use:** neutral precinct reference boundaries.
- **Verified public geometry:** 514 precinct features in the current 2022-defined era.
- **Useful fields:** `prec_2022`; neighborhood label commonly exposed as `neigh22`.
- **Reliability:** HIGH.
- **Fallback:** versioned public GeoJSON snapshot from the SF civic-data project `sfbay/datadiver`; if used, the app labels that fallback visibly.

## S002 — San Francisco Land Use
- **Agency:** San Francisco Planning / DataSF
- **Dataset ID:** `c5ge-t6pj`
- **Use:** large-multifamily property layer.
- **Current snapshot observed:** `data_as_of` 2026-08-17.
- **Verified useful fields:** `ludb_id`, `mapblklot`, `resunits`, `resunits_s`, `geography_type`, `data_as_of`, geometry.
- **Current app query:** records with `resunits >= 20`.
- **Important interpretation:** rows can describe parcels, parcel groups, or analytical geography; the map must not imply building-door accessibility.
- **Reliability:** HIGH as an official Planning dataset, subject to its own data-quality limitations.

## S003 — Archived San Francisco Land Use 2023
- **Agency:** San Francisco Planning / DataSF
- **Dataset ID:** `fdfd-xptc`
- **Use:** visible runtime fallback/schema precedent only.
- **Fields:** parcel geometry, `mapblklot`, `resunits`, `restype`, and related land-use attributes.
- **Reliability for current conditions:** MEDIUM because it is archived.

## S004 — Streets — Active and Retired
- **Agency:** San Francisco Public Works / DataSF
- **Dataset ID:** `3psu-pn9h`
- **Update pattern:** daily.
- **Use:** base street geometry for hill/grade derivation; potentially useful for joining other street records by CNN.
- **Known field:** Centerline Network Number (CNN); class code 5 is residential street in the published documentation.
- **Caveat:** must filter retired/inactive streets appropriately.

## S005 — Elevation Contours
- **Agency:** City and County of San Francisco / DataSF
- **Dataset ID:** `rnbg-2qxw`
- **Description:** 5-foot elevation contours.
- **Use:** candidate elevation source for deriving/validating street grade.
- **Caveat:** contour-to-street grade requires interpolation and real-world validation.

## S006 — Slopes of 20% or Greater
- **Agency:** San Francisco Planning / DataSF
- **Dataset ID:** `3vv2-nvev`
- **Use:** validation/cross-check for steep-street classification, not necessarily the primary metric.
- **Caveat:** polygonal/binary slope layer is less intuitive than street-segment grade for field use.

## S007 — Police Department Incident Reports: 2018 to Present
- **Agency:** San Francisco Police Department / DataSF
- **Dataset ID:** `wg3w-h783`
- **Update pattern:** daily.
- **Use:** recent reported-incident points with user-selectable time window.
- **Useful fields:** incident date/time, category/subcategory, incident ID, published geographic fields.
- **Critical caveat:** SFPD maps locations to nearby intersections for privacy; exact-address precision must not be implied. SFPD also changed the intersection mapping method in April 2024.

## S008 — Temporary Street Closures
- **Agency:** SFMTA / DataSF
- **Dataset ID:** `8x25-yybr`
- **Update pattern:** public report issued daily; source database maintained continuously.
- **Use:** date/time-filtered street-line overlay.
- **Verified useful fields:** `case_num`, `case_name`, `type`, `status`, `start_dt`, `end_dt`, `loc_desc`, `cnn`, `street`, `from_st`, `to_st`, `direction`, `veh_imp`, `info`, line geometry.
- **Critical caveat:** does not represent every closure controlled by Public Works or SFPD.

## S009 — Street-Use Permits
- **Agency:** San Francisco Public Works / DataSF
- **Dataset ID:** `b6tj-gt35`
- **Update pattern:** daily, roughly one-day lag.
- **Use:** candidate construction/right-of-way disruption layer.
- **Critical caveat:** a permit is not proof of a full street closure; one permit may appear on multiple location rows.
- **Implementation question:** compare with active-only/current-upcoming permit datasets before selecting the final live layer.

## Rejected source

### R001 — `PARCEL_GEO` / `NR_UNITS` ArcGIS service
- **Rejected because:** metadata showed City of Seattle / King County, not San Francisco.
- **Project impact:** never used in map code or analysis.

## Source acceptance rule

A source moves from candidate to production only after:
1. schema is inspected;
2. required fields/geography are verified;
3. duplicate/one-to-many behavior is understood;
4. several real-world SF examples are spot-checked;
5. material limitations are represented in the UI or docs.
