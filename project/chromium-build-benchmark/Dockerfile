# Use an official Ubuntu base image with Docker already installed
FROM ubuntu:22.04

WORKDIR /src

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Install Mantatory tools (curl git python3) and optional tools (vim sudo)
RUN apt-get update && \
    apt-get install -y curl git lsb-release python3 git file vim sudo time && \
    rm -rf /var/lib/apt/lists/* && \
    git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git

# Export depot_tools path
ENV PATH="/src/depot_tools:${PATH}"

WORKDIR /src/chromium
RUN fetch --nohooks chromium

WORKDIR /src/chromium/src
RUN ./build/install-build-deps.sh && \
    gclient runhooks && \
    gn gen out/Default

CMD ["autoninja", "-C", "out/Default", "chrome"]
