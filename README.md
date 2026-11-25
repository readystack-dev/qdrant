# Qdrant: ReadyStack build kit

The offline build kit for the Docker image `readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.20.2-CE-ubuntu24.04-r2](https://github.com/readystack-dev/qdrant/releases/tag/v1.20.2-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/qdrant:v1.20.2-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/qdrant/tags), manifest digest `sha256:2a3c73bda032227aefe7695f8a1ae7158d6b86201152f4339f182a530e97ad90`
- Product page: https://readystack.dev/products/qdrant
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=qdrant

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/qdrant/recipe. The complete kit is the release download. Each release is a tag here.
