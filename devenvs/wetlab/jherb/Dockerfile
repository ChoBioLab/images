FROM public.ecr.aws/c8r7r8g5/chobiolab/devenvs/r:r-4.2.1-e16f0bc

WORKDIR /dep
COPY DESCRIPTION DESCRIPTION

ENV RENV_PATHS_LIBRARY renv/library
RUN R -e "renv::install()"

