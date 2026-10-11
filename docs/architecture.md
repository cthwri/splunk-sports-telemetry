# Architecture

> Planned design. Updated as components are built.

```
ESPN API ──backfill / poll──▶ collector (Go, single binary)
                                ├─ raw JSON cache (local disk)
                                ├─ normalize → events
                                ├─ disk-backed queue ──batch──▶ Splunk HEC :8088
                                └─ /status page + heartbeat events

Splunk 10.4 (Docker)
  ├─ index=wnba        game, play, shot, win-probability events
  ├─ index=collector   collector heartbeats and health
  └─ Dashboard Studio + custom visualization app
```

## Collector modes

| Mode | What it does |
|---|---|
| `backfill` | Loads every game in a season. Event time = when the play happened. |
| `replay` | Re-sends a finished game paced by its real timestamps (1x or faster), so dashboards look live any time of year. |
| `live` | Polls in-progress games and sends new plays, deduplicated by play id. |

## Design choices

Sources and sinks are interfaces, so each new league (NFL, NBA) is a new source, not a new collector. Decisions are logged in [decisions/](decisions/).
