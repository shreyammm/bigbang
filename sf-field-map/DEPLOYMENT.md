# SF Field Conditions Map — Deployment Architecture

## Goal

Publish a normal web URL that another person can open without installing anything.

## Production shape

```text
public-source refresh scripts
        ↓
versioned processed GeoJSON / JSON snapshots
        ↓
static web app build
        ↓
dist/
        ↓
static host / shareable URL
```

## Data strategy

**Mostly static layers** — precincts, large multifamily, and derived hill grades can ship as versioned processed snapshots with source dates.

**Time-sensitive layers** — SFMTA closures, Public Works permits, and recent SFPD incidents should prefer live official public API requests where practical, display freshness metadata, and retain a labeled last-known snapshot fallback so an outage does not create an unexplained blank layer.

## Product rules

- no voter files or private campaign data;
- no secrets/API keys in browser code;
- no machine-specific paths;
- source and freshness metadata visible;
- hover/click behavior works from the hosted URL;
- final static artifact is portable;
- normal laptop browser is primary; tablet/mobile remains usable.

## Review-build architecture

Checkpoint 3B is intentionally self-contained in `app/index.html`: inline CSS/JavaScript and a dependency-free SVG map renderer. This prevents the failure seen in the first chat preview, where sibling CSS/JS and Leaflet CDN dependencies were not loaded.

## GitHub workflow

Current work lives on the `sf-field-map` branch under `sf-field-map/` so the existing repository's `main` branch remains untouched until reviewed. The preferred final state is a dedicated repository or an explicitly approved merge/deployment target.
