# GENERATED L-009 hermetic Rust build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Cargo tree + web-vault + debs from Dockerfile.vendor.
FROM rust:1.98.1-bookworm@sha256:93ce27a88655056a51dbdd8f5f2d7ddc071c7b0070fb288a37b5a285fc83971e AS build_qdrant
# build-stage tools (strategy.build_packages) installed offline from the
# vendored deb closure — build.rs helpers like protoc live here.
RUN --mount=type=bind,source=vendored/build-debs,target=/tmp/bdebs \
    set --; for f in /tmp/bdebs/*.deb; do [ -e "$f" ] && set -- "$@" "$f"; done; \
    for pass in 1 2 3 4 5; do [ $# -eq 0 ] || dpkg -i --skip-same-version "$@" >/dev/null 2>&1 && break; done; \
    dpkg --configure -a && bad= && for d in "$@"; do p=$(dpkg-deb -f "$d" Package) v=$(dpkg-deb -f "$d" Version); \
      case "$(dpkg-query -W -f='${Version} ${db:Status-Abbrev}' "$p" 2>/dev/null)" in "$v ii"*) ;; *) bad="$bad $p=$v" ;; esac; done && \
    { [ -z "$bad" ] || { echo "vendored debs not installed at their vendored version:$bad" >&2; false; }; }
WORKDIR /src
COPY vendored/qdrant-src/ .
ENV CARGO_NET_OFFLINE=true CARGO_HOME=/usr/local/cargo RUSTUP_TOOLCHAIN=1.98.1
ARG SOURCE_DATE_EPOCH=1795672785
ENV SOURCE_DATE_EPOCH=${SOURCE_DATE_EPOCH}
RUN cargo build --release --offline --locked --bin qdrant && \
    cp target/release/qdrant /qdrant && /qdrant --version
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289
ENV DEBIAN_FRONTEND=noninteractive QDRANT__SERVICE__HOST=0.0.0.0 QDRANT__SERVICE__HTTP_PORT=6333 QDRANT__SERVICE__GRPC_PORT=6334 QDRANT__STORAGE__STORAGE_PATH=/qdrant/storage QDRANT__STORAGE__SNAPSHOTS_PATH=/qdrant/snapshots QDRANT__TELEMETRY_DISABLED=true RUN_MODE=production
RUN --mount=type=bind,source=vendored/debs,target=/tmp/debs \
    set --; for f in /tmp/debs/*.deb; do [ -e "$f" ] && set -- "$@" "$f"; done; \
    for pass in 1 2 3 4 5; do [ $# -eq 0 ] || dpkg -i --skip-same-version "$@" >/dev/null 2>&1 && break; done; \
    dpkg --configure -a && bad= && for d in "$@"; do p=$(dpkg-deb -f "$d" Package) v=$(dpkg-deb -f "$d" Version); \
      case "$(dpkg-query -W -f='${Version} ${db:Status-Abbrev}' "$p" 2>/dev/null)" in "$v ii"*) ;; *) bad="$bad $p=$v" ;; esac; done && \
    { [ -z "$bad" ] || { echo "vendored debs not installed at their vendored version:$bad" >&2; false; }; } && \
    rm -rf /var/lib/apt/lists/* \
           /var/log/dpkg.log /var/log/alternatives.log /var/log/apt /var/cache/ldconfig/aux-cache /var/cache/fontconfig
ARG SOURCE_DATE_EPOCH=1795672785
RUN groupadd -r qdrant && useradd -r -g qdrant -d /qdrant -m qdrant && \
    mkdir -p /qdrant/storage /qdrant/snapshots /qdrant/config /qdrant/static && chown -R qdrant:qdrant /qdrant/storage /qdrant/snapshots /qdrant/config /qdrant/static && \
    : "${SOURCE_DATE_EPOCH:?SOURCE_DATE_EPOCH must be set for a reproducible build}" && \
    sed -ri "s/^([^:]*:[^:]*):[0-9]*:/\1:$((SOURCE_DATE_EPOCH/86400)):/" /etc/shadow && \
    rm -f /etc/passwd- /etc/shadow- /etc/group- /etc/gshadow-
COPY --from=build_qdrant /qdrant /usr/bin/qdrant
COPY vendored/web-vault/ /qdrant/static/
COPY --from=build_qdrant /src/docs/redoc/master/openapi.json /qdrant/static/openapi.json
COPY --from=build_qdrant /src/config/config.yaml /qdrant/config/config.yaml
COPY --from=build_qdrant /src/config/production.yaml /qdrant/config/production.yaml
RUN chmod 755 /usr/bin/qdrant; rm -f /qdrant/static/qdrant-web-ui.spdx.json; chown -R qdrant:qdrant /qdrant/static; chown -R qdrant:qdrant /qdrant/static/openapi.json; chown -R qdrant:qdrant /qdrant/config/config.yaml; chown -R qdrant:qdrant /qdrant/config/production.yaml
LABEL org.opencontainers.image.title="Qdrant"
LABEL org.opencontainers.image.description="Qdrant provides a self-contained vector database for efficient similarity search and AI application development. It eliminates external dependencies by embedding storage directly within the service, simplifying infrastructure management for your team."
LABEL org.opencontainers.image.source="https://github.com/qdrant/qdrant"
LABEL org.opencontainers.image.version="v1.20.2-CE-ubuntu24.04-r3"
LABEL org.opencontainers.image.revision="23065a0bf6857c3e5da45f6c8939cc746cc0580e"
HEALTHCHECK --interval=5s --timeout=300s --start-period=10s \
  CMD curl -fsS -o /dev/null -w '%{http_code}' http://127.0.0.1:6333/healthz || exit 1
WORKDIR /qdrant
USER qdrant
EXPOSE 6333 6334
ENTRYPOINT ["/usr/bin/qdrant"]
