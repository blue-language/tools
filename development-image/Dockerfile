FROM ubuntu:18.04

ENV TERM xterm-256color
ENV HOME /home/developer

RUN set -ex \
  && apt-get update \
  && apt-get dist-upgrade -y \
  && apt-get install -y \
    curl \
    git \
    sudo \
    zsh \
    nano \
    cmake \
    g++-8 \
    wget \
    gnupg \
    zlib1g-dev

RUN mkdir ${HOME}

RUN curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh

RUN chmod 666 /etc/passwd /etc/group

COPY /home ${HOME}/
COPY /docker-entrypoint.d /etc/docker-entrypoint.d/
COPY /sudoers.d /etc/sudoers.d/
RUN chmod 440 /etc/sudoers.d/*

COPY /sources.list.d /etc/apt/sources.list.d

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -

RUN set -ex \
  && apt-get update \
  && apt-get install -y \
    libllvm8 \
    llvm-8 \
    llvm-8-dev \
    llvm-8-doc \
    llvm-8-examples \
    llvm-8-runtime \
    lldb-8 \
    lld-8 \
    libc++-8-dev \
    libc++abi-8-dev \
    libomp-8-dev

ENTRYPOINT ["/home/developer/docker-entrypoint.sh"]
