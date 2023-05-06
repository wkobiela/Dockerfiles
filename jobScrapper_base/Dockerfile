FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="${PATH}:/home/jenkins/.local/bin"

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    git \
    curl \
    software-properties-common \
    gpg-agent \
	> /dev/null && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN add-apt-repository ppa:deadsnakes/ppa > /dev/null

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    python3.7 \
    python3.7-venv \
    python3.8 \
    python3.8-venv \
    python3.9 \
    python3.9-venv \
    python3.10 \
    python3.10-venv \
    python3.11 \
    python3.11-venv \
	> /dev/null && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.7 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.8 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.9 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10 && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.11

ENV HOME /home/jenkins
RUN adduser --disabled-password --gecos '' jenkins && \
    usermod -u 1002 jenkins && \
    groupmod -g 1002 jenkins && \
    adduser jenkins jenkins && \
    adduser jenkins sudo && \
    mkdir -p "${HOME}/.ssh" && \
    mkdir -p /home/jenkins/test
    
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    echo '%jenkins ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER jenkins
WORKDIR /home/jenkins/test
