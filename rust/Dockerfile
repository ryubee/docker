FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive

RUN \
  apt-get update \
  && apt-get upgrade -y \
  && apt-get -y --no-install-recommends install \
    ca-certificates vim curl git make apt-utils bash sudo build-essential xorg dbus dbus-x11 gtk2-engines \
    libreadline-dev libsqlite3-dev wget llvm libncurses5-dev libncursesw5-dev \
    make build-essential libssl-dev zlib1g-dev libbz2-dev \
    xz-utils tk-dev libffi-dev liblzma-dev python-openssl git \
    zlib1g zlib1g-dev gzip ssh-client screenfetch \
    libedit-dev \
    python3-pip \
    locales \
  && rm -rf /var/lib/apt/lists/* \
  && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN locale-gen ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

# install rust
#ENV RUST_VERSION stable
ENV RUST_VERSION nightly
ENV CARGO_HOME /usr/local
ENV RUSTUP_HOME /usr/local
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain ${RUST_VERSION}
ENV PATH $PATH:${HOME}/.cargo/bin
RUN rustup update
#RUN cargo install --git 'https://github.com/phildawes/racer.git'
#RUN cargo install racer
#RUN rustup component add rust-src
RUN rustup component add rust-src --toolchain $RUST_VERSION
RUN rustup component add rls-preview --toolchain $RUST_VERSION
RUN rustup component add rust-analysis --toolchain $RUST_VERSION
ENV RUST_SRC_PATH /usr/local/toolchains/nightly-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/src


# install neovim
RUN curl -sSLO https://github.com/neovim/neovim/releases/download/nightly/nvim-linux64.tar.gz
RUN tar zxf nvim-linux64.tar.gz
RUN mv nvim-linux64/bin/nvim /usr/local/bin
RUN cp -r nvim-linux64/share /usr/local


# install python
ENV PYENV_ROOT /opt/pyenv
RUN git clone https://github.com/pyenv/pyenv.git ${PYENV_ROOT}
ENV PATH ${PYENV_ROOT}/bin:${PATH}
RUN echo 'export PYENV_ROOT="/opt/pyenv"' >> /etc/profile \
 && echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> /etc/profile \
 && echo 'eval "$(pyenv init -)"' >> /etc/profile
            
RUN pyenv install 3.7.3
RUN pyenv global 3.7.3
RUN chmod -R 777 /opt/pyenv

RUN ["/bin/bash", "-c", " \
        source /etc/profile \
        &&  python3 -m pip install setuptools \
        &&  python3 -m pip install wheel \
        &&  python3 -m pip install pynvim \
    "]


CMD ["/bin/bash"]
