# Build Container for AOSP13+ (Docker)

![GitHub release (latest by date)](https://img.shields.io/github/v/release/alexanderwolz/aosp-docker)
![GitHub](https://img.shields.io/badge/aosp-14-orange)
![GitHub](https://img.shields.io/badge/docker-23.0.1-orange)
![GitHub](https://img.shields.io/badge/docker_compose-1.29.2-orange)
![GitHub](https://img.shields.io/github/license/alexanderwolz/aosp-docker)
![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/alexanderwolz/aosp-docker)
![GitHub all releases](https://img.shields.io/github/downloads/alexanderwolz/aosp-docker/total?color=informational)

## About

This repository holds a Dockerfile to provide the needed toolchain for building AOSP14+

## Install Docker CE and Compose
1. Install Docker CE and Docker-Compose on your host machine (recommended: Debian, 30GB+, 8 Cores, 250GB+ HDD)
2. see https://docs.docker.com/engine/install/debian/ and https://docs.docker.com/compose/install/

## Run
1. checkout repo and change ```config/gitconfig``` file using your full name and email
3. ```docker-compose up -d --build```
4. ```docker exec -it aosp_builder bash```

## Download AOSP source
This follows the normal AOSP approach, e.g.
1. ```repo init --depth=1 -u https://android.googlesource.com/platform/manifest -b android-14.0.0_r14```
2. ```repo sync -c --no-tags --no-clone-bundle -j$(nproc --all)```

## Build AOSP
This follows the normal AOSP approach, e.g.
1. ```source build/envsetup.sh```
2. ```lunch aosp_car_arm64```
3. ```m -j$(nproc --all)```
