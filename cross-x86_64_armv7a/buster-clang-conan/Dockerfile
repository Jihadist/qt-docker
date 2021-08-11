FROM atom63/qt-docker:linux-buster-cross-x86_64-armv7a-clang

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
   
COPY --chown=user:user ./profiles/armhf ./.conan/profiles/

RUN cp ./.conan/profiles/armhf ./.conan/profiles/default 

RUN conan install zlib/1.2.11@ --build=missing

RUN conan install zlib/1.2.11@ --profile armhf --build=missing

