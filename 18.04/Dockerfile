FROM ubuntu:18.04

WORKDIR /root
ENV LC_CTYPE C.UTF-8
ENV TERM xterm-256color
ARG DEBIAN_FRONTEND=noninteractive

# Install
RUN dpkg --add-architecture i386
RUN apt update -y
RUN apt install file sudo python python-dev python-setuptools python3 python3-pip python3-dev python3-setuptools python-capstone libssl-dev libffi-dev build-essential libc6-dbg gcc-multilib make gcc netcat git curl wget gdb vim nano zsh ruby-full -y
RUN wget https://bootstrap.pypa.io/pip/2.7/get-pip.py && python get-pip.py && rm -rf get-pip.py
RUN python -m pip install --upgrade pip && python3 -m pip install --upgrade pip
RUN python -m pip install --ignore-installed pwntools && python3 -m pip install --ignore-installed pwntools && python3 -m pip install keystone-engine ropper && python -m pip install pathlib2
RUN gem install one_gadget seccomp-tools

# Install old version gef (avoid to error)
WORKDIR /root
RUN git clone https://github.com/hugsy/gef.git
WORKDIR /root/gef
RUN git checkout tags/2022.01
RUN cp ./gef.py .gdbinit-gef.py
RUN echo source ~/.gdbinit-gef.py >> ~/.gdbinit

# Install old version pwndbg (avoid to error)
WORKDIR /root
RUN git clone https://github.com/pwndbg/pwndbg.git
WORKDIR /root/pwndbg
RUN git checkout tags/ubuntu18.04-final
RUN ./setup.sh

# Install gdb-peda-pwndbg-gef
WORKDIR /root/.docker_set
RUN git clone https://github.com/is07king/gdb-peda-pwndbg-gef.git
WORKDIR /root/.docker_set/gdb-peda-pwndbg-gef
RUN ./install.sh

# Finish Setting
WORKDIR /root/.docker_set
RUN git clone https://github.com/is07king/pwn_docker_setting.git
WORKDIR /root/.docker_set/pwn_docker_setting/ubuntu
RUN ./zsh-plugin.sh

# Finally fixed the last error(GEF)
RUN python3 -m pip install unicorn==1.0.3 

# Clean junk
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Finish
RUN chsh -s /bin/zsh
WORKDIR /root
RUN mkdir pwn
WORKDIR /root/pwn