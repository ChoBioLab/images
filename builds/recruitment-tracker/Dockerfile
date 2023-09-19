# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Clone your GitHub repository into the container
RUN git clone https://github.com/ibdgc/ibdgc-db.git .

# Copy the requirements file into the container
COPY ./requirements.txt requirements.txt

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Install the current repository as a Python package
RUN pip install .

# Set environment variables (replace with your actual values)
ENV REDCAP_API_TOKEN=""
ENV AWS_ACCESS_KEY_ID=""
ENV AWS_SECRET_ACCESS_KEY=""
ENV S3_BUCKET_NAME=""

# Make the script executable
RUN chmod +x ./reports/recruitment/redcap_recruitment_summary.sh

# Run the script to export from REDCap, execute the notebook, convert to HTML, and upload to S3
CMD ["./reports/recruitment/redcap_recruitment_summary.sh"]
