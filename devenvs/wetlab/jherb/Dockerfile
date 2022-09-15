ARG TAG
ARG R_VER

FROM public.ecr.aws/c8r7r8g5/chobiolab/devenvs/r:r-${R_VER}-${TAG}

WORKDIR /dep
COPY DESCRIPTION DESCRIPTION

ENV RENV_PATHS_LIBRARY renv/library
RUN R -e "renv::install()"

