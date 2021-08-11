FROM atom63/qt-docker:linux-buster-x86_64

USER root

RUN dpkg --add-architecture armhf && apt update 

RUN apt install -y build-essential \
    pkg-config \
    binutils:amd64 \
    gcc-8-arm-linux-gnueabihf \
    cross-config \
    dpkg-cross
    
RUN apt install -y libstdc++-8-dev:armhf \
    crossbuild-essential-armhf \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

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
   
COPY --chown=user:user ./profiles/armhf ./.conan/profiles/

RUN cp ./.conan/profiles/armhf ./.conan/profiles/default 

RUN conan install zlib/1.2.11@ --build=missing

RUN conan install zlib/1.2.11@ --profile armhf --build=missing
