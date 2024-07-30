FROM python:3.10.4-slim

WORKDIR /app
ADD corescpy/ /app

LABEL maintainer="christopher.tastad@mssm.edu"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir . \
    && pip install --no-cache-dir notebook \
    && rm -rf ./*
