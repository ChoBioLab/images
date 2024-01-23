FROM python:3.10.4-slim

WORKDIR /app
ADD crispr/ /app

MAINTAINER christopher.tastad@mssm.edu

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN pwd -P
RUN ls
RUN ls crispr/
