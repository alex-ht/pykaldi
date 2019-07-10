# Dockerfile for building PyKaldi image from Ubuntu 16.04 image
FROM ubuntu:18.04

RUN sed -i "s:archive.:tw.archive.:g" /etc/apt/sources.list
# Install necessary system packages
RUN apt-get update \
    && apt-get install -y \
    python3 \
    python3-pip \
    python2.7 \
    autoconf \
    automake \
    cmake \
    curl \
    g++ \
    git \
    graphviz \
    libatlas-base-dev \
    libtool \
    make \
    pkg-config \
    subversion \
    sox \
    unzip \
    wget \
    zlib1g-dev

# Make python3 default
RUN ln -s /usr/bin/python3 /usr/bin/python \
    && ln -s /usr/bin/pip3 /usr/bin/pip

# Install necessary Python packages
RUN pip install --upgrade pip \
    numpy \
    setuptools \
    pyparsing \
    jupyter \
    ninja

# Copy pykaldi directory into the container
ADD . /pykaldi

# Install Protobuf, CLIF, Kaldi and PyKaldi
WORKDIR /pykaldi/tools
RUN ./check_dependencies.sh
RUN ./install_protobuf.sh
RUN ./install_clif.sh
RUN ./install_kaldi.sh

WORKDIR /pykaldi
RUN python setup.py install
