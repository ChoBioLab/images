FROM python:3.7

MAINTAINER <christopher.tastad@mssm.edu>

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    r-base \
    && pip install --upgrade pip \
    && pip install cellphonedb==3.1.0

WORKDIR /data

CMD ["cellphonedb"]

