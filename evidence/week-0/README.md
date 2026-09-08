# Week 0 Evidence

| File | Command | Proves |
|---|---|---|
| 01-containers-running.png | `docker compose up -d` + `docker compose ps` | §9 all containers healthy |
| 02-health-endpoint.png | `curl -i http://localhost:8081/health` | §5 health endpoint returns HTTP 200 |
| 03-ui-in-browser.png | http://localhost:8080 | §6 UI loads and calls API health endpoint |
| 04-sql-reachable-from-api.png | `/health/db`, `getent hosts sql`, `wget http://api:8080/health` | §9 SQL reachable from API; Docker DNS verified |
| 05-jwt-middleware.png | `curl -i http://localhost:8081/secure/ping` | §1 JWT middleware enabled (401 without token) |
| 06-volume-persistence.png | insert row → `docker compose down` → `up` → row still present | §4/§9 named volume `sql_data` survives container recreation |

All container-to-container traffic uses Docker service names (`sql`, `api`), never `localhost`.
The two `localhost` references in docker-compose.yml are healthchecks a container runs
against its own process, not traffic between containers.
