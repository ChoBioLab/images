FROM python:3.8.19-slim

MAINTAINER <christopher.tastad@mssm.edu>

# Set the working directory inside the container
WORKDIR /app

# Install necessary system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libxml2-dev \
    libxslt-dev \
    && rm -rf /var/lib/apt/lists/*

# Upgrade pip
RUN pip install --upgrade pip

# Install the stlearn package and python deps
RUN pip install numpy==1.22.4
RUN pip install -U stlearn

# Modify the source code
RUN sed -i '77s/np.int/np.int64/' /usr/local/lib/python3.8/site-packages/stlearn/tools/microenv/cci/permutation.py

CMD ["stlearn"]
