FROM python:3.10.12-alpine

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

RUN git clone https://github.com/nickvsnetworking/pyhss.git

RUN apk update && \
    apk add --no-cache --virtual .build-deps \
        python3-dev \
        build-base \
        pkgconfig \
        libffi-dev \
        openssl-dev \
        bash \
        gcc \
        g++ \
        musl-dev \
        linux-headers \
        libxml2-dev \
        libxslt-dev \
        yaml-dev \
        py3-yaml && \
    apk add mariadb-dev lksctp-tools-dev && \
    pip install --upgrade pip setuptools wheel && \
    pip install --no-cache-dir -r /pyhss/requirements.txt && \
    apk del .build-deps

WORKDIR /pyhss/services

ENTRYPOINT ["sh", "-c", "python apiService.py & python hssService.py & python diameterService.py & wait"]
