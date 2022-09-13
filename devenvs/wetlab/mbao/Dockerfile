FROM rocker/r-ver:4.2.1

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    cmake \
    libcurl4-openssl-dev \
    libxml2-dev \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libglpk-dev \
    libcairo2-dev \
    libxt-dev \
    libproj-dev \
    libgdal-dev \
    libgeos-dev \
    libhdf5-dev \
    && rm -rf /var/lib/apt/lists/* \
    && R -q -e 'install.packages("curl")'

ENV RENV_VERSION 0.15.5

RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"

WORKDIR /depend
COPY renv.lock renv.lock
COPY DESCRIPTION DESCRIPTION

ENV RENV_PATHS_LIBRARY renv/library
RUN R -e "renv::restore()"
RUN R -e "renv::install()"

