# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Clone your GitHub repository into the container
RUN git clone https://github.com/ibdgc/ibdgc-db.git .

# Copy the requirements file into the container
COPY requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Install the current repository as a Python package
RUN pip install ibdgc-db/
