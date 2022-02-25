# Dockerfile for AOSP12+

This repository holds a Dockerfile to provide the needed toolchain for building AOSP12

## Install Docker CE and Compose
1. Install Docker CE and Docker-Compose on your host machine (recommended: Debian, 30GB+, 8 Cores, 250GB+ HDD)
2. see https://docs.docker.com/engine/install/debian/ and https://docs.docker.com/compose/install/

## Run
1. checkout repo and change ```config/gitconfig``` file using your full name and email
3. ```docker-compose up -d --build```
4. ```docker exec -it aosp_builder bash```

## Download AOSP source
This follows the normal AOSP approach, e.g.
1. ```repo init --depth=1 -u https://android.googlesource.com/platform/manifest -b android12-qpr1-release```
2. ```repo sync -c --no-tags --no-clone-bundle -j$(nproc --all)```

## Build AOSP
This follows the normal AOSP approach, e.g.
1. ```source build/envsetup.sh```
2. ```lunch aosp_car_arm64```
3. ```m -j$(nproc --all)```
