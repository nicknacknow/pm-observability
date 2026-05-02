# pm-observability

Shared observability stack for local PM services.

## Services

- Prometheus for metrics scraping and alert rules
- Grafana for dashboards and alert views
- Loki for container logs

## Run

```bash
docker network create pm-observability
cp .env.example .env
docker compose up -d
```

## Notes

- Add new scrape targets in `prometheus/prometheus.yml`.
- Prometheus scrapes `pm-trades-db` from `pm-trades-db:8001/metrics`.
- Prometheus scrapes `pminspect` from `pminspect:8001/metrics`.
- Prometheus also scrapes Postgres via `postgres_exporter`.
- Grafana auto-loads `metrics-pm-trades-db` and `metrics-pminspect` dashboards from provisioning.
- The `pminspect` dashboard is split into `Overview`, `Throughput`, and `Logs`.
- Grafana also shows `pminspect` logs from Loki on the same dashboard.
- Grafana starts with the built-in `admin` / `admin` login. (to change u may need to run `docker compose down -v` to clear volume)
- The stack is meant to be reused across `pminspect`, `pm-trades-db`, and other services.

All three compose projects attach to the shared `pm-observability` network. That lets Prometheus scrape both services by name while each service keeps the same internal metrics port (`8001`).

## TODO:

- add healthchecks
