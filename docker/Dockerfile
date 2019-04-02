FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04

RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    sudo \
    git \
    bzip2 \
    libx11-6 \
    wget \
    python3-dev \
    libopenmpi-dev \
    python3-pip \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libfontconfig1 \
    libxrender1 \
    swig \
    cmake \
    zlib1g-dev \
    ffmpeg \
    freeglut3-dev \
    xvfb \
    vim \
 && rm -rf /var/lib/apt/lists/*

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# Create a working directory
RUN mkdir /app
WORKDIR /app

# Create a non-root user and switch to it
RUN adduser --disabled-password --gecos '' --shell /bin/bash user \
 && chown -R user:user /app
RUN echo "user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-user
USER user

# All users can use /home/user as their home directory
ENV HOME=/home/user
RUN chmod 777 /home/user

ENV PATH="/home/user/.local/bin:${PATH}"

RUN \
    python3 -m pip install --user --upgrade pip && \
    python3 -m pip install --user jupyter && \
    python3 -m pip install --user box2d-py && \
    python3 -m pip install --user pybullet && \
    python3 -m pip install --user pytablewriter && \
    python3 -m pip install --user pyyaml


RUN \
    git clone https://github.com/ebots-inc/spinningup.git  && \
    cd spinningup && \
    python3 -m pip install --user -e .

CMD /bin/bash
