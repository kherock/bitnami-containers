FROM docker.io/bitnami/minideb:bullseye

ARG TARGETARCH

LABEL org.opencontainers.image.authors="https://bitnami.com/contact" \
      org.opencontainers.image.description="Application packaged by Bitnami" \
      org.opencontainers.image.ref.name="0.13.5-debian-11-r4" \
      org.opencontainers.image.source="https://github.com/bitnami/containers/tree/main/bitnami/metallb-speaker" \
      org.opencontainers.image.title="metallb-speaker" \
      org.opencontainers.image.vendor="VMware, Inc." \
      org.opencontainers.image.version="0.13.5"

ENV HOME="/" \
    OS_ARCH="${TARGETARCH:-amd64}" \
    OS_FLAVOUR="debian-11" \
    OS_NAME="linux"

COPY prebuildfs /
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip libc6 procps tar
RUN mkdir -p /tmp/bitnami/pkg/cache/ && cd /tmp/bitnami/pkg/cache/ && \
    if [ ! -f metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz ]; then \
      curl -SsLf https://downloads.bitnami.com/files/stacksmith/metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz -O ; \
      curl -SsLf https://downloads.bitnami.com/files/stacksmith/metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz.sha256 -O ; \
    fi && \
    sha256sum -c metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz.sha256 && \
    tar -zxf metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz -C /opt/bitnami --strip-components=2 --no-same-owner --wildcards '*/files' && \
    rm -rf metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz metallb-speaker-0.13.5-0-linux-${OS_ARCH}-debian-11.tar.gz.sha256
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN chmod g+rwX /opt/bitnami

ENV APP_VERSION="0.13.5" \
    BITNAMI_APP_NAME="metallb-speaker" \
    PATH="/opt/bitnami/metallb-speaker/bin:$PATH"

USER 1001
ENTRYPOINT [ "speaker" ]
CMD [ "--help" ]
