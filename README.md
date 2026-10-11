# splunk-sports-telemetry

Real sports play-by-play data, streamed into Splunk and shown on dashboards built entirely from Splunk 10.4 custom visualizations.

> **Status:** early development. This README grows as each phase lands. See [CHANGELOG.md](CHANGELOG.md).

## What it does

A Go collector pulls WNBA play-by-play (shots with court coordinates, win probability, box scores) and sends it to Splunk over the HTTP Event Collector (HEC). A disk-backed queue keeps data safe if Splunk is down. Custom visualizations turn it into a live game view and post-game analysis.

NFL comes next, a very different data shape (drives, downs, field position), to show the same pipeline handles any data. NBA follows. It uses the same data format as the WNBA, so adding it tests that the collector is truly reusable (configuration, not new code) and makes side-by-side league comparisons possible.

Inspired by the F1 telemetry → Splunk demo shown at Splunk .conf 2026.

## Architecture

See [docs/architecture.md](docs/architecture.md).

## Roadmap

- [ ] Splunk 10.4 in Docker with HEC
- [ ] Go collector: backfill, replay, live modes
- [ ] Explore the data, then design custom visualizations and dashboards around it
- [ ] NFL as a second source
- [ ] NBA as a third source

## License

[Apache-2.0](LICENSE)
