FROM ubuntu:22.04

# Avoid interactive prompts while installing `tzdata` dependency with `DEBIAN_FRONTEND`.
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends \
  g++ \
  make \
  ninja-build \
  file \
  curl \
  ca-certificates \
  python3 \
  git \
  cmake \
  sudo \
  gdb \
  libssl-dev \
  pkg-config \
  xz-utils \
  && rm -rf /var/lib/apt/lists/*

COPY scripts/sccache.sh /scripts/
RUN sh /scripts/sccache.sh

ENV RUST_CONFIGURE_ARGS --build=x86_64-unknown-linux-gnu \
  --disable-optimize-tests \
  --set rust.test-compare-mode
ENV SCRIPT python3 ../x.py test --stage 1 --set rust.optimize=false library/std \
  && python3 ../x.py --stage 2 test
