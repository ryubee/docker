FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get update \
  && apt-get upgrade -y \
  && apt-get -y --no-install-recommends install \
    ca-certificates ssh-client vim neovim curl apt-utils bash sudo build-essential \
    xorg dbus dbus-x11 gtk2-engines screenfetch \
    libffi-dev libgmp-dev zlib1g-dev git \
    g++ gcc libc6-dev libffi-dev libgmp-dev make xz-utils zlib1g-dev git gnupg netbase \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN curl -sSL https://get.haskellstack.org/ | sh

CMD ["/bin/bash"]
