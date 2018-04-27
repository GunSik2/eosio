# Local Dev. Env using WSL(Windows Subsystem for Linux) 

## Introduction
- Dev environment
  - Windows 10
  - WSL(Windows Subsystem for Linux) 
  - vscode (Visual Studio Code)
  - firefox
  - term
  
## Install the Windows Subsystem for Linux
- Open PowerShell as Administrator and run:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
- Restart your computer when prompted.

## Install your Linux Distribution
- Open the Microsoft Store and choose your favorite Linux distribution: ubuntu

## (Optional) Run OpenSSH Server
- Run bash to launch a new Ubuntu shell and inside it run update & upgrade:
```
sudo apt update
sudo apt full-upgrade
```

- Install Full OpenSSH Server
```
sudo apt-get remove -y openssh-server
sudo apt-get install -y openssh-server
```
- /etc/ssh/sshd_config
```
#Port 22
#ListenAddress 0.0.0.0
PasswordAuthentication yes
```
- Restart
```
sudo service ssh restart 
```
- Access to ssh server with terminal: [mobaXterm](https://mobaxterm.mobatek.net)
```
ssh username@localhost 
```
## (Optional) Reinstall ubuntu
- Open Windows command prompt and run:
```
lxrun /uninstall /full to uninstall
lxrun /install to reinstall
```

## VS Code
- Download & install: https://code.visualstudio.com/Download
- Enable Ubuntu bash console inside Visual Studio Code: File > Preferences > User Settings:
```
{
  "terminal.integrated.shell.windows":  "C:\\Windows\\sysnative\\bash.exe"
}
```
- Open ubuntu console: Ctrl + ' or View > Integrated Terminal

## Untility
```
sudo apt -y install firefox nautilus gnome-terminal
```

## Reference
- https://github.com/EOSIO/eos/wiki/Local-Environment
- https://steemit.com/eos/@tokenika/installing-and-running-eos-on-windows
- https://medium.com/@rkttu/windows-10%EC%97%90%EC%84%9C-%EB%A6%AC%EB%88%85%EC%8A%A4%EC%9A%A9-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%84%A4%EC%B9%98%ED%95%98%EA%B3%A0-%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0-2cb0d7892d12
