# Use base image
FROM vpetukhov/baysor:v0.7.0

# Set the working directory in the container
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libgl1-mesa-glx \
    libglib2.0-0 \
    wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Download and install Miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh && \
    bash miniconda.sh -b -p /opt/conda && \
    rm miniconda.sh

# Add conda to path
ENV PATH="/opt/conda/bin:${PATH}"

# Initialize conda in bash and configure
RUN conda init bash && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc

# Clone the sopa repository
RUN git clone https://github.com/gustaveroussy/sopa.git --branch v1.1.5

# Create a conda environment and install packages in a single layer
RUN conda create -n sopa python=3.10 -y && \
    . /opt/conda/etc/profile.d/conda.sh && \
    conda activate sopa && \
    cd sopa && \
    pip install --no-cache-dir -e ".[snakemake,cellpose,baysor,tangram]" && \
    conda clean -afy && \
    rm -rf /root/.cache

# Set the default command to activate the conda environment and run bash
SHELL ["/bin/bash", "-c"]
ENTRYPOINT ["conda", "run", "-n", "sopa"]
CMD ["/bin/bash"]

