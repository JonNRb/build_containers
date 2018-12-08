from ubuntu:rolling

# install deps
run apt-get update \
 && apt-get install -y vim gdb gcc gcc-7 g++ g++-7 git wget openjdk-8-jdk \
      zlib1g-dev bash-completion unzip python \
 && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 60 \
 && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 60

run wget -q https://github.com/bazelbuild/bazel/releases/download/0.20.0/bazel_0.20.0-linux-x86_64.deb \
 && wget -q https://github.com/bazelbuild/bazel/releases/download/0.20.0/bazel_0.20.0-linux-x86_64.deb.sha256 \
 && sha256sum -c bazel_0.20.0-linux-x86_64.deb.sha256 \
 && dpkg -i bazel_0.20.0-linux-x86_64.deb

# extract the bazel install
run bazel

run mkdir /output \
 && mkdir /src
workdir /src
run echo "#!/bin/sh" > /usr/bin/dbazel \
 && echo "exec bazel --batch --output_base=/output \$@" >> /usr/bin/dbazel \
 && chmod +x /usr/bin/dbazel
