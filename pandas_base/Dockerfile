FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="${PATH}:/home/jenkins/.local/bin"
ENV TZ Asia/Kuala_Lumpur

RUN echo $TZ > /etc/timezone && \
    apt-get -qq update > /dev/null && apt-get install -y tzdata --no-install-recommends > /dev/null && \
    rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
    systemd \
    build-essential \
    python3 \
    python3-dev \
    python3-venv \
    python3-pip \
    git \
	> /dev/null && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

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