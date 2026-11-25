# homelab-gitops

Infrastructure as code for my home server: an old laptop running CasaOS, with every service defined in this repo and deployed with Docker Compose. If the server is lost, this repo is enough to rebuild it.

> Status: repository structure in place. Services are being moved into code phase by phase (see Roadmap).

## Architecture

_Diagram coming in Phase 7. See [docs/architecture.md](docs/architecture.md)._

## Services

| Stack | Services | Folder | Status |
|---|---|---|---|
| Databases | MariaDB 12.3, PostgreSQL 17, Adminer | [stacks/databases](stacks/databases) | Ready to deploy ([runbook](docs/runbooks/deploy-database-stack.md)) |
| Monitoring | Uptime Kuma, Grafana, Prometheus | [stacks/monitoring](stacks/monitoring) | Planned (Phase 4) |
| Media | Jellyfin | [stacks/media](stacks/media) | Planned |

## Repository layout

```
stacks/        one folder per Docker Compose stack
scripts/       backup and restore scripts
ansible/       server setup as code
docs/          architecture, runbooks, decision records
.github/       CI checks that run on every push
```

## How to deploy

Each stack has its own folder with a `compose.yml` and a `.env.example`. On the server: copy `.env.example` to `.env`, fill in real values, then run `docker compose up -d` in that folder. Step-by-step: [deploy the database stack](docs/runbooks/deploy-database-stack.md). Deploying straight from GitHub through Portainer comes in Phase 2.

## Backups and recovery

_Written in Phase 5._

## Security

- Secrets live in `.env` files on the server only; this repo holds `.env.example` files with variable names, never real values.
- Database ports are reachable on the home network only.

## Roadmap

- [x] Phase 0: Repository structure
- [x] Phase 0: SSH key login
- [x] Phase 0: Fixed IP reservation
- [ ] Phase 1: Database stack in Docker Compose
- [ ] Phase 2: Deploy from GitHub via Portainer stacks
- [ ] Phase 3: CI checks (compose validation, YAML lint, secret scan)
- [ ] Phase 4: Monitoring and alerts
- [ ] Phase 5: Nightly backups with a tested restore
- [ ] Phase 6: Firewall, remote access via Tailscale, automatic updates
- [ ] Phase 7: Architecture diagram and runbooks
