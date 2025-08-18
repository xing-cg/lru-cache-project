FROM ubuntu:24.04
LABEL maintainer="woodycpp <3256928@qq.com>"

RUN apt update && apt install -y gcc g++ cmake gdb clang-format vim git unzip zip default-jdk wget libboost-all-dev psmisc lcov zlib1g-dev libcurl4-openssl-dev openjdk-8-jdk strace valgrind ccache distcc net-tools && apt clean && rm -rf /var/lib/apt/lists/*

#install bazel
RUN mkdir -p /root/env/bazel \
    && wget https://github.com/bazelbuild/bazel/releases/download/6.3.0/bazel-6.3.0-installer-linux-x86_64.sh -O /root/env/bazel/bazel.sh \
    && chmod +x /root/env/bazel/bazel.sh \
    && /root/env/bazel/bazel.sh > /dev/null \
    && rm -rf /root/env

ADD .clang-format /root/.clang-format
