# CLion + WSL

## Prerequistes
- [CLione for Linux](https://www.jetbrains.com/clion/download/download-thanks.html?platform=linux)
- WSL & Ubuntu

## Install on WSL Ubuntu
- Download: install cmake, gcc, or/and clang, openssh
```
$ wget https://raw.githubusercontent.com/JetBrains/clion-wsl/master/ubuntu_setup_env.sh && bash ubuntu_setup_env.sh
```
- SSH 설정
```
# SSH server parameters (/etc/ssh/sshd_config):
Port 2222
UsePrivilegeSeparation no
PasswordAuthentication yes
```
- X 환경 설정
```
$ export DISPLAY=0:0
```
- X Server 설치 (VcXsrv)

- CLion 설치
```
$ tar xvzf CLion-2018.1.2.tar.gz; cd clion-2018.1.2/bin; 
$ ./clion.sh
```

## Reference
- [JetBrains CLion on WSL](https://blog.jetbrains.com/clion/2018/01/clion-and-linux-toolchain-on-windows-are-now-friends/)
