FROM docker.io/bitnami/minideb:bullseye
ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-11" \
    OS_NAME="linux"

LABEL org.opencontainers.image.authors="https://bitnami.com/contact" \
      org.opencontainers.image.description="Application packaged by Bitnami" \
      org.opencontainers.image.ref.name="2.4.0-debian-11-r3" \
      org.opencontainers.image.source="https://github.com/bitnami/containers/tree/main/bitnami/influxdb" \
      org.opencontainers.image.title="influxdb" \
      org.opencontainers.image.vendor="VMware, Inc." \
      org.opencontainers.image.version="2.4.0"

COPY prebuildfs /
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip libc6 libgcc-s1 procps tar
RUN mkdir -p /tmp/bitnami/pkg/cache/ && cd /tmp/bitnami/pkg/cache/ && \
    if [ ! -f wait-for-port-1.0.3-154-linux-amd64-debian-11.tar.gz ]; then \
      curl -SsLf https://downloads.bitnami.com/files/stacksmith/wait-for-port-1.0.3-154-linux-amd64-debian-11.tar.gz -O ; \
    fi && \
    echo "74a09c2208af7316f32ee3ee8479d70b20ad54f1a989e84b6417e23c1f07c147  wait-for-port-1.0.3-154-linux-amd64-debian-11.tar.gz" | sha256sum -c - && \
    tar -zxf wait-for-port-1.0.3-154-linux-amd64-debian-11.tar.gz -C /opt/bitnami --strip-components=2 --no-same-owner --wildcards '*/files' && \
    rm -rf wait-for-port-1.0.3-154-linux-amd64-debian-11.tar.gz
RUN mkdir -p /tmp/bitnami/pkg/cache/ && cd /tmp/bitnami/pkg/cache/ && \
    if [ ! -f influxdb-2.4.0-0-linux-amd64-debian-11.tar.gz ]; then \
      curl -SsLf https://downloads.bitnami.com/files/stacksmith/influxdb-2.4.0-0-linux-amd64-debian-11.tar.gz -O ; \
    fi && \
    echo "dc179a42855ed905bd19434ff50a89a56e0e7a4ca34ea47995a335af0c2f271e  influxdb-2.4.0-0-linux-amd64-debian-11.tar.gz" | sha256sum -c - && \
    tar -zxf influxdb-2.4.0-0-linux-amd64-debian-11.tar.gz -C /opt/bitnami --strip-components=2 --no-same-owner --wildcards '*/files' && \
    rm -rf influxdb-2.4.0-0-linux-amd64-debian-11.tar.gz
RUN mkdir -p /tmp/bitnami/pkg/cache/ && cd /tmp/bitnami/pkg/cache/ && \
    if [ ! -f gosu-1.14.0-154-linux-amd64-debian-11.tar.gz ]; then \
      curl -SsLf https://downloads.bitnami.com/files/stacksmith/gosu-1.14.0-154-linux-amd64-debian-11.tar.gz -O ; \
    fi && \
    echo "e36c3d90f4fbfbe989f40947fa7c8ab817f12fcf97d3aef893c753a20ce976ab  gosu-1.14.0-154-linux-amd64-debian-11.tar.gz" | sha256sum -c - && \
    tar -zxf gosu-1.14.0-154-linux-amd64-debian-11.tar.gz -C /opt/bitnami --strip-components=2 --no-same-owner --wildcards '*/files' && \
    rm -rf gosu-1.14.0-154-linux-amd64-debian-11.tar.gz
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/influxdb/postunpack.sh
ENV APP_VERSION="2.4.0" \
    BITNAMI_APP_NAME="influxdb" \
    PATH="/opt/bitnami/common/bin:/opt/bitnami/influxdb/bin:$PATH"

VOLUME [ "/bitnami/influxdb" ]

EXPOSE 8086 8088

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/influxdb/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/influxdb/run.sh" ]
