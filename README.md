[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fqdrant-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/qdrant) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/qdrant)](https://hub.docker.com/r/readystack/qdrant) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/qdrant) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# Qdrant: ReadyStack build kit

The offline build kit for the Docker image `readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.20.2-CE-ubuntu24.04-r2](https://github.com/readystack-dev/qdrant/releases/tag/v1.20.2-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/qdrant/tags), manifest digest `sha256:2a3c73bda032227aefe7695f8a1ae7158d6b86201152f4339f182a530e97ad90`
- Product page: https://readystack.dev/products/qdrant
- Source and build recipe: https://readystack.dev/products/qdrant/recipe
- Build trail: https://readystack.dev/products/qdrant/trail/v1.20.2-CE-ubuntu24.04-r2
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=qdrant

## The image

Single self-contained container. Embedded on-disk storage, no datastore sidecar.

## Who uses Qdrant and why

Developers building semantic search, recommendations or retrieval for AI applications.

Qdrant is a vector database and similarity search engine. It stores vectors with a payload, finds the closest matches to a query vector, and filters results on the payload.

A typical use: A support team wants its help-centre search to find articles by meaning, not exact words. Each article is turned into an embedding and stored in Qdrant with its product and language; a user's question is embedded the same way, and Qdrant returns the closest articles for that product.

From the upstream project's own description: https://github.com/qdrant/qdrant.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-25 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 96 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`qdrant`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-25; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/qdrant.

## Download

From the [v1.20.2-CE-ubuntu24.04-r2 release](https://github.com/readystack-dev/qdrant/releases/tag/v1.20.2-CE-ubuntu24.04-r2): `ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r2.tar.gz` (920.6 MB), SHA-256 `11700bef8e934deaa58404319bf7bb80ef22ebd521e46219d637713332e9f505`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r2.rebuild.json.sigstore ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r2.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r2.tar.gz
cd v1.20.2-CE-ubuntu24.04-r2
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-qdrant-v1.20.2-CE-ubuntu24.04-r2.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/qdrant/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
