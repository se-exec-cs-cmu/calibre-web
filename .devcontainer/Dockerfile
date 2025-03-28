ARG BASE_IMAGE=mcr.microsoft.com/devcontainers/python:1-3.12-bullseye
FROM ${BASE_IMAGE} AS base

RUN apt-get update \
 && apt-get install -y \
        curl \
        gcc \
        git \
        libldap2-dev \
        libsasl2-dev \
        libssl-dev \
        sqlite3 \
        unrar-free \
 && rm -rf /var/lib/apt/lists/*

# install calibre
# FIXME pick URL based on arch
ENV CALIBRE_VERSION 6.4.0
ENV X86_64_URL "https://download.calibre-ebook.com/${CALIBRE_VERSION}/calibre-${CALIBRE_VERSION}-x86_64.txz"
ENV AARCH64_URL "https://download.calibre-ebook.com/${CALIBRE_VERSION}/calibre-${CALIBRE_VERSION}-arm64.txz"
ENV CALIBRE_URL "https://download.calibre-ebook.com/${CALIBRE_VERSION}/calibre-${CALIBRE_VERSION}-arm64.txz"
RUN mkdir -p /opt/calibre \
 && wget -nv -O /tmp/calibre.txz "${CALIBRE_URL}" \
 && tar -xJf /tmp/calibre.txz -C /opt/calibre
ENV PATH "/opt/calibre:${PATH}"

# install reqs
WORKDIR /tmp
COPY requirements.txt optional-requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt \
 && pip install --no-cache-dir -r optional-requirements.txt
