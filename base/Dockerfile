FROM debian:bullseye-20230227-slim

ENV LANG=C.UTF-8 \
    USER=root HOME=/root \
    S6_CMD_WAIT_FOR_SERVICES=1 \
    S6_CMD_WAIT_FOR_SERVICES_MAXTIME=10000

ARG S6_VERSION=v2.2.0.3

COPY rootfs /

RUN apt_install \
      apt-utils \
      ca-certificates \
      git \
      gettext \
      less \
      nano \
      # temporary:
      curl \
\
 # S6 Overlay
 && cd /tmp \
 # Download
 && curl -LSs https://github.com/just-containers/s6-overlay/releases/download/$S6_VERSION/s6-overlay-amd64.tar.gz -o s6-overlay-amd64.tar.gz \
 # Install
 && tar -xzf s6-overlay-amd64.tar.gz -C / \
 # Clean
 && rm -rf /tmp/* \
 && apt_purge curl \
 && rm -rf /etc/init.d/ \
\
 && ln -s /bin/s6-setuidgid /bin/setuidgid

VOLUME /data
ENTRYPOINT ["/init"]
