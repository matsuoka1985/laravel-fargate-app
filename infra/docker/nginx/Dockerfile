FROM node:20-alpine AS node
FROM nginx:1.27-alpine
LABEL maintainer="ucan-lab <yes@u-can.pro>"
SHELL ["/bin/ash", "-oeux", "pipefail", "-c"]

ENV TZ=UTC

RUN apk update && \
  apk add --update --no-cache --virtual=.build-dependencies g++
RUN apk add --no-cache libstdc++ libc6-compat

# node command
COPY --from=node /usr/local/bin /usr/local/bin
# npm command
COPY --from=node /usr/local/lib /usr/local/lib
# yarn command
COPY --from=node /opt /opt
# nginx config file
COPY ./infra/docker/nginx/*.conf /etc/nginx/conf.d/

COPY ./backend/public /work/backend/public


WORKDIR /work/backend
