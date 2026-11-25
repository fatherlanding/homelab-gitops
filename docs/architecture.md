# Architecture

## Hardware

| Item | Value |
|---|---|
| Machine | Old laptop (model to record) |
| CPU / RAM / storage | 8 threads, 10 GB RAM + 4 GB swap, 512 GB NVMe SSD (Micron 2200V) |
| OS | Ubuntu 26.04.1 LTS with CasaOS |
| Network | Wired Ethernet to a TP-Link Deco mesh node; fixed IP via Deco address reservation (done) |

## Services and ports

| Service | Stack | Port | Reachable from |
|---|---|---|---|
| MariaDB | databases | 3306 | Home LAN only |
| PostgreSQL | databases | 5432 | Home LAN only |
| Adminer | databases | 8080 | Home LAN only |
| Portainer | CasaOS app | To record | Home LAN only |
| Jellyfin | media | 8096 | Home LAN only |

No passwords, keys or public IP addresses in this file.

## Diagram

_Added in Phase 7._
