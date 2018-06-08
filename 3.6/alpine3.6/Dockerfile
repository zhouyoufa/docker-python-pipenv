FROM python:3.6-alpine3.6
LABEL maintainer="iamzhouu@gmail.com"

# -- Install Pipenv:
RUN set -ex && pip install --upgrade pipenv;

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

# -- Install Application into container:
RUN set -ex && mkdir -p /usr/src/app

WORKDIR /usr/src/app

# -- Adding Pipfiles
ONBUILD COPY Pipfile Pipfile
ONBUILD COPY Pipfile.lock Pipfile.lock

# -- Install dependencies:
ONBUILD RUN set -ex \
	&& apk add --no-cache --virtual .build-deps \
		bzip2-dev \
		coreutils \
		dpkg-dev dpkg \
		expat-dev \
		gcc \
		gdbm-dev \
		libc-dev \
		libffi-dev \
		linux-headers \
		make \
		ncurses-dev \
		libressl \
		libressl-dev \
		pax-utils \
		readline-dev \
		sqlite-dev \
		tcl-dev \
		tk \
		tk-dev \
		xz-dev \
		zlib-dev \
    && pipenv install --deploy --system \
    && apk del .build-deps

CMD ["python", "--version"]