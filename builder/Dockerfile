
FROM    multiarch/alpine:aarch64-edge
#FROM    multiarch/alpine:armhf-edge

ADD     repositories /etc/apk/repositories
RUN     apk add --upgrade apk-tools && \
        apk -U add alpine-sdk

RUN     mkdir -p /var/cache/distfiles && \
        adduser -D packager && \
        addgroup packager abuild && \
        chgrp abuild /var/cache/distfiles && \
        chmod g+w /var/cache/distfiles && \
        echo "packager    ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN     apk add --update ccache 

ENV     PATH="/usr/lib/ccache/bin:$PATH"

ADD     setup.sh /home/packager/bin/setup.sh

RUN     sed -i 's|JOBS=2|JOBS=$(nproc)|' /etc/abuild.conf

WORKDIR /work
USER    packager
