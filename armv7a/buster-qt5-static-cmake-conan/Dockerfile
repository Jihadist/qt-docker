FROM atom63/qt-docker:linux-buster-armv7a-qt5-static-cmake
  
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

RUN conan profile new default --detect
RUN conan profile update settings.compiler.libcxx=libstdc++11 default
# We have clang-11
RUN conan profile update settings.compiler=clang default
RUN conan profile update settings.compiler.version=11 default

USER root

#RUN ln -s /usr/bin/clang++-11 /usr/bin/clang++

#RUN ln -s /usr/bin/clang-11 /usr/bin/clang

RUN apt update  && apt install -y --no-install-recommends \
    libudev-dev \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

#ENV CC=/usr/bin/clang

#ENV CXX=/usr/bin/clang++

USER user

RUN conan install hidapi/0.10.1@ --build=missing

RUN conan install cppzmq/4.7.1@ --build=missing

RUN conan install protobuf/3.17.1@ --build=missing

USER root

RUN apt update  && apt install -y --no-install-recommends \
    libhidapi-dev \
    file \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

USER user

