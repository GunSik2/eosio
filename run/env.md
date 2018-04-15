
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
```
docker run --name nodeos -p 8888:8888 -p 9876:9876 -t eosio/eos start_nodeos.sh arg1 arg2
```

## Get chain info
```
curl http://127.0.0.1:8888/v1/chain/get_info
```

## Reference
- https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-after-using-the-convenience-script
- https://github.com/EOSIO/eos/wiki/Local-Environment#3-docker
