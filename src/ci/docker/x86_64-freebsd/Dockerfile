FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
  g++ \
  make \
  file \
  curl \
  ca-certificates \
  python2.7 \
  git \
  cmake \
  ccache \
  sudo \
  bzip2 \
  xz-utils \
  wget

COPY build-toolchain.sh /tmp/
RUN sh /tmp/build-toolchain.sh

RUN curl -OL https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb && \
    dpkg -i dumb-init_*.deb && \
    rm dumb-init_*.deb
ENTRYPOINT ["/usr/bin/dumb-init", "--"]

ENV SCCACHE_DIGEST=7237e38e029342fa27b7ac25412cb9d52554008b12389727320bd533fd7f05b6a96d55485f305caf95e5c8f5f97c3313e10012ccad3e752aba2518f3522ba783
RUN curl -L https://api.pub.build.mozilla.org/tooltool/sha512/$SCCACHE_DIGEST | \
      tar xJf - -C /usr/local/bin --strip-components=1

ENV \
    AR_x86_64_unknown_freebsd=x86_64-unknown-freebsd10-ar \
    CC_x86_64_unknown_freebsd=x86_64-unknown-freebsd10-gcc

ENV RUST_CONFIGURE_ARGS --target=x86_64-unknown-freebsd
ENV RUST_CHECK_TARGET ""
RUN mkdir /tmp/obj
RUN chmod 777 /tmp/obj
