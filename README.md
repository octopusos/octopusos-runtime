# octopusos-runtime (Release Artifacts Repo)

This is a **release artifacts repository** used by OctopusOS Desktop (Electron) to download
sidecar binaries:
- `octopusos-runtime` (OctopusOS backend runtime)
- `ollama` (local model server)

Design goals:
- End users never run CLI commands.
- Desktop app can auto-download verified binaries if they are missing/corrupted.

## Repo Layout

- `artifacts/` (optional): local staging area (not required by GitHub Releases).
- `manifest.json`: machine-readable mapping from platform to download URL + sha256 for both sidecars.
- `scripts/`: helper scripts to build and publish releases from the main monorepo.

## Publishing

From the main monorepo root:

```bash
bash scripts/desktop/publish_runtime_repo.sh
```

This builds a platform-specific `octopusos-runtime-*` binary, fetches and extracts the upstream
Ollama binary, updates `manifest.json`, commits + tags, and (if `gh` is installed) creates a
GitHub Release with uploaded assets.
