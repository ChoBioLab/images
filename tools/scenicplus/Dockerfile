FROM python:3.11.9-slim

# Install Git and Conda
RUN apt-get update && \
    apt-get install -y git wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

# Set the path for Conda
ENV PATH=/opt/conda/bin:$PATH

# Set the working directory
WORKDIR /app

# Copy the Conda environment file and requirements file to the working directory
COPY environment.yml .
COPY requirements.txt .

# Create and activate the Conda environment
RUN conda env create -f environment.yml && \
    conda clean -afy

# Activate the Conda environment
SHELL ["conda", "run", "-n", "scenicplus", "/bin/bash", "-c"]

# Install additional dependencies from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt
