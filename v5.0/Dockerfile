FROM espressif/idf:release-v5.0 AS base

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
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && usermod -a -G dialout $USERNAME \
    && usermod -a -G plugdev $USERNAME \
    && echo ". /opt/esp/idf/export.sh" >> /home/$USERNAME/.bashrc \
    && echo "export PATH:$PATH:$HOME/.platformio/penv/bin" >> /home/$USERNAME/.bashrc \
    && /opt/esp/idf/install.sh \
    && chown -Rv $USERNAME:$USERNAME /opt/esp

USER $USERNAME
RUN python3 -c "$(curl -fsSL https://raw.githubusercontent.com/platformio/platformio/master/scripts/get-platformio.py)"

ENTRYPOINT ["/bin/bash"]
