FROM debian:buster-slim

ARG QT_VERSION=5.15.2
ENV DEBIAN_FRONTEND=noninteractive \
    QT_PATH=/opt/Qt \
    QT_BIN_PACKAGE=gcc_64
ENV QT_DESKTOP ${QT_PATH}/${QT_VERSION}/${QT_BIN_PACKAGE}
#ENV PATH ${QT_DESKTOP}/bin:${QT_PATH}/Tools/CMake/bin:${QT_PATH}/Tools/Ninja:$PATH

RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list

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
    clang-11/buster-backports \
    cmake/buster-backports \
    python \
    perl \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

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

RUN cd qt5 && sudo make install

ENV PATH ${QT_PATH}/bin:$PATH

RUN rm -rf qt5
