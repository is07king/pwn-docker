# pwn-docker
Latest pwn-docker with high compatibility

## Ubuntu
- 16.04
- 18.04
- 20.04
- 22.04

## Settings
- [gdb-peda-pwndbg-gef](https://github.com/is07king/gdb-peda-pwndbg-gef)
  - gdb-peda
  - gdb-peda-intel
  - gdb-peda-arm
  - gdb-pwndbg
  - gdb-gef
- zsh(powerlevel10k theme, required [font](https://github.com/romkatv/powerlevel10k#fonts))
- nvim

## How to use
### docker build image command

```sh
cd pwn-docker/16.04
docker build --tag pwn-docker:16.04 .

cd pwn-docker/18.04
docker build --tag pwn-docker:18.04 .

cd pwn-docker/20.04
docker build --tag pwn-docker:20.04 .

cd pwn-docker/22.04
docker build --tag pwn-docker:22.04 .
```

### docker run contianer command

```sh

docker run --rm -it -v $(pwd):/root/pwn --name ubuntu_16 pwn-docker:16.04 /bin/zsh

```


### docker alias in ~/.zshrc or ~/.bashrc
Change the somewhere variable value to the path you want
```sh
export somewhere="/path/to/somewhere"
alias pwn16="docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined --rm -it -v $somewhere:/root/pwn --name ubuntu_16 pwn-docker:16.04 /bin/zsh"
alias pwn18="docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined --rm -it -v $somewhere:/root/pwn --name ubuntu_18 pwn-docker:18.04 /bin/zsh"
alias pwn20="docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined --rm -it -v $somewhere:/root/pwn --name ubuntu_20 pwn-docker:20.04 /bin/zsh"
alias pwn22="docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined --rm -it -v $somewhere:/root/pwn --name ubuntu_22 pwn-docker:22.04 /bin/zsh"
```

## Reference
[pwn_docker_settings](https://github.com/h1ghl1kh7/tools)<br>
[gdb-peda-pwndbg-gef](https://github.com/apogiatzis/gdb-peda-pwndbg-gef)<br>
[pwn-docker](https://github.com/Kangwoosun/pwn-docker)
