FROM alpine:3.20

ENV AWG_TOOLS=v1.0.20241018
ENV AWG_GO=v0.2.12

SHELL ["/bin/sh", "-o", "pipefail", "-c"]

RUN \
    apk add --no-cache --virtual .build-dependencies \
        build-base \
        linux-headers \
        git \
    && apk add --no-cache \
        go \
        iptables \
        libqrencode-tools \
        openresolv \
        bash \
        ca-certificates \
    && ln -sf /sbin/xtables-nft-multi /sbin/ip6tables \
    && ln -sf /sbin/xtables-nft-multi /sbin/iptables \
    && git clone --depth=1 --branch ${AWG_TOOLS} \
        https://github.com/amnezia-vpn/amneziawg-tools.git /tmp/wg-tools \
    && cd /tmp/wg-tools/src && make && make install \
    && git clone --depth=1 --branch ${AWG_GO} \
        https://github.com/amnezia-vpn/amneziawg-go.git /tmp/wireguard \
    && cd /tmp/wireguard && make && make install \
    && rm -f -r /tmp/* \
    && apk del --no-cache --purge .build-dependencies go

COPY rootfs /

ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION}
