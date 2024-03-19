# Use the official Golang Docker image as base
FROM golang:1.19

# Install necessary system packages
RUN apt-get update && \
    apt-get install -y git && \
    apt-get install -y curl && \
    apt-get install -y gnupg2 && \
    apt-get install -y software-properties-common && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get install -y nodejs && \
    apt-get install -y gcc && \
    apt-get install -y musl-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Hugo Extended
RUN wget -O /tmp/hugo.tar.gz https://github.com/gohugoio/hugo/releases/download/v0.123.7/hugo_extended_0.123.7_Linux-64bit.tar.gz && \
    tar -xzf /tmp/hugo.tar.gz -C /tmp && \
    mv /tmp/hugo /usr/local/bin/hugo && \
    rm -rf /tmp/hugo.tar.gz

# Set environment variables
ENV HUGO_BIND=0.0.0.0 \
    HUGO_DESTINATION=public \
    HUGO_ENV=DEV \
    HOME=/tmp

# Set the working directory
WORKDIR /src

# Expose default Hugo port
EXPOSE 1313

# Set default command to start Hugo server
CMD ["hugo", "server", "--bind", "$HUGO_BIND", "--destination", "$HUGO_DESTINATION", "--environment", "$HUGO_ENV"]
