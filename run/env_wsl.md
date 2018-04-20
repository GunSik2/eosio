# Using WSL(Windows Subsystem for Linux)

## Install the Windows Subsystem for Linux
- Open PowerShell as Administrator and run:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
- Restart your computer when prompted.

## Install your Linux Distribution
- Open the Microsoft Store and choose your favorite Linux distribution: ubuntu


## Run OpenSSH Server
- Install Full OpenSSH Server
```
sudo apt-get remove  openssh-server
sudo apt-get install  openssh-server
```
- /etc/ssh/sshd_config
```
Port 2200
ListenAddress 0.0.0.0
PasswordAuthentication yes
```
- Restart
```
sudo service ssh restart 
```
