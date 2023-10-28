FROM espressif/idf:release-v4.3 AS base

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ENV DEBIAN_FRONTEND=noninteractive \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get -y dist-upgrade \
    && apt-get -y install \
      bc \
      bison \
      build-essential \
      ca-certificates \
      clang \
      curl \
      flex \
      gcc \
      git \
      libncurses5-dev \
      python3 \
      python3-dev \
      python3-distutils \
      python3-pip \
      python3-setuptools \
      python3.8-venv \
      srecord \
      sudo \
      udev \
      xz-utils \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && usermod -a -G dialout $USERNAME \
    && usermod -a -G plugdev $USERNAME \
    && echo ". /opt/esp/idf/export.sh" >> /home/$USERNAME/.bashrc \
    && echo "export PATH=$PATH:/home/$USERNAME/.platformio/penv/bin" >> /home/$USERNAME/.bashrc \
    && /opt/esp/idf/install.sh \
    && mkdir -p /IdeaProjects \ 
    && chown -R $USERNAME:$USERNAME /opt/esp /IdeaProjects

USER $USERNAME

ADD --chown=$USERNAME:$USERNAME https://raw.githubusercontent.com/platformio/platformio-core-installer/master/get-platformio.py /tmp
RUN python3 /tmp/get-platformio.py

ENTRYPOINT ["/bin/bash", "-l", "-c"]
