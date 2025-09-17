<img width="1536" height="672" alt="gbb" src="https://github.com/user-attachments/assets/f967eb2d-54c6-4835-97fc-e0780b297683" />

More information in https://rapidforge.io/. Checkout our [walkthrough video](https://youtu.be/k8p6r3uzEnI?si=7tutiWTuQBOYG-Gj)

Sample dockerfile for you to start with should you wish to use docker


```dockerfile


FROM debian:latest

# sqlite3 is required if you want Key-Value store to work
RUN apt-get update && apt-get install -y \
    ca-certificates \
    curl \
    jq \
    sqlite3 \
    tar \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Fetch the latest version dynamically from GitHub
ARG ARCH="x86_64"
ARG PLATFORM="Linux"
ARG BINARY_NAME="rapidforge"
RUN VERSION=$(curl -s https://api.github.com/repos/rapidforge-io/release/releases/latest | jq -r '.tag_name') && \
    TARBALL="${BINARY_NAME}_${PLATFORM}_${ARCH}.tar.gz" && \
    curl -L "https://github.com/rapidforge-io/release/releases/download/${VERSION}/${TARBALL}" -o ${TARBALL} && \
    tar -xzvf ${TARBALL} && \
    chmod +x ${BINARY_NAME} && \
    rm ${TARBALL}

ARG PORT=8080
ENV RF_PORT=$PORT
EXPOSE ${PORT}

CMD ["./rapidforge"]
```
