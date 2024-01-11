FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="${PATH}:/home/jenkins/.local/bin"

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    git \
    curl \
    software-properties-common \
    gpg-agent \
    gcc \
	> /dev/null && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install stable Pythons
RUN add-apt-repository ppa:deadsnakes/ppa > /dev/null

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    python3.9 \
    python3.9-venv \
    python3.10 \
    python3.10-venv \
    python3.11 \
    python3.11-venv \
    python3.12 \
    python3.12-venv \
	> /dev/null && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.9 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.11 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.12
    
RUN groupadd -g 1001 k8sworker && \
    useradd -u 1001 -g 1001 k8sworker && \
    mkdir /home/k8sworker && \
    chown k8sworker:k8sworker /home/k8sworker

ENV PATH="${PATH}:/home/k8sworker/.local/bin"

WORKDIR /home/k8sworker

USER k8sworker
