# WSL(Windows Subsystem for Linux) 

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

## EOS Local Env on Ubuntu
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
995858ms thread-0   chain_plugin.cpp:99           plugin_initialize    ] initializing chain plugin
995858ms thread-0   net_plugin.cpp:2711           plugin_initialize    ] Initialize net plugin
995859ms thread-0   net_plugin.cpp:2734           plugin_initialize    ] host: 0.0.0.0 port: 9876
995860ms thread-0   net_plugin.cpp:2810           plugin_initialize    ] my node_id is ed948db5bbe63ff052fd05b1157b5bf56804877cebea1babea6534dfc3f01e50
995861ms thread-0   main.cpp:90                   main                 ] nodeos version 380ec6a4
995861ms thread-0   main.cpp:91                   main                 ] eosio root is /home/steward/.local/share
995861ms thread-0   http_plugin.cpp:285           plugin_startup       ] start listening for http requests
995863ms thread-0   wallet_api_plugin.cpp:70      plugin_startup       ] starting wallet_api_plugin
995863ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/create
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/get_public_keys
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/import_key
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/list_keys
995864ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/list_wallets
995865ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/lock
995865ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/lock_all
995865ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/open
995865ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/set_timeout
995866ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/sign_transaction
995866ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/wallet/unlock
995964ms thread-0   block_log.cpp:120             open                 ] Log is nonempty
995966ms thread-0   block_log.cpp:128             open                 ] Index is nonempty
996119ms thread-0   chain_plugin.cpp:208          plugin_startup       ] starting chain in read/write mode
996119ms thread-0   chain_plugin.cpp:213          plugin_startup       ] Blockchain started; head block is #39, genesis timestamp is 2018-03-01T12:00:00.000
996120ms thread-0   chain_api_plugin.cpp:62       plugin_startup       ] starting chain_api_plugin
996120ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/abi_bin_to_json
996120ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/abi_json_to_bin
996120ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_account
996121ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_block
996121ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_code
996121ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_currency_balance
996121ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_currency_stats
996121ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_info
996121ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_required_keys
996122ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/get_table_rows
996122ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/push_block
996122ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/push_transaction
996122ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/chain/push_transactions
996123ms thread-0   account_history_api_plugin.cpp:45 plugin_startup       ] starting account_history_api_plugin
996123ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/account_history/get_controlled_accounts
996123ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/account_history/get_key_accounts
996123ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/account_history/get_transaction
996124ms thread-0   http_plugin.cpp:325           add_handler          ] add api url: /v1/account_history/get_transactions
996126ms thread-0   net_plugin.cpp:2822           plugin_startup       ] starting listener, max clients is 25
996126ms thread-0   producer_plugin.cpp:161       plugin_startup       ] producer plugin:  plugin_startup() begin
996126ms thread-0   producer_plugin.cpp:166       plugin_startup       ] Launching block production for 1 producers.
996127ms thread-0   producer_plugin.cpp:176       plugin_startup       ] producer plugin:  plugin_startup() end
996502ms thread-0   fork_database.cpp:78          _push_block          ] Number of missed blocks: 20
eosio generated block 7b7783e9... #40 @ 2018-04-20T22:16:36.500 with 0 trxs, lib: 39
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
## Reference
- https://github.com/EOSIO/eos/wiki/Local-Environment
- https://steemit.com/eos/@tokenika/installing-and-running-eos-on-windows
