ARG BUILD_FROM=hassioaddons/debian-base:3.2.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy Python requirements file
COPY requirements.txt /tmp/

# Setup base
RUN \
    apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        dirmngr \
        gpg-agent \
        gpg \    
    && curl -L https://apt.mopidy.com/mopidy.gpg | apt-key add - \
    && curl -L https://apt.mopidy.com/mopidy.list -o /etc/apt/sources.list.d/mopidy.list \
    \
    && apt-get update \

# Move access.log to stdout and error.log to stderr
RUN mkdir -p /var/log/nginx && ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Mopidy" \
    io.hass.description="Mopidy is an extensible music server" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Bram Mittendorff, Franck Nijhof, Robbert Müller" \
    org.opencontainers.image.title="Mopidy" \
    org.opencontainers.image.description="Mopidy is an extensible music server" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Bram Mittendorff, Franck Nijhof, Robbert Müller" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/hassio-addons/addon-mopidy" \
    org.opencontainers.image.documentation="https://github.com/hassio-addons/addon-mopidy/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
