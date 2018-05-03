
## EOS Deployment on Ubuntu
- Getting the Code
```
git clone https://github.com/EOSIO/eos --recursive
```
- Get dawn-v3.0
```
cd eos
git checkout dawn-v3.0.0
git submodule update --recursive
```
- Building EOSIO
```
./eosio_build.sh
```
- (Optional) Error resolve
```
Error when building dawn 3.0 "unable to find the requested Boost libraries. eosio."

I fixed the issue by editing eos/scripts/eosio_build_ubuntu.sh line 113.
old: tar xf boost.1.66.0.tar.bz2
new: tar xf boost_1_66_0.tar.bz2
```
- (Optional) Install the executables
```
cd build
sudo make install
```
## Program Folders - /eos/programs
- nodeos : EOSIO daemon to run a node
- cleos : cli to interact with EOSIO 
- keosd : EOSIO wallet daemon 
- eosio-launcher : application to assist with deploying a multi-node blockchain network

## Running EOS 
- Creating and Launching a Single Node Testnet
```
cd build/programs/nodeos/
./nodeos -e -p eosio \
    --plugin eosio::wallet_api_plugin \
    --plugin eosio::chain_api_plugin \
    --plugin eosio::account_history_api_plugin
```
- Starting logs
```
995855ms thread-0   wallet_plugin.cpp:41          plugin_initialize    ] initializing wallet plugin
995858ms thread-0   http_plugin.cpp:247           plugin_initialize    ] configured http to listen on 127.0.0.1:8888
...
995863ms thread-0   wallet_api_plugin.cpp:70      plugin_startup       ] starting wallet_api_plugin
995863ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/create
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/get_public_keys
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/import_key
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/list_keys
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/list_wallets
...
996120ms thread-0   chain_api_plugin.cpp:62       plugin_startup       ] starting chain_api_plugin
996120ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/abi_bin_to_json
996120ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/abi_json_to_bin
996120ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_account
...
eosio generated block 3c070cce... #41 @ 2018-04-20T22:16:37.000 with 0 trxs, lib: 40
eosio generated block 1dc4fc1f... #42 @ 2018-04-20T22:16:37.500 with 0 trxs, lib: 41
```
- Default configuration
```
~/.local/share/eosio/nodeos
|-- config
|   |-- config.ini
|   `-- genesis.json
`-- data
    |-- blocks
    |   |-- blocks.index
    |   `-- blocks.log
    `-- shared_mem
        |-- shared_memory.bin
        `-- shared_memory.meta
```

## Error resolved
- nodeos starting error
```
3285366ms thread-0   main.cpp:95                   main                 ] 10 assert_exception: Assert Exception
head_block_num() == 0: last block ID does not match current chain state
==> 
./nodeos --resync
```
