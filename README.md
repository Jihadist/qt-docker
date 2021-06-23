# qt-docker

Repository with multiple docker recipes for C++ and mainly Qt projects linked against old standard library.

Main feature of this recipes is modern compilers, build systems and 3rd-party libs.

I looked here https://github.com/dockcross/dockcross but it uses ancient compilers
So here you can receive:
- clang-11 - debian-backports
- cmake-latest (3.21.0-rc1 - 23.06.2021) - built from sources
- qt-5.15.2 - build from sources, kde-patches can be easily integrated  if it needs
- other tools are the same as debian:buster repository

Plans:
- Integrate conan


Debian buster x64 qt-static
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-x64.yml/badge.svg?branch=master)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-x64.yml)

Debian buster x64 qt-static-crosscompiled-armhf
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-armv7a.yml/badge.svg?branch=master)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-armv7a.yml)

Debian buster armhf qt-static - qemu
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-armv7a-qemu.yml/badge.svg?branch=master)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-armv7a-qemu.yml)

Debian buster armhf qt-static cmake - qemu
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-armv7a-qemu-cmake.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-armv7a-qemu-cmake.yml)
