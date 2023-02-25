ARG VERSION=3.16

FROM alpine:$VERSION

LABEL version=$VERSION

RUN apk update && \
  apk upgrade && \
  apk --no-cache add \
    tzdata \
    ca-certificates \
    procps \
    gnupg \
    bash \
    curl \
    upx \
    tini && \
  curl -sfL https://github.com/powerman/dockerize/releases/download/v0.11.5/dockerize-`uname -s`-`uname -m` \
    | install /dev/stdin /usr/local/bin/dockerize && \
  upx -9 /usr/local/bin/dockerize && \
  adduser -D -g "" -u 10001 -s /bin/false alpinite && \
  mkdir -p /apps && \
  chown -R alpinite /apps

ENV TZ=Europe/Lisbon \
    LANG=pt_PT.UTF-8 \
    LANGUAGE=pt_PT.UTF-8 \
    LC_ALL=pt_PT.UTF-8

RUN cp /usr/share/zoneinfo/$TZ /etc/localtime && \
  echo $TZ > /etc/timezone && \
  apk del tzdata upx && \
  rm -rf /var/cache/apk/*

USER indie

WORKDIR /apps

ENTRYPOINT ["/sbin/tini", "--"]
