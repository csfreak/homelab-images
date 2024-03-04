FROM docker.homelab.csfreak.com/library/ubuntu:latest

ENV SONARR_BRANCH="main"
ARG SONARR_VERSION
ARG SONARR_CHANNEL="v4-stable"
ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_CONFIG_HOME="/config/xdg"

RUN \
    echo "**** install packages ****" && \
    apt-get update && \
    apt-get install -y \
    --no-install-recommends \
    --no-install-suggests \
    ca-certificates-mono \
    mono-devel \
    mono-vbnc && \
    apt-get install -y \
    jq \
    curl \
    mediainfo && \
    echo "**** install sonarr ****" && \
    mkdir -p /app/sonarr/bin && \
    if [ -z ${SONARR_VERSION+x} ]; then \
    SONARR_VERSION=$(curl -sX GET http://services.sonarr.tv/v1/releases \
    | jq -r ".[] | select(.releaseChannel==\"${SONARR_CHANNEL}\") | .version"); \
    fi && \
    curl -o \
    /tmp/sonarr.tar.gz -L \
    "https://services.sonarr.tv/v1/update/${SONARR_BRANCH}/download?version=${SONARR_VERSION}&os=linuxmusl&runtime=netcore&arch=x64" && \
    tar xf \
    /tmp/sonarr.tar.gz -C \
    /app/sonarr/bin --strip-components=1 && \
    echo "UpdateMethod=docker\nBranch=${SONARR_BRANCH}\nPackageVersion=${VERSION}\nPackageAuthor=[homelab.csfreak.com](https://console-openshift-console.apps.homelab.csfreak.com)" > /app/sonarr/package_info && \
    rm -rf /app/sonarr/bin/Sonarr.Update && \
    echo "**** cleanup ****" && \
    apt-get clean && \
    rm -rf \
    /tmp/* \
    /var/tmp/* && \
    chown -R 1025:100 /app/sonarr

USER 1025:100
EXPOSE 8989
VOLUME /config
VOLUME /media
VOLUME /downloads

CMD ["mono", "--debug", "/app/sonarr/bin/Sonarr.exe", "-nobrowser", "-data=/config"]

LABEL tv.sonarr.version ${SONARR_VERSION}