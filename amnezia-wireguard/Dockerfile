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
    && ln -sf /sbin/xtables-nft-multi /sbin/ip6tables \
    && ln -sf /sbin/xtables-nft-multi /sbin/iptables \
    && git clone --depth=1 --branch $AWG_TOOLS \
        "https://github.com/amnezia-vpn/amneziawg-tools.git" /tmp/wg-tools \
    && cd /tmp/wg-tools/src \
    && make \
    && make install \
    && git clone --depth=1 --branch $AWG_GO \
        "https://github.com/amnezia-vpn/amneziawg-go.git" /tmp/wireguard \
    && cd /tmp/wireguard \
    && make \
    && make install \
    && rm -f -r /tmp/* \
    && apk del --no-cache --purge \
        .build-dependencies \
        go
