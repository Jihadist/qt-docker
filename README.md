# qt-docker

Repository with multiple docker recipes for C++ and mainly Qt projects linked against old standard library.

Main feature of this recipes is modern compilers, build systems and 3rd-party libs.

I looked here https://github.com/dockcross/dockcross but it uses ancient compilers
So here you can receive:
- clang-11 - debian-backports
- cmake-latest (3.21.0-rc1 - 23.06.2021) - built from sources
- qt-5.15.2 - build from sources, kde-patches can be easily integrated  if it needs
- other tools are the same as debian:buster repository
- conan


Debian buster x86_64 with qt5-static
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-x86_64-qt5-static.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-x86_64-qt5-static.yml)

Debian buster x86_64 with cmake from scratch
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-x86_64.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-x86_64.yml)

Debian buster x86_64 with cmake from scratch, qt5 from buster upstream
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-x86_64-qt5.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-x86_64-qt5.yml)

Debian buster x86_64 cross armv7a(armhf) with qt5-static
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-cross-buster-x86_64-armv7a-qt-static.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-cross-buster-x86_64-armv7a-qt-static.yml)

Debian buster armhf with qt5-static
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-armv7a-qt5-static.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-armv7a-qt5-static.yml)

Debian buster armhf with qt5-static, cmake from scratch
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-armv7a-qt5-static-cmake.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-armv7a-qt5-static-cmake.yml)

Debian buster armhf with qt5-static, cmake from scratch, conan
[![Docker Image CI](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-armv7a-qt5-static-cmake-conan.yml/badge.svg)](https://github.com/Jihadist/qt-docker/actions/workflows/docker-image-buster-armv7a-qt5-static-cmake-conan.yml)
