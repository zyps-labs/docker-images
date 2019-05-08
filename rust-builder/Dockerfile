FROM zyps/base-build:latest

ENV RUST_VERSION 1.34.1

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain $RUST_VERSION \
# Init cargo packages index for faster builds
  && . ~/.profile \
  && cargo search serde \
  && apt-get update \
  && apt-get install -y --no-install-recommends capnproto \
# Clean
  && rm -rf /var/lib/apt/lists/*
