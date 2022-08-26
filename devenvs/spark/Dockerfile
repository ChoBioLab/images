FROM rocker/rstudio:4.2.1

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
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
    && rm -rf /var/lib/apt/lists/* \
    && R -q -e 'install.packages("curl")'

ENV RENV_VERSION 0.15.5

RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"
RUN R -e "install.packages('BiocManager')"
RUN R -e "install.packages('devtools')"
RUN R -e "install.packages('tidyverse')"

RUN groupadd --gid 1001 cholab
RUN for i in \
    chris \
    jiayu; \
    do \
    useradd --gid cholab -ms /bin/bash "$i"; \
    echo "${i}:password" | chpasswd; \
    done

WORKDIR /project
COPY renv.lock renv.lock

ENV RENV_PATHS_LIBRARY renv/library
RUN R -e "renv::restore()"

WORKDIR /data
RUN chmod 777 /data
