FROM debian:bullseye-20220125-slim

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y upgrade && \
apt-get -y install git nano build-essential flex bison zip unzip curl screen \
gnupg zlib1g-dev libncurses5 x11proto-core-dev libx11-dev libgl1-mesa-dev gperf \
libc6-dev libxml2-utils xsltproc fontconfig openjdk-17-jdk libncurses6 procps \
gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev lib32z1-dev ccache \
gnupg rsync lib32z1-dev python3 && ln -sf /usr/bin/python3 /usr/bin/python \
&& adduser --system --group --uid 1000 aosp

# see https://source.android.com/setup/develop#installing-repo
ARG REPO=/bin/repo
RUN curl -o ${REPO} https://storage.googleapis.com/git-repo-downloads/repo \
&& gpg --recv-key 8BB9AD793E8E6153AF0F9A4416530D5E920F5C65 \
&& curl -s https://storage.googleapis.com/git-repo-downloads/repo.asc | gpg --verify - ${REPO} \
&& chmod a+x ${REPO}

VOLUME /aosp
VOLUME /ccache

#overwrite ~/.gitignore with your file using file mounts
RUN git config --global user.name "Your Name" \
&& git config --global user.email "you@example.com"

WORKDIR /aosp

USER aosp

#aliases
RUN echo "alias lstat=\"stat -L\"" >> ~/.bashrc

#enable ccache
RUN echo "export USE_CCACHE=1" >> ~/.bashrc \
&& echo "export CCACHE_EXEC=/usr/bin/ccache" >> ~/.bashrc \
&& echo "export CCACHE_DIR=/ccache" >> ~/.bashrc \
&& echo "ccache -M 50G > /dev/null" >> ~/.bashrc

# we want to run that container forever until we shut it down manually
# TODO find a better way
ENTRYPOINT ["tail", "-f", "/dev/null"]