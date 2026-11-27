# Provenance — Qdrant (`v1.20.2-CE-ubuntu24.04-r3`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/qdrant/qdrant
- Revision built: `v1.20.2` (commit `23065a0bf6857c3e5da45f6c8939cc746cc0580e`)
- Source tree: `ce1013f7ea124065ee90ecd44ebeeb3c1f8fd53f9e8817aac93ba07e1a870712` over 2687 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-rust`; base image `ubuntu:24.04`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- Not compiled here, shipped as upstream's prebuilt files: the web UI in /qdrant/static is upstream's prebuilt release https://github.com/qdrant/qdrant-web-ui/releases/download/v0.2.18/dist-qdrant.zip (sha256 `fdce24c04ec1…`)
- SOURCE_DATE_EPOCH: `1795672785` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/qdrant:v1.20.2-CE-ubuntu24.04-r3` — index digest `sha256:cf1019f47c80973feb6ad0844a365f3a0f87e1b13bec08eafe476b023ad86b69` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:05f1c2e2f6e452fcfe234a5a90ccee89760b9235bb3e1c224c7a48735cac0795` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/qdrant:v1.20.2-CE-ubuntu24.04-r3`

## Pinned inputs, and why

- 25 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, language runtimes and toolchains 1, dependency versions readystack sets 9, files the vendor stage downloads 1, pins in the kit's dockerfiles 4, readystack's build engine 1, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r3.trail.json`, published beside this archive and signed with the release key (`ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r3.trail.json.sigstore`), and readable at https://readystack.dev/products/qdrant/trail/v1.20.2-CE-ubuntu24.04-r3.

