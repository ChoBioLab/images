FROM continuumio/miniconda3

RUN conda config --add channels defaults && \
    conda config --add channels bioconda && \
    conda config --add channels conda-forge && \
    conda config --set channel_priority strict && \
    conda install -c conda-forge -c bioconda \
    scanpy \
    celltypist \
    scenicplus \
    python=3.10 \
    -y

ENTRYPOINT ["python"]
