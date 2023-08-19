FROM ubuntu:20.04

WORKDIR /root
ENV LC_CTYPE C.UTF-8
ENV TERM xterm-256color
ARG DEBIAN_FRONTEND=noninteractive

# Install
RUN dpkg --add-architecture i386
RUN apt update -y
RUN apt install python python-dev python-setuptools python3 python3-pip python3-dev python3-setuptools python-capstone libssl-dev libffi-dev build-essential libc6-i386 libc6-dbg gcc-multilib make gcc netcat git curl wget gdb vim nano zsh ruby-full libtool -y
RUN curl -O https://bootstrap.pypa.io/pip/2.7/get-pip.py && python get-pip.py && rm get-pip.py
RUN python -m pip install --upgrade pip && python3 -m pip install --upgrade pip
RUN python -m pip install --ignore-installed pwntools && python3 -m pip install --ignore-installed pwntools && python3 -m pip install z3-solver
RUN gem install one_gadget seccomp-tools

# Install gdb-peda-pwndbg-gef
WORKDIR /root/.docker_set
RUN git clone https://github.com/is07king/gdb-peda-pwndbg-gef.git
WORKDIR /root/.docker_set/gdb-peda-pwndbg-gef
RUN ./install.sh

# Install patchelf
WORKDIR /root/.docker_set
RUN git clone https://github.com/NixOS/patchelf.git
WORKDIR /root/.docker_set/patchelf
RUN ./bootstrap.sh
RUN ./configure
RUN make
RUN make check
RUN make install

# Finish Setting
WORKDIR /root/.docker_set
RUN git clone https://github.com/is07king/pwn_docker_setting.git
WORKDIR /root/.docker_set/pwn_docker_setting/ubuntu
RUN ./zsh-plugin.sh

# Clean junk
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Finish
RUN chsh -s /bin/zsh
WORKDIR /root
RUN mkdir pwn
WORKDIR /root/pwn
