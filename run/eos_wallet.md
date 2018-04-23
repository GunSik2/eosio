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
### managing multiple wallets 
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

$ ./cleos wallet lock -n testuser2

$ ./cleos wallet unlock -n testuser2
```

### Reopn wallet after restarting nodeos
```
$ cleos wallet open

$ cleos wallet list
Wallets:
[
  "default"
]

$ cleos wallet open -n testuser1

$ cleos wallet open -n testuser1

$ cleos wallet list
Wallets:
[
  "default",
  "testuser1",
  "testuser2"
]
```

### Generating and Importing EOSIO Keys
```
$ ./cleos create key
Private key: 5KJNAcrz3uK8bE4sfJ1wSrmsrdySzD7kM8H8m65Xnuyx6vcK6ey
Public key: EOS8SBn4J3Kkk9X3KMFdYowmjZVujPY4MuiFpkQ1SiZfhpWEcsMGQ

$ ./cleos create key
Private key: 5J34pdZWerAAyecdQa1rV3W9WaLLvqJyAkAB5kRHpvmHx9WgstF
Public key: EOS6m2t4D1UorWkunezVLNte5eaaDLvTtubfY2EPi1xgLfN95yaQU

$ cleos wallet import 5KJNAcrz3uK8bE4sfJ1wSrmsrdySzD7kM8H8m65Xnuyx6vcK6ey
imported private key for: EOS8SBn4J3Kkk9X3KMFdYowmjZVujPY4MuiFpkQ1SiZfhpWEcsMGQ

$ cleos wallet import 5J34pdZWerAAyecdQa1rV3W9WaLLvqJyAkAB5kRHpvmHx9WgstF
imported private key for: EOS6m2t4D1UorWkunezVLNte5eaaDLvTtubfY2EPi1xgLfN95yaQU

$ cleos wallet keys
[[
    "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
    "5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"
  ],[
    "EOS6m2t4D1UorWkunezVLNte5eaaDLvTtubfY2EPi1xgLfN95yaQU",
    "5J34pdZWerAAyecdQa1rV3W9WaLLvqJyAkAB5kRHpvmHx9WgstF"
  ],[
    "EOS8SBn4J3Kkk9X3KMFdYowmjZVujPY4MuiFpkQ1SiZfhpWEcsMGQ",
    "5KJNAcrz3uK8bE4sfJ1wSrmsrdySzD7kM8H8m65Xnuyx6vcK6ey"
  ]
]
```

### Creating an Account
```
$ cleos create account eosio myaccount \
        EOS6m2t4D1UorWkunezVLNte5eaaDLvTtubfY2EPi1xgLfN95yaQU \
        EOS6m2t4D1UorWkunezVLNte5eaaDLvTtubfY2EPi1xgLfN95yaQU
executed transaction: 5a99112b0108888f33c187350c7af25cb6ac908cd855ba359436f7dc58ef90cc  352 bytes  102400 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"myaccount","owner":{"threshold":1,"keys":[{"key":"EOS6m2t4D1UorWkunezVLNt...
```


## Reference
- https://github.com/EOSIO/eos/wiki/Tutorial-Comprehensive-Accounts-and-Wallets
