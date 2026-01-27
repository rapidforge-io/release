<div align="center">
  <img width="1536" height="672" alt="RapidForge Banner" src="https://github.com/user-attachments/assets/f967eb2d-54c6-4835-97fc-e0780b297683" />
</div>

# RapidForge

**RapidForge** is a powerful tool for rapid application development and deployment. Get started quickly with our comprehensive documentation and resources.

## 📚 Resources

- 🌐 **Website**: [rapidforge.io](https://rapidforge.io/)
- 💻 **Source Code**: [rapidforge-io/rapidforge](https://github.com/rapidforge-io/rapidforge)
- 📦 **Latest Release**: [Download here](https://github.com/rapidforge-io/release/releases/latest)

## 🎥 Walkthrough Video

<div align="center">
  <a href="https://youtu.be/k8p6r3uzEnI?si=7tutiWTuQBOYG-Gj">
    <img src="https://img.youtube.com/vi/k8p6r3uzEnI/maxresdefault.jpg" alt="RapidForge Walkthrough" style="width:100%;max-width:800px;">
  </a>
  <p><em>Click the image above to watch our walkthrough video</em></p>
</div>

## 🐳 Docker Quick Start

Get started with RapidForge using Docker with the sample Dockerfile below:

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

### Building and Running

```bash
# Build the Docker image
docker build -t rapidforge:latest .

# Run the container
docker run -p 8080:8080 rapidforge:latest
```

## 🚀 Features

- **Fast Development**: Rapidly build and deploy applications
- **Key-Value Store**: Built-in SQLite3 support for data persistence
- **Containerized**: Easy deployment with Docker
- **Cross-Platform**: Available for Linux, macOS, and Windows

## 📖 Getting Started

Visit our [documentation](https://rapidforge.io/) for detailed setup instructions and usage guides.

## 📄 License

Please refer to the main repository for license information.

---

<div align="center">
  Made with ❤️ by the RapidForge team
</div>
