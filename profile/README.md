# x3s.host

[![Build and Push Images](https://github.com/x3s-host/x3s/actions/workflows/build-and-push-images.yml/badge.svg)](https://github.com/x3s-host/x3s/actions/workflows/build-and-push-images.yml)
[![React Doctor Score](https://img.shields.io/badge/React%20Doctor-92%2F100-great?style=flat-square&color=2ea043)](https://github.com/x3s-host/.github/blob/main/profile/README.md#react-doctor-score-x3s-hostx3s)

Sovereign hosting for AI agent runtimes.

x3s.host runs a stability-first hosting platform for agent containers using a split control-plane/runtime architecture and image-based production deployments.

## Repositories

- Platform: [`x3s-host/x3s`](https://github.com/x3s-host/x3s)
- Org profile/docs: [`x3s-host/.github`](https://github.com/x3s-host/.github)

## React Doctor Score (`x3s-host/x3s`)

- **Latest score:** **92 / 100** (`Great`)
- **Warnings:** 339 across 278/283 files
- **Last checked:** 2026-03-01
- **Command:** `npx -y react-doctor@latest . --verbose`

## Architecture Snapshot

- **Control Plane (Coolify host)**
  - Coolify orchestration
  - `coolify-proxy` / Traefik
  - No tenant workloads

- **Runtime Plane (worker hosts)**
  - x3s backend/frontend runtime containers
  - Tenant runtime containers
  - Deployment destinations in Coolify

- **Build Plane (CI)**
  - GitHub Actions builds Docker images
  - Images published to GHCR
  - Coolify deploys pinned image tags

## Release Workflow

1. Merge to `main` in `x3s-host/x3s`.
2. GitHub Actions builds and pushes backend/frontend images.
3. Promote tag-pinned refs into deploy env.
4. Run preflight + role audit checks.
5. Deploy through Coolify to runtime destinations.

## Operator Commands (from `x3s` repo)

```bash
./scripts/infra-role-audit.sh
./scripts/deploy-preflight.sh
./scripts/promote-release-images.sh <tag>
```

## Operational Rules

- Control-plane servers are `control` role only.
- Runtime scheduling is limited to `runtime` / `hybrid` roles.
- Production deploys are image-based for core services.
- Secrets are never committed; rotate immediately if exposed.

## Links

- Website: https://x3s.host
- Support: support@x3s.host
- Org: https://github.com/x3s-host
