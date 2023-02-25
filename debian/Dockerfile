ARG FROM_REPO=debian
ARG FROM_TAG=bullseye-slim

FROM ${FROM_REPO}:${FROM_TAG}

ARG USER_UID=500 \
    DISTRIB_CODENAME=bullseye

LABEL description=$DESCRIPTION \
      team_owner=$TEAM

# Add common tools
ENV TZ="Europe/Lisbon"
ENV DEBIAN_FRONTEND=noninteractive
ENV DISTRIB_CODENAME=${DISTRIB_CODENAME}

# Copy configs
COPY configs/etc/apt/apt.conf.d /etc/apt/apt.conf.d/
COPY configs/etc/dpkg/dpkg.cfg.d /etc/dpkg/dpkg.cfg.d/
COPY configs/var/lib/locales/supported.d /var/lib/locales/supported.d


RUN rm -rf /usr/share/doc/ && \
    rm -rf /usr/share/man/

RUN set -e && \
    apt-get update && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    dumb-init \
    gnupg \
    procps \
    --no-install-recommends --no-install-suggests && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/archives \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add unpriviliged user
RUN adduser --disabled-password --gecos "" --uid ${USER_UID} --shell /bin/false debianite && \
    mkdir -p /apps && \
    chown -R debianite /apps
USER debianite
WORKDIR /home/indie/

# Set entrypoint to Yelp's dumb init
ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["/bin/bash"]
