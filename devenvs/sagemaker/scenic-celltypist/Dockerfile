FROM continuumio/miniconda3

RUN conda install -c conda-forge \
    scanpy \
    celltypist \
    scenicplus \
    python=3.10 \
    -y

ENTRYPOINT ["python"]
