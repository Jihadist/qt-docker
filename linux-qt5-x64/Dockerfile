FROM atom63/qt-docker:linux-cmake-x64

ENV DEBIAN_FRONTEND=noninteractive 

#ENV PATH ${QT_DESKTOP}/bin:${QT_PATH}/Tools/CMake/bin:${QT_PATH}/Tools/Ninja:$PATH

#RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list

USER root

RUN apt update && apt full-upgrade -y && apt install -y \
    qt5-default \
    qttools5-dev \
    qtdeclarative5-dev \
    qtbase5-dev \
    libqt5widgets5 \
    libqt5x11extras5-dev \
    libqt5svg5-dev \
    libqt5serialport5-dev \
    qtbase5-private-dev \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*


RUN apt update  && apt install -y --no-install-recommends \
    python3-pip \
    python3-setuptools \
    python3-dev \
    python3-wheel \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

USER root

RUN apt update  && apt install -y --no-install-recommends \
    libudev-dev \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

RUN apt update  && apt install -y --no-install-recommends \
    libhidapi-dev \
    file \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

RUN apt update && apt full-upgrade -y && apt install -y --no-install-recommends \
    ninja-build/buster-backports \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/* 

USER user

ENV PATH "$PATH:/home/user/.local/bin"

RUN pip3 install conan

RUN conan profile new default --detect
RUN conan profile update settings.compiler.libcxx=libstdc++11 default
# We have clang-11
RUN conan profile update settings.compiler=clang default
RUN conan profile update settings.compiler.version=11 default    
    

