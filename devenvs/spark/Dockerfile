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
    && rm -rf /var/lib/apt/lists/* \
    && R -q -e 'install.packages("curl")'

ENV RENV_VERSION 0.15.5

RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"

WORKDIR /project
COPY renv.lock renv.lock
COPY DESCRIPTION DESCRIPTION

ENV RENV_PATHS_LIBRARY renv/library
RUN R -e "renv::restore()"
RUN R -e "renv::install()"

#ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
#ENV PATH /opt/conda/bin:$PATH
#
#RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O ~/miniconda.sh && \
#    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
#    rm ~/miniconda.sh && \
#    /opt/conda/bin/conda clean -tipsy && \
#    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
#    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
#    echo "conda activate base" >> ~/.bashrc
#
#ENV TINI_VERSION v0.16.1
#ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
#RUN chmod +x /usr/bin/tini
#
#WORKDIR /working
#COPY environment.yml .
#RUN conda env create -f environment.yml
#
#SHELL ["conda", "run", "-n", "myenv", "/bin/bash", "-c"]
#RUN R -e "reticulate::install_miniconda()"









#RUN groupadd --gid 1001 cholab
#RUN for i in \
#    chris \
#    jiayu; \
#    do \
#    useradd --gid cholab -ms /bin/bash "$i"; \
#    echo "${i}:password" | chpasswd; \
#    done
#
#WORKDIR /mnt/cho_lab/disk2
#RUN chmod 777 /mnt/cho_lab/disk2





#ARG UBUNTU_VER=18.04
#ARG CONDA_VER=latest
#ARG OS_TYPE=x86_64
#ARG PY_VER=3.9
#ARG PANDAS_VER=1.3
#
#FROM ubuntu:${UBUNTU_VER}
## System packages
#RUN apt-get update && apt-get install -yq curl wget jq vim
#
## Use the above args
#ARG CONDA_VER
#ARG OS_TYPE
## Install miniconda to /miniconda
#RUN curl -LO "http://repo.continuum.io/miniconda/Miniconda3-${CONDA_VER}-Linux-${OS_TYPE}.sh"
#RUN bash Miniconda3-${CONDA_VER}-Linux-${OS_TYPE}.sh -p /miniconda -b
#RUN rm Miniconda3-${CONDA_VER}-Linux-${OS_TYPE}.sh
#ENV PATH=/miniconda/bin:${PATH}
#RUN conda update -y conda
#RUN conda init
#
#ARG PY_VER
#ARG PANDAS_VER
## Install packages from conda
#RUN conda install -c anaconda -y python=${PY_VER}
#RUN conda install -c anaconda -y \
#    pandas=${PANDAS_VER}
