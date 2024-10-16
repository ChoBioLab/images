# Use Miniconda base image
FROM continuumio/miniconda3:latest

# Set the working directory in the container
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    wget \
    unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Download and set up Baysor binary
RUN wget https://github.com/kharchenkolab/Baysor/releases/download/v0.7.0/baysor-x86_x64-linux-v0.7.0_build.zip \
    && unzip baysor-x86_x64-linux-v0.7.0_build.zip -d /opt/Baysor \
    && rm baysor-x86_x64-linux-v0.7.0_build.zip

# Add Baysor to PATH
ENV PATH="/opt/Baysor/bin/baysor/bin:${PATH}"

# Clone the sopa repository
RUN git clone https://github.com/gustaveroussy/sopa.git --branch v1.1.5

# Create a conda environment
RUN conda create --name sopa python=3.10 -y

# Set up shell to use conda
SHELL ["conda", "run", "-n", "sopa", "/bin/bash", "-c"]

# Activate conda environment and install sopa with extras
RUN cd sopa && \
    conda install datrie && \
    pip install -e ".[snakemake,cellpose,baysor,tangram]"

# Set the default command to activate the conda environment and run bash
CMD ["conda", "run", "-n", "sopa", "/bin/bash"]
