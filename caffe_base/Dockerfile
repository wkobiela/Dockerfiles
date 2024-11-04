FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="${PATH}:/home/jenkins/.local/bin"

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    git \
    cmake \
    build-essential \
    ca-certificates \
    libboost-all-dev \
    libblas-dev \
    libprotobuf-dev \
    protobuf-compiler \
    libgoogle-glog-dev \
    libgflags-dev \
    libhdf5-dev \
    libgflags-dev \
    liblmdb-dev \
    libleveldb-dev \
    libsnappy-dev \
    libatlas-base-dev \
	> /dev/null \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ENV HOME /home/jenkins
RUN adduser --disabled-password --gecos '' jenkins && \
    usermod -u 1002 jenkins && \
    groupmod -g 1002 jenkins && \
    adduser jenkins jenkins && \
    adduser jenkins sudo && \
    mkdir -p "${HOME}/.ssh"
    
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    echo '%jenkins ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER jenkins