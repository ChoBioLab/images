FROM rocker/r-ver:4.2.2

WORKDIR /app
ADD . /app

MAINTAINER christopher.tastad@mssm.edu

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    zlib1g-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    libbz2-dev \
    liblzma-dev \
    libssl-dev \
    libpng-dev \
    libhdf5-dev \
    libglpk-dev \
    patch \
    git \
    && rm -rf /var/lib/apt/lists/*

ENV RENV_VERSION 0.17.3
ENV RENV_PATHS_CACHE_HOST=/opt/local/renv/cache
ENV RENV_PATHS_CACHE_CONTAINER=/renv/cache
ENV RENV_PATHS_CACHE=${RENV_PATHS_CACHE_CONTAINER}

VOLUME "${RENV_PATHS_CACHE_HOST}:${RENV_PATHS_CACHE_CONTAINER}"

RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"

ENV RENV_PATHS_LIBRARY renv/library
RUN R -e "renv::restore()"
