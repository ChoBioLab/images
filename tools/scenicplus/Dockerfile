FROM python:3.11.9-slim

# Install Git, Wget, Curl, and build tools
RUN apt-get update && \
    apt-get install -y \
    git \
    wget \
    python3-dev \
    build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    /bin/bash /tmp/miniconda.sh -b -p /opt/conda && \
    rm /tmp/miniconda.sh

# Set the path for Conda
ENV PATH="/opt/conda/bin:${PATH}"

# Set the working directory
WORKDIR /app

# Copy the Conda environment file and requirements file to the working directory
COPY environment.yml .
COPY requirements.txt .

# Create and activate the Conda environment
RUN conda env create -f environment.yml && \
    conda clean -afy

# Activate the Conda environment
ENV CONDA_DEFAULT_ENV="scenicplus"
ENV CONDA_PREFIX="scenicplus"
ENV PATH="/opt/conda/envs/scenicplus/bin:${PATH}"

# Install dependencies from requirements.txt within the activated Conda environment
RUN pip install --no-cache-dir -r requirements.txt
