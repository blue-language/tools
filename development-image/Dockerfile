FROM ubuntu:18.04

ENV TERM xterm-256color
ENV HOME /home/developer

RUN set -ex \
  && ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
  && echo ${TIMEZONE} > /etc/timezone

RUN set -ex \
  && apt-get update \
  && apt-get dist-upgrade -y \
  && apt-get install -y \
    curl \
    git \
    sudo \
    zsh \
    nano \
    ocaml

RUN set -ex \
  && mkdir ${HOME}

RUN set -ex \
  && curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh

RUN set -ex \
  && chmod 666 /etc/passwd /etc/group

COPY /home ${HOME}/
COPY /docker-entrypoint.d /etc/docker-entrypoint.d/
COPY /sudoers.d /etc/sudoers.d/

RUN chmod 440 /etc/sudoers.d/*

ENTRYPOINT ["/home/developer/docker-entrypoint.sh"]