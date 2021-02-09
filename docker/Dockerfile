FROM frolvlad/alpine-glibc:alpine-3.12

LABEL maintainer="https://github.com/aymond/hive.factorio"
LABEL originalauthor="https://github.com/factoriotools/factorio-docker"

ARG USER=factorio
ARG GROUP=factorio
ARG PUID=1000
ARG PGID=1000
ARG WRITEFOLDER=/factorio
ARG DEBUG=TRUE

ENV PORT=34197 \
    RCON_PORT=27015 \
    VERSION=stable \
    WRITEFOLDER="${WRITEFOLDER}" \
    SAVES=${WRITEFOLDER}/saves \
    CONFIG=${WRITEFOLDER}/config \
    MODS=${WRITEFOLDER}/mods \
    SCENARIOS=${WRITEFOLDER}/scenarios \
    SCRIPTOUTPUT=${WRITEFOLDER}/script-output \
    PUID="$PUID" \
    PGID="$PGID" \
    DEBUG=${DEBUG}}

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]
RUN set -ox pipefail \
    && archive="/tmp/factorio_headless_x64_$VERSION.tar.xz" \
    && mkdir -p /opt ${WRITEFOLDER} \
    && apk add --update --no-cache --no-progress bash binutils curl file gettext jq libintl pwgen shadow su-exec \
    && curl -sSL "https://www.factorio.com/get-download/1.1.21/headless/linux64" -o "$archive" \
    && tar xf "$archive" --directory /opt \
    && chmod ugo=rwx /opt/factorio \
    && rm "$archive" \
    && ln -s "$SCENARIOS" /opt/factorio/scenarios \
    && ln -s "$SAVES" /opt/factorio/saves \
    && mkdir -p /opt/factorio/config/ \
    && addgroup -g "$PGID" -S "$GROUP" \
    && adduser -u "$PUID" -G "$GROUP" -s /bin/sh -SDH "$USER" \
    && chown -R "$USER":"$GROUP" /opt/factorio ${WRITEFOLDER}

COPY files/*.sh /
RUN ["chmod", "+x", "/docker-entrypoint.sh"]

VOLUME ["${WRITEFOLDER}"]
EXPOSE $PORT/udp $RCON_PORT/tcp
ENTRYPOINT ["/docker-entrypoint.sh"]
