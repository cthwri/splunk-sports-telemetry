# 0001: WNBA first, using the ESPN public API

**Date:** 2026-10-07 (updated 2026-10-10: NFL and NBA chosen as later sources)
**Status:** Accepted

## Context
The project needs real, free, event-level sports data with timestamps and positions, so the dashboards have something worth visualizing.

## Decision
Start with WNBA play-by-play from ESPN's public (undocumented) API. Add NFL second and NBA third, from the same API.

## Why
- ESPN returns about 420 plays per WNBA game, shot x/y coordinates, real wall-clock timestamps, and win probability. No API key needed.
- WNBA is less covered than NBA or NFL, so the project stands out.
- NFL data is a different shape (drives, downs, field position), which proves the pipeline is general.
- NBA uses the same format as WNBA, which tests that the collector is truly reusable.
- Knowing these sports well makes it easier to spot bad data and explain findings.

## Consequences
- The API is undocumented and could change. The collector caches raw JSON locally and keeps requests to 1 per second or fewer.
- One provider for all three leagues means an ESPN outage or change affects everything. The raw cache limits the damage.
- Fallback sources exist if ESPN changes: wehoop (WNBA), nflverse (NFL), hoopR (NBA).
- Season totals are spot-checked by hand against Sports Reference.
- Bulk API data is not committed to this repo. Only small test fixtures are.
