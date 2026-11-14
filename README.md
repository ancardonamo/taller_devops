# Taller DevOps - Observabilidad y Monitoreo

App Flask que expone métricas Prometheus (`webapp_visits_total`), Prometheus (scrape cada 5 s) y Grafana con dashboard aprovisionado, orquestados con Docker Compose y desplegados en EC2 con GitHub Actions.

| Servicio   | Puerto |
|------------|--------|
| app        | 8000   |
| prometheus | 9090   |
| grafana    | 3000   |

Workflows (`.github/workflows/`):
- `build-push.yml` – build de `app/` y push a GHCR con tag `latest`.
- `deploy-app.yml` – `workflow_dispatch` → SSH a EC2 → `git pull` → `docker compose up -d app`.
- `deploy-monitoring.yml` – cambios en `monitoring/` → SSH a EC2 → `git pull` → despliega prometheus y grafana.

Secrets requeridos: `EC2_HOST`, `EC2_USER`, `EC2_SSH_KEY`.
