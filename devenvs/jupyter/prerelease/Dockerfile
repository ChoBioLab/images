FROM public.ecr.aws/chobiolab/nebraska:prerelease

MAINTAINER christopher.tastad@mssm.edu

RUN pip3 install \
    'jupyterhub==4.*' \
    'notebook==7.*'

# create a user, since we don't want to run as root
RUN useradd -m jovyan
ENV HOME=/home/jovyan
WORKDIR $HOME
USER jovyan

CMD ["jupyterhub"]

