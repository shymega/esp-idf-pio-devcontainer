FROM espressif/idf:release-v5.0 AS base

ENV DEBIAN_FRONTEND=noninteractive \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get -y dist-upgrade \
    && apt-get -y install \
      bc \
      sudo \
      build-essential \
      ca-certificates \
      clang \
      curl \
      libncurses5-dev \
      flex \
      bison \
      gcc \
      git \
      python3 \
      python3-dev \
      python3-distutils \
      python3-pip \
      python3.8-venv \
      python3-setuptools \
      srecord \
      udev \
      xz-utils \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && echo ". /opt/esp/idf/export.sh" >> /root/.bashrc \
    && echo "export PATH=$PATH:/root/.platformio/penv/bin" >> /root/.bashrc \
    && /opt/esp/idf/install.sh \
    && mkdir -p /IdeaProjects

ADD https://raw.githubusercontent.com/platformio/platformio-core-installer/master/get-platformio.py /tmp
RUN python3 /tmp/get-platformio.py

ENTRYPOINT ["/bin/bash", "-l", "-c"]
