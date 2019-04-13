FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get update \
  && apt-get upgrade -y \
  && apt-get -y --no-install-recommends install \
    ca-certificates vim neovim curl git make apt-utils bash sudo build-essential xorg dbus dbus-x11 gtk2-engines \
    ssh-client screenfetch \
    python3-pip \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN python3 -m pip install setuptools
RUN python3 -m pip install neovim

ENV RUST_VERSION stable
ENV CARGO_HOME /usr/local
ENV RUSTUP_HOME /usr/local
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain ${RUST_VERSION}

ENV PATH $PATH:${HOME}/.cargo/bin

RUN rustup update
RUN rustup component add rls-preview --toolchain stable
RUN rustup component add rust-analysis --toolchain stable
RUN rustup component add rust-src --toolchain stable

#RUN cargo install --git 'https://github.com/phildawes/racer.git'
RUN rustup component add rust-src

ENV RUST_SRC_PATH '$(echo /usr/local/toolchains/*/lib/rustlib/src/rust/src)'

CMD ["/bin/bash"]
