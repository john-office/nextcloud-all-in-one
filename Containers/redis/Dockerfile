# syntax=docker/dockerfile:latest
# From https://github.com/docker-library/redis/blob/master/7.2/alpine/Dockerfile
FROM redis:7.2.6-alpine

COPY --chmod=775 start.sh /start.sh

RUN set -ex; \
    apk upgrade --no-cache -a; \
    apk add --no-cache openssl bash; \
    \
# Give root a random password
    echo "root:$(openssl rand -base64 12)" | chpasswd; \
    \
# Get rid of unused binaries
    rm -f /usr/local/bin/gosu;

USER redis
ENTRYPOINT ["/start.sh"]

HEALTHCHECK CMD redis-cli -a $REDIS_HOST_PASSWORD PING || exit 1
LABEL com.centurylinklabs.watchtower.enable="false"
