FROM python:3.7.2-stretch

ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get update \
  && apt-get upgrade -y \
  && apt-get -y --no-install-recommends install \
    ca-certificates curl apt-utils bash sudo build-essential xorg dbus dbus-x11 gtk2-engines \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN python -m pip install pipenv

CMD ["/bin/bash"]
