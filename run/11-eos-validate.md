# Validate the EOSIO environment
## Prerequiste
- finished the steps in [10-eos-install.md](10-eos-install.md) 

## Introduction
EOS comes with example contracts that can be uploaded and run for testing purposes.
We will validate our single node setup using the sample contact "currency". 
It is assumed nodeos is running as described in [10-eos-install.md](10-eos-install.md)

## Run currency contract

### Create a wallet
### Import the Private Key for eosio Account
- We need to add the private key of eosio account to our wallet so we can work with it. 
```
./cleos wallet import <eosio_account_private_key>
```
### Load the Bios Contract
- Set eosio.bios as the default system contract. 
- This contract enables you to have direct control over the resource allocation of other accounts and to access other privileged API calls.
```
./cleos set contract eosio \
        build/contracts/eosio.bios/ \
        build/contracts/eosio.bios/eosio.bios.wast \
        build/contracts/eosio.bios/eosio.bios.abi
```
### Create an account for the “currency” contract
### Upload the sample “currency” contract to the blockchain
### Transfer funds using the “currency” contract
### Check the “currency” contract balances


## Reference
- https://infinitexlabs.com/first-steps-in-eos-blockchain-development/
