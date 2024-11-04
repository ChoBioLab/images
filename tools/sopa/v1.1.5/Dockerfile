# Stage 1: Build Baysor
FROM julia:1.10.5 AS baysor-builder

RUN apt-get update && apt-get install -y build-essential

# Julia Baysor environment
ARG CACHEBUST=1
RUN julia -e 'using Pkg; Pkg.add(PackageSpec(url="https://github.com/kharchenkolab/Baysor.git", rev="v0.7.0"));'

ENV LazyModules_lazyload=false

RUN julia -e 'import Baysor, Pkg; Pkg.activate(dirname(dirname(pathof(Baysor)))); Pkg.instantiate(); Pkg.build();'
RUN echo "export PATH=/root/.julia/bin/:$PATH" >> ~/.bashrc
RUN echo "alias julia='/usr/local/julia/bin/julia --sysimage=/root/.julia/scratchspaces/cc9f9468-1fbe-11e9-0acf-e9460511877c/sysimg/libbaysor.so'" >> ~/.bashrc
RUN ln -s /root/.julia/bin/baysor /usr/local/bin/baysor

RUN /root/.julia/bin/baysor --help

# Stage 2: Final image
FROM python:3.10-slim

# Set the working directory in the container
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libgl1-mesa-glx \
    libglib2.0-0 \
    wget \
    gcc \
    python3-venv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copy Julia from the first stage
COPY --from=baysor-builder /usr/local/julia /usr/local/julia

# Copy Baysor from the first stage
COPY --from=baysor-builder /usr/local/bin/baysor /usr/local/bin/baysor
COPY --from=baysor-builder /root/.julia /root/.julia

# Add Julia to PATH
ENV PATH="/usr/local/julia/bin:${PATH}"

# Clone the sopa repository
RUN git clone https://github.com/gustaveroussy/sopa.git --branch v1.1.5

# Install sopa and its dependencies using pip
RUN cd sopa && \
    pip install --no-cache-dir -e ".[cellpose,baysor,tangram]" && \
    rm -rf /root/.cache

# Set the working directory
WORKDIR /app/sopa

# Set the default command
CMD ["/bin/bash"]

