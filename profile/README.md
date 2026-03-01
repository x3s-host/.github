# x3s.host

Sovereign hosting for AI agent runtimes.

x3s.host provides managed deployment and operations for agent containers with a control-plane + worker architecture, runtime isolation, and image-based production releases.

## What We Operate

- Control plane: Coolify orchestration and proxy management
- Runtime workers: app and tenant workload execution
- CI build plane: GitHub Actions builds and publishes Docker images to GHCR

## Platform Principles

- Stability first: keep control-plane hosts out of workload scheduling
- Image-only production deploys: avoid host-side source builds for core services
- Region-aware placement: strict infra policy and health-based server selection
- Security by default: secret hygiene, scoped credentials, and explicit preflight checks

## Core Repository

- Product repo: [`x3s-host/x3s`](https://github.com/x3s-host/x3s)

## Release Flow

1. Merge to `main`
2. GitHub Actions builds and pushes backend/frontend images to GHCR
3. Promote tag-pinned image refs into deploy env
4. Run deployment preflight and infra role audits
5. Deploy through Coolify to runtime worker destinations

## Operations Commands (from `x3s` repo)

```bash
./scripts/infra-role-audit.sh
./scripts/deploy-preflight.sh
./scripts/promote-release-images.sh <tag>
```

## Architecture (Current)

- **Control host role:** `control`
- **Worker host role:** `runtime` (or `hybrid` when explicitly intended)
- Placement excludes control-plane hosts for runtime deployments.

## Security Notes

- Never commit live secrets
- Use test keys in non-production environments
- Rotate credentials immediately on exposure

## Contact

- Support: `support@x3s.host`
- Website: `https://x3s.host`
