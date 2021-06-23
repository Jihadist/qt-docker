FROM multiarch/debian-debootstrap:armhf-buster

ARG QT_VERSION=5.15.2
ENV DEBIAN_FRONTEND=noninteractive \
    QT_PATH=/opt/Qt \
    QT_BIN_PACKAGE=gcc_armhf
ENV QT_DESKTOP ${QT_PATH}/${QT_VERSION}/${QT_BIN_PACKAGE}
#ENV PATH ${QT_DESKTOP}/bin:${QT_PATH}/Tools/CMake/bin:${QT_PATH}/Tools/Ninja:$PATH

RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list
#ENV PATH ${QT_DESKTOP}/bin:${QT_PATH}/Tools/CMake/bin:${QT_PATH}/Tools/Ninja:$PATH

#RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list

# Install updates & requirements:
#  * git, openssh-client, ca-certificates - clone & build
#  * locales, sudo - useful to set utf-8 locale & sudo usage
#  * curl - to download Qt bundle
#  * build-essential, pkg-config, libgl1-mesa-dev - basic Qt build requirements
#  * libsm6, libice6, libxext6, libxrender1, libfontconfig1, libdbus-1-3 - dependencies of the Qt bundle run-file
RUN apt update && apt full-upgrade -y && apt install -y --no-install-recommends \
    git \
    openssh-client \
    ca-certificates \
    locales \
    sudo \
    curl \
    build-essential \
    pkg-config \
    libgl1-mesa-dev \
    libsm6 \
    libice6 \
    libxext6 \
    libxrender1 \
    libxkbcommon-x11-0 \
    libfontconfig1 \
    libdbus-1-3 \
    python3 \
    perl \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

RUN apt update && apt-get -t buster-backports install -y --no-install-recommends \
    clang-11 \
#    cmake \
# cmake-3.16.3 isn't appropriate for cross-compiling with qemu
    ninja-build \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*
    
#RUN dpkg --add-architecture armhf && apt update && \
#    apt install libc:armhf \
#    binutils:armhf


# Reconfigure locale
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales


# Add group & user + sudo
RUN groupadd -r user && useradd --create-home --gid user user && echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

USER user
WORKDIR /home/user
ENV HOME /home/user

RUN git clone https://code.qt.io/qt/qt5.git -b ${QT_VERSION}

RUN cd qt5 && perl init-repository --module-subset=qtbase,qtserialport

RUN cd qt5 && ./configure -developer-build \
	-opensource \ 
	-no-widgets \
	-no-gui \
	-nomake examples \ 
	-nomake tests \
	-confirm-license \ 
	-c++std c++17 \
	-static \
	-prefix ${QT_PATH} \ 
	-release \
	-recheck-all

RUN cd qt5 && make -j 8

USER root

RUN mkdir -p ${QT_PATH}

RUN chown user ${QT_PATH}

USER user

WORKDIR /home/user

RUN cd qt5 && make install

ENV PATH ${QT_SYSROOT}/${QT_PATH}/bin:$PATH

RUN rm -rf qt5
