FROM ghcr.io/k8s-at-home/ubuntu:latest

ARG VERSION

USER root

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# hadolint ignore=DL3008,DL3015,SC2086
RUN \
  apt-get -qq update \
  && apt-get -qq install -y curl \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && apt-get autoremove -y \
  && apt-get clean \
  && \
  rm -rf \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/ \
  && update-ca-certificates

USER kah

COPY ./apps/cloudflare-ddns/cloudflare-ddns.sh /entrypoint.sh
CMD ["/entrypoint.sh"]

LABEL \
  org.opencontainers.image.title="cloudflare-ddns" \
  org.opencontainers.image.source="https://github.com/onedr0p/home-ops/" \
  org.opencontainers.image.version="${VERSION}"