
# Local env with docker

## Ubuntu 16.04 (virutal box)

## Install docker
```
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

## Build EOSIO image
```
git clone https://github.com/EOSIO/eos.git --recursive
cd eos/Docker
sudo docker build . -t eosio/eos
```

## Start nodeos docker container only

## Reference
- https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-after-using-the-convenience-script
- https://github.com/EOSIO/eos/wiki/Local-Environment#3-docker
