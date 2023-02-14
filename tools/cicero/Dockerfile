FROM public.ecr.aws/chobiolab/seurat:latest

WORKDIR /data

MAINTAINER christopher.tastad@mssm.edu

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

RUN R -e "install.packages('devtools')" \
RUN R -e "install.packages('BiocManager')" \
RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "BiocManager::install(c('Gviz', 'GenomicRanges', 'rtracklayer'))" \
RUN R -e "devtools::install_github('cole-trapnell-lab/cicero-release', ref = 'monocle3')" \
RUN R -e "devtools::install_github('cole-trapnell-lab/monocle3')"

