FROM ubuntu:24.04
LABEL maintainer="woodycpp <3256928@qq.com>"

RUN apt update && apt install -y gcc g++ cmake gdb clang-format vim git unzip zip default-jdk wget libboost-all-dev psmisc lcov zlib1g-dev libcurl4-openssl-dev openjdk-8-jdk strace valgrind ccache distcc net-tools && apt clean && rm -rf /var/lib/apt/lists/*

ARG TARGETARCH

# install bazel
RUN if [ "$TARGETARCH" = "amd64" ]; then \
        mkdir -p /root/env/bazel && \
        wget https://github.com/bazelbuild/bazel/releases/download/6.3.0/bazel-6.3.0-installer-linux-x86_64.sh -O /root/env/bazel/bazel.sh && \
        chmod +x /root/env/bazel/bazel.sh && \
        /root/env/bazel/bazel.sh > /dev/null && \
        rm -rf /root/env && echo "$TARGETARCH" ; \
    elif [ "$TARGETARCH" = "arm64" ]; then \
        wget https://github.com/bazelbuild/bazel/releases/download/6.3.0/bazel-6.3.0-linux-arm64 -O /usr/local/bin/bazel && \
        chmod +x /usr/local/bin/bazel ; \
    else \
        echo "Arch: $TARGETARCH" ; \
    fi
