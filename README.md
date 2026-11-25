# homelab-gitops

Infrastructure as code for my home server: an old laptop running CasaOS, with every service defined in this repo and deployed with Docker Compose. If the server is lost, this repo is enough to rebuild it.

> Status: repository structure in place. Services are being moved into code phase by phase (see Roadmap).

## Architecture

_Diagram coming in Phase 7. See [docs/architecture.md](docs/architecture.md)._

## Services

| Stack | Services | Folder | Status |
|---|---|---|---|
| Databases | MariaDB, PostgreSQL, Adminer | [stacks/databases](stacks/databases) | Planned (Phase 1) |
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

_Written in Phase 2._

## Backups and recovery

_Written in Phase 5._

## Security

- Secrets live in `.env` files on the server only; this repo holds `.env.example` files with variable names, never real values.
- Database ports are reachable on the home network only.

## Roadmap

- [x] Phase 0: Repository structure
- [ ] Phase 0: SSH key login, fixed IP reservation
- [ ] Phase 1: Database stack in Docker Compose
- [ ] Phase 2: Deploy from GitHub via Portainer stacks
- [ ] Phase 3: CI checks (compose validation, YAML lint, secret scan)
- [ ] Phase 4: Monitoring and alerts
- [ ] Phase 5: Nightly backups with a tested restore
- [ ] Phase 6: Firewall, remote access via Tailscale, automatic updates
- [ ] Phase 7: Architecture diagram and runbooks
