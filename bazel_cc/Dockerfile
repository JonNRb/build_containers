from ubuntu:rolling

env BAZEL_VERSION 3.3.0
env SRC_URL https://github.com/bazelbuild/bazel/releases/download/$BAZEL_VERSION/bazel_$BAZEL_VERSION-linux-x86_64.deb
env SRC_HASH aebed9ba87b0e4b56e3ae6baeece004a31774ee402182ad4e9f70715345d5f56

add $SRC_URL bazel.deb

env DEBIAN_FRONTEND noninteractive
run echo "$SRC_HASH  bazel.deb" |sha256sum -c - \
 && apt-get update \
 && apt-get install -y vim gdb gcc gcc-7 g++ g++-7 git wget openjdk-8-jdk \
      zlib1g-dev bash-completion unzip python \
 && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 60 \
 && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 60 \
 && dpkg -i bazel.deb \
 && bazel \
 && mkdir /output /src \
 && echo "#!/bin/sh" > /usr/bin/dbazel \
 && echo "exec bazel --batch --output_base=/output \$@" >> /usr/bin/dbazel \
 && chmod +x /usr/bin/dbazel

workdir /src
