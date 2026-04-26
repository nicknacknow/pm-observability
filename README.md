# pm-observability

Shared observability stack for local PM services.

## Services

- Prometheus for metrics scraping and alert rules
- Grafana for dashboards and alert views

## Run

```bash
cp .env.example .env
docker compose up -d
```

## Notes

- Add new scrape targets in `prometheus/prometheus.yml`.
- Prometheus scrapes `pm-trades-db` from `host.docker.internal:8001/metrics`.
- Prometheus also scrapes Postgres via `postgres_exporter`.
- Grafana starts with the built-in `admin` / `admin` login. (to change u may need to run `docker compose down -v` to clear volume)
- The stack is meant to be reused across `pminspect`, `pm-trades-db`, and other services.

## TODO:

- add healthchecks
