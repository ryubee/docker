FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get update \
  && apt-get upgrade -y \
  && apt-get -y --no-install-recommends install \
    ca-certificates \
    apt-utils  \
    software-properties-common \
    curl \
    sudo \
    bash \
    vim \
    neovim \
    git \
    make \
    build-essential \
    autoconf \
    automake \
    gnat \
    zlib1g-dev \
    gtkwave \
    iverilog \
    xorg \
    dbus \
    dbus-x11 \
    gtk2-engines \
    screenfetch \
    ssh-client \
    autoconf \
    automake \
    autotools-dev \
    libmpc-dev \
    libmpfr-dev \
    libgmp-dev \
    libusb-1.0-0-dev \
    gawk \
    build-essential \
    bison \
    flex \
    texinfo \
    gperf \
    libtool \
    patchutils \
    bc \
    zlib1g-dev \
    device-tree-compiler \
    pkg-config \
    libexpat-dev \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR /tmp
RUN curl -O https://cmake.org/files/v3.14/cmake-3.14.0.tar.gz
RUN tar zxvf cmake-3.14.0.tar.gz \
    && cd cmake-3.14.0 && ./bootstrap && make -j$(nproc) && make install

WORKDIR /tmp
RUN git clone https://github.com/ghdl/ghdl.git 
WORKDIR /tmp/ghdl
## check 20190410
RUN git checkout -b build 88830edd0ac769f04e18e2a0d6fe0d5e23cf203f
RUN ./configure --prefix=/usr/local && make -j$(nproc) && make install

ENV RISCV /opt/riscv
ENV PATH /opt/riscv/bin:${PATH}

WORKDIR /tmp
RUN git clone https://github.com/riscv/riscv-gnu-toolchain.git
WORKDIR /tmp/riscv-gnu-toolchain
## check 20190410
RUN git checkout -b build afcc8bc655d30cf6af054ac1d3f5f89d0627aa79
RUN git submodule update --init --recursive
RUN mkdir build_newlib \
    && cd build_newlib \
    && ../configure --prefix=/opt/riscv \
    && make -j$(nproc) \
    && make install
RUN mkdir build_riscv64_linux \
    && cd build_riscv64_linux \
    && ../configure --prefix=/opt/riscv \
    && make linux -j$(nproc) \
    && make install
RUN mkdir build_riscv32_linux \
    && cd build_riscv32_linux \
    && ../configure --prefix=/opt/riscv --with-arch=rv32gc --with-abi=ilp32d \
    && make linux -j$(nproc) \
    && make install

WORKDIR /tmp
RUN git clone https://github.com/riscv/riscv-tools.git
WORKDIR /tmp/riscv-tools
## check 20190410
RUN git checkout -b build 26190623292f82a0f001bdcba40cfa98786e8819
RUN git submodule update --init --recursive
RUN ./build.sh
WORKDIR /

CMD ["/bin/bash"]
