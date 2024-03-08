ARG BASE_IMAGE
ARG BASE_IMAGE_VERSION
FROM ${BASE_IMAGE}:${BASE_IMAGE_VERSION}

ARG BASE_IMAGE_USER=jboss

ADD --chown=${BASE_IMAGE_USER}:${BASE_IMAGE_USER} --chmod=777 https://github.com/Pugmatt/BedrockConnect/releases/latest/download/BedrockConnect-1.0-SNAPSHOT.jar .

EXPOSE 19132/udp