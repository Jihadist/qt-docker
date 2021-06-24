FROM atom63/qt-docker:qemu_linux-qt5-armv7a-static-cmake
  
USER root

RUN apt update  && apt install -y --no-install-recommends \
    python3-pip \
    python3-setuptools \
    python3-dev \
    python3-wheel \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

USER user

ENV PATH "$PATH:/home/user/.local/bin"

RUN pip3 install conan
