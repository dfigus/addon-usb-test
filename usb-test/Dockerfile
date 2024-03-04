ARG BUILD_FROM
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

RUN \
    apk update \
    && apk add --no-cache  \
    alpine-sdk=1.0-r1 \
    git=2.43.0-r0 \
    linux-tools=6.6.4-r0 \
    linux-headers=6.5-r0 \
    linux-lts-dev=6.6.18-r0 \
    build-base=0.5-r3 \
    patchutils=0.4.2-r2 \
    perl-proc-processtable=0.636-r1 \
    python3=3.11.8-r0 \
    py3-pip=23.3.1-r0 \
    && pip3 install \
    --no-cache-dir \
    --prefer-binary \
    usb_resetter==1.3.0

# hadolint ignore=DL3003,DL3059
RUN \
       git clone https://github.com/ljalves/media_build.git /tmp/media_build \
    && git clone --depth=1 https://github.com/ljalves/linux_media.git -b latest /tmp/media \
    && cd /tmp/media_build \
    && make dir DIR=../media \
    && make distclean \
    && make

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Daniel Figus <10271668+dfigus@users.noreply.github.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="dfigus" \
    org.opencontainers.image.authors="Daniel Figus <10271668+dfigus@users.noreply.github.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/dfigus/addon-usb-test" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}