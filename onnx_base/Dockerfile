FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="${PATH}:/home/jenkins/.local/bin"

RUN apt-get -qq update > /dev/null && apt-get -qq install -y --no-install-recommends \
	python3 \
	git \
	cmake \
	python3-pip \
	python3-dev \
	build-essential \
	sudo \
 	adduser \
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

RUN python3 -m venv /home/jenkins/system_venv
ENV PATH="$PATH:/home/jenkins/system_venv/bin"

RUN which pip && \
    pip install --no-cache-dir \
	pytest \
	nbval \
	pytest-html \
	parameterized
