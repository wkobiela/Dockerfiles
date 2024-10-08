FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="${PATH}:/home/jenkins/.local/bin"

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    chromium-browser \
    curl \
    gcc \
    git \
    gpg-agent \
    libasound2-dev \
    libatk-bridge2.0-0 \
    libatk1.0-0 \
    libatk1.0-0 \
    libcups2 \
    libdrm-dev \
    libgbm-dev \
    libnss3 \
    libpangocairo-1.0-0 \
    libxcb-randr0-dev \
    libxcb-shape0-dev \
    libxcb-xinerama0-dev \
    libxcb-xkb-dev \
    libxcb-xtest0-dev \
    libxcomposite-dev \
    libxdamage1 \
    libxkbcommon-x11-0 \
    libxrandr2 \
    software-properties-common \
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
    python3.13 \
    python3.13-venv \
	> /dev/null && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Enable installing pip other than from system packages for python3.12
ENV PIP_BREAK_SYSTEM_PACKAGES=1

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.9 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.11 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.12 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.13

RUN groupadd -g 1001 k8sworker && \
    useradd -u 1001 -g 1001 k8sworker && \
    mkdir /home/k8sworker && \
    chown k8sworker:k8sworker /home/k8sworker

ENV PATH="${PATH}:/home/k8sworker/.local/bin"

WORKDIR /home/k8sworker

USER k8sworker
