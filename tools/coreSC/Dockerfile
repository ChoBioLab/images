FROM rocker/r-ver:4.2.1

MAINTAINER christopher.tastad@mssm.edu

WORKDIR /app
RUN git clone git@github.com:ChoBioLab/coreSC.git &&
    cd coreSC &&
    git checkout bcd3de7

zlib1g-dev
libxml2-dev
libcurl4-openssl-dev
libbz2-dev
liblzma-dev
libssl-dev
libpng-dev
libgsl-dev
libgeos-dev
libhdf5-dev

CMD ['./run']
