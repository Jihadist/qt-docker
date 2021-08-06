FROM atom63/qt-docker:linux-qt5-armv7a-static
  
RUN git clone https://github.com/Kitware/CMake.git -b release

USER root

RUN apt update  && apt install -y --no-install-recommends \
    libssl-dev \
    libffi-dev \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

# Part of https://gitlab.kitware.com/cmake/cmake/-/issues/22328
# RUN cd CMake && \
#     mkdir Testing && \
#     cd Testing && \
#     mkdir JacocoCoverage && \
#     cd JacocoCoverage && \
#     mkdir Coverage
#       
#     
# RUN cp -r  /home/user/CMake/Tests/JacocoCoverage/Coverage/target /home/user/CMake/Testing/JacocoCoverage/Coverage/target

RUN cd ~/CMake && ./bootstrap
    
RUN cd ~/CMake && make

RUN cd ~/CMake && make install

RUN rm -rf CMake
