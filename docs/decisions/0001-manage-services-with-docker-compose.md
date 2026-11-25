# 0001: Manage services with Docker Compose files in Git

Date: 2026-11-25
Status: Accepted

## Context

Services were first installed by clicking in the CasaOS app store. That setup lives only on the server: it cannot be reviewed, versioned or rebuilt if the laptop fails.

## Decision

Every service is defined in a `compose.yml` under `stacks/`, committed to this repository, and deployed from it. Secrets stay in `.env` files on the server.

## Consequences

- The server can be rebuilt from the repository plus the `.env` files and backups.
- Every change has a commit history.
- A service must not also be managed through the CasaOS app store, or two tools will fight over the same container.
