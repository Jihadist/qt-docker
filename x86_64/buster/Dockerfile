FROM debian:buster-slim


ENV DEBIAN_FRONTEND=noninteractive

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

RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list

RUN apt update && apt full-upgrade -y && apt install -y --no-install-recommends \
    clang-11/buster-backports \
    ninja-build/buster-backports
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*    

RUN apt update  && apt install -y --no-install-recommends \
    libssl-dev \
    libffi-dev \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/clang++-11 /usr/bin/clang++

RUN ln -s /usr/bin/clang-11 /usr/bin/clang

ENV CC=/usr/bin/clang

ENV CXX=/usr/bin/clang++

WORKDIR /tmp

RUN git clone https://github.com/Kitware/CMake.git -b release

WORKDIR /tmp/CMake

RUN ./bootstrap
    
RUN make

RUN make install

WORKDIR /tmp

RUN rm -rf CMake

# Reconfigure locale
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Add group & user + sudo
RUN groupadd -r user && useradd --create-home --gid user user && echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

USER user
WORKDIR /home/user
ENV HOME /home/user

ENV CC=/usr/bin/clang

ENV CXX=/usr/bin/clang++
