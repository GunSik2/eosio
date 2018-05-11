## Install virtualbox
- install virtualbox for windows, not for ubuntu

## Install vagrant
- install latest vagrant deb file from the following site:
- https://www.vagrantup.com/downloads.html
- run
```
sudo dpkg -i /mnt/c/Users/USER/Downloads/vagrant_2.1.1_x86_64.deb

export PATH="$PATH:/mnt/c/Program\ Files/Oracle/VirtualBox:/mnt/c/Windows/SysWOW64/cmd.exe"

export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"

export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/Vagrant/"
```

## Run vagrant ubuntu
```
mkdir ubuntu-16.04; cd ubuntu-16.04;

cat Vagrantfile
---
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "public_network"
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 4
    v.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end
end

# run
vagrant up --provider virtualbox
 
# ssh
vagrant ssh
```

# Reference
- https://www.vagrantup.com/docs/other/wsl.html
- https://github.com/joelhandwell/ubuntu_vagrant_boxes/issues/1
