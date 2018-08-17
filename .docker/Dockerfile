
FROM alpine:latest as base

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH
ENV PYTHON_PIP_VERSION 18.0
ENV LANG C.UTF-8

RUN set -ex; \
    addgroup -g 1000 -S django; \
    adduser -u 1000 -S django -G django; \
    echo -e '#!/bin/sh\npython manage.py $@' >> /usr/bin/manage; \
    chmod +x /usr/bin/manage; \
    mkdir /home/django/src; \
    chown -R django /home/django; \
    apk update; \
    apk add --no-cache python3 py3-psycopg2 gettext ca-certificates; \
    cd /usr/bin; \
	ln -s pydoc3 pydoc; \
	ln -s python3 python; \
	wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
	python get-pip.py \
		--disable-pip-version-check \
		--no-cache-dir \
		"pip==$PYTHON_PIP_VERSION" \
	; \
	pip --version; \
	find /usr/ -depth \
		\( \
			\( -type d -a \( -name test -o -name tests \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' +; \
	rm -f get-pip.py


FROM base as dependencies

RUN set -ex; \
	apk add --no-cache --virtual .build-deps \
    build-base \
    python3-dev \
    linux-headers \
    gcc \
    postgresql-dev

WORKDIR /build

COPY requirements.txt ./
RUN pip install -r requirements.txt


FROM base as develop

COPY --from=dependencies /root/.cache /build/requirements.txt /root/.cache/

RUN set -xe; \
    pip install -r /root/.cache/requirements.txt; \
    rm -rf /root/.cache;

WORKDIR /home/django/src
USER django
EXPOSE 8500
