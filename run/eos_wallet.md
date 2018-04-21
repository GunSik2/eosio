## EOSIO Accounts and Wallets Conceptual Overview
[https://github.com/EOSIO/eos/wiki/assets/Accounts-and-Wallets-Overview.png]

## cleos
### create master wallet
```
$ cd eos/build/programs/cleos

$ ./cleos wallet create
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5K9Cnq92DK1RNeZ9z6XLwuXnNEQk2mBkSMcgexUBXaoLM57G3Bn"

$ ls -l ~/.local/share/eosio/nodeos/data/
default.wallet

$ ./cleos wallet list
Wallets:
[
  "default *"
]
```
### create user wallet
```
$ ./cleos wallet create -n testuser1
Creating wallet: testuser1
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5KWjR6wY2L5dPfV47KXqgGSeK3KScmCBVWRN93vnFueAoAjUHpF"

$ ./cleos wallet create -n testuser2
Creating wallet: testuser2
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5K3GeVFg7gtFiWVi363JxJF4srYZTC7TvGb7KFnBrvLACHftja8"

$ ls ~/.local/share/eosio/nodeos/data/
default.wallet
testuser1.wallet
testuser2.wallet

$ ./cleos wallet list
Wallets:
[
  "default *",
  "testuser1 *",
  "testuser2 *"
]
```

## Reference
- https://github.com/EOSIO/eos/wiki/Tutorial-Comprehensive-Accounts-and-Wallets
