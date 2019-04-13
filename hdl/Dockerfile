FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get update \
  && apt-get upgrade -y \
  && apt-get -y --no-install-recommends install \
    ca-certificates apt-utils software-properties-common curl sudo bash vim \
    git \
    make \
    build-essential \
    autoconf \
    automake \
    gnat \
    zlib1g-dev \
    gtkwave \
    iverilog \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR /tmp
RUN curl -O https://cmake.org/files/v3.14/cmake-3.14.0.tar.gz
RUN tar zxvf cmake-3.14.0.tar.gz \
    && cd cmake-3.14.0 && ./bootstrap && make -j$(nproc) && make install

WORKDIR /tmp
RUN git clone https://github.com/ghdl/ghdl.git \
    && cd ghdl \
    && ./configure --prefix=/usr/local \
    && make -j$(nproc) && make install

CMD ["/bin/bash"]
