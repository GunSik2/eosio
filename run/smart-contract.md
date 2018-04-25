# 스마트컨트랙트 맛보기 튜토리얼

## 스마트컨트랙트 시작하기
두 부로 나눠 진행한다.
스마트컨트랙트 시험을 위한 로컬 블럭체인 설치해 보기 
- 로컬 블럭체인 실행
- 지갑 생성
- 바이오스 컨트랙트 로딩
- 계정 생성

자신만의 스마트 계약서를 생성하고 배포해 보기
- eosio.token 계약
- exchange 계약
- HelloWorld 계약

## 로컬 블럭체인 실행
```
$ nodeos -e -p eosio --plugin eosio::wallet_api_plugin --plugin eosio::chain_api_plugin --plugin eosio::account_history_api_plugin 
```

## 지갑 생성
지갑은 블럭체인 실행 인가에 필요한 개인 키 저장소로, 지갑 키로 암호화하여 디스크에 저장한다.
```
$ cleos wallet create
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5JuBXoXJ8JHiCTXfXcYuJabjF9f9UNNqHJjqDVY7igVffe3pXub"

$ cleos wallet unlock --password PW5JuBXoXJ8JHiCTXfXcYuJabjF9f9UNNqHJjqDVY7igVffe3pXub
$ cleos wallet lock
```

## 바이오스 컨트랙트 로딩
기본 시스템 계약을 설정한다. 기본 값으로 eosio.bios 계약은 계정 별 리소스 할당을 제어한다.
eosio.bios 계약은 contracts/eosio.bios 하위에 위치한다. 
```
$ cleos set contract eosio build/contracts/eosio.bios -p eosio
Reading WAST/WASM from contracts/eosio.bios/eosio.bios.wast...
Assembling WASM...
Publishing contract...
executed transaction: 60a0522ae5b78fcc83e1feb5e12039770997ad8f56883b89c5f6b16b83ba99f9  3288 bytes  2200576 cycles
#         eosio <= eosio::setcode               {"account":"eosio","vmtype":0,"vmversion":0,"code":"0061736d0100000001581060037f7e7f0060057f7e7e7e7e...
#         eosio <= eosio::setabi                {"account":"eosio","abi":{"types":[],"structs":[{"name":"set_account_limits","base":"","fields":[{"n...
```

## 구좌 생성
- 구좌 생성
```
$ cleos create key
Private key: 5HpMAapnBSSusqediNddgnTa4kSxxeoPiHHnWqmhQGgbp8ZzUbh
Public key: EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v

$ cleos wallet import 5HpMAapnBSSusqediNddgnTa4kSxxeoPiHHnWqmhQGgbp8ZzUbh
imported private key for: EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v

$ cleos wallet list
$ cleos wallet keys
..
  [
    "EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v",
    "5HpMAapnBSSusqediNddgnTa4kSxxeoPiHHnWqmhQGgbp8ZzUbh"
  ]
..
```
- 사용자 계정 생성
```
$ cleos create account eosio user EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
executed transaction: 2cb828cb8f95774f442ded5a6f51e4d5b89cc80e64daba3a7961a03c8b5fa68e  352 bytes  102400 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"user","owner":{"threshold":1,"keys":[{"key":"EOS7nbHJCKH1ofvSjmb9Aw77ajjG...

$ cleos create account eosio tester EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
executed transaction: ddd4dbeae2e439f920dd5fbc76f64669334d21ff2844efbb19a0b77a66dd0089  352 bytes  102400 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"tester","owner":{"threshold":1,"keys":[{"key":"EOS7nbHJCKH1ofvSjmb9Aw77aj...
```

## eosio.token 계약
## exchange 계약
## HelloWorld 계약

## Reference
- https://github.com/EOSIO/eos/wiki/Tutorial-Getting-Started-With-Contracts
- https://objectcomputing.com/resources/publications/sett/february-2018-eos-smart-contracts
