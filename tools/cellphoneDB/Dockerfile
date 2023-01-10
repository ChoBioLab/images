FROM python:3.7

MAINTAINER <christopher.tastad@mssm.edu>

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    r-base \
    r-base-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    && pip install --upgrade pip \
    && pip install cellphonedb==3.1.0

RUN R -e "install.packages('devtools', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "install.packages('BiocManager', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "install.packages('ggraph', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "devtools::install_github('zktuong/ktplots', dependencies = TRUE)"

WORKDIR /data

CMD ["cellphonedb"]

