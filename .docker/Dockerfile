FROM python:3.7.0-alpine

RUN set -xe \
 && addgroup -g 1000 -S django \
 && adduser -u 1000 -S django -G django \
 && apk update --no-cache \
 && apk upgrade --no-cache \
 && apk add --no-cache --virtual .build-deps \
        build-base \
        linux-headers \
        gcc \
        postgresql-dev

WORKDIR /home/django
COPY requirements.txt ./

RUN set -xe \
 && pip install -r requirements.txt \
 && rm requirements.txt \
 && apk del .build-deps

USER django

EXPOSE 8500
