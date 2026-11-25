# Qdrant v1.20.2 — ReadyStack release `v1.20.2-CE-ubuntu24.04-r2`

Generated 2026-11-25 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2` (linux/amd64). Index digest `sha256:856d8eb9087b1e7b643c62c32d37c24f8eef18ec484433b87c44180af6426bb5` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:2a3c73bda032227aefe7695f8a1ae7158d6b86201152f4339f182a530e97ad90` [`TARGET_DIGEST.txt`].
- **Upstream:** Qdrant v1.20.2 built from source at `v1.20.2` of https://github.com/qdrant/qdrant (the web UI in /qdrant/static is upstream's prebuilt release https://github.com/qdrant/qdrant-web-ui/releases/download/v0.2.18/dist-qdrant.zip (sha256 `fdce24c04ec1…`)) — upstream notes: https://github.com/qdrant/qdrant/releases/tag/v1.20.2 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** `ubuntu:24.04`; runtime user `qdrant`.
- **Build:** `source-rebuild-rust`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v1.20.2-CE-ubuntu24.04-r1`.

## What changed in this release

- Upstream version unchanged (v1.20.2); ReadyStack rebuild.
- Qdrant v1.20.2 is unchanged from the release this supersedes (v1.20.2-CE-ubuntu24.04-r1); this release rebuilds it. Changes: libssh-4 moves from 0.10.6-2ubuntu0.5 to 0.10.6-2ubuntu0.6 (USN-9187-1). Settings, ports and data volumes are those of v1.20.2-CE-ubuntu24.04-r1: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-25)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `qdrant` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.
- **Before exposing this service:** Without QDRANT__SERVICE__API_KEY, anyone who reaches ports 6333/6334 can read, change and delete all collections, including through the dashboard. Set an API key, or keep the ports on a private network.
- **Before exposing this service:** Traffic is plain HTTP/gRPC unless you enable TLS (QDRANT__SERVICE__ENABLE_TLS=true with QDRANT__TLS__CERT and QDRANT__TLS__KEY); an API key crosses the network in clear text without it.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:2a3c73bda032227aefe7695f8a1ae7158d6b86201152f4339f182a530e97ad90`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 4 of 4 use cases passed (5 authored, 4 kept in the suite; 1 not exercised, see below) against the running image [`docs/validation/test-results.json`].
- 1 further authored check was not exercised and is not counted above: it used a method this release's API does not offer on that path (listed under Not exercised in `docs/validation/FAILED_TESTS.md`).

## Known issues

- **high** (upstream): Unauthenticated access by default [`RSD-qdrant-ace5db2625`]

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

