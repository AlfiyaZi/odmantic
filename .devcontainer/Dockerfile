FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies.
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    make \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    wget \
    curl \
    llvm \
    libncurses5-dev \
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    git \
    git-lfs \
    ca-certificates \
    libffi-dev \
  && apt-get clean autoclean \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/* \
  && rm -f /var/cache/apt/archives/*.deb

# Install ``pyenv``.
RUN git clone https://github.com/pyenv/pyenv /root/.pyenv

# Install the desired versions of Python.
RUN for PYTHON_VERSION in 3.6.12 3.7.9 3.8.6; do \
  set -ex \
    && /root/.pyenv/bin/pyenv install ${PYTHON_VERSION} \
    && /root/.pyenv/versions/${PYTHON_VERSION}/bin/python -m pip install --upgrade pip \
  ; done

ENV PATH /root/.pyenv/versions/3.6.12/bin:${PATH}
ENV PATH /root/.pyenv/versions/3.7.9/bin:${PATH}
ENV PATH /root/.pyenv/versions/3.8.6/bin:${PATH}

# Install task
RUN curl -sL https://taskfile.dev/install.sh | sh
ENV PATH /root/.bin/:${PATH}

# Install devtools
RUN python3.8 -m pip install poetry
RUN python3.8 -m pip install tox
RUN python3.8 -m pip install pre-commit
