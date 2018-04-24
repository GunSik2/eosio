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
cleos set contract eosio build/contracts/eosio.bios -p eosio
```

## 구좌 생성
- 구좌 생성
```
$ cleos create key
Private key: 5Jmsawgsp1tQ3GD6JyGCwy1dcvqKZgX6ugMVMdjirx85iv5VyPR
Public key: EOS7ijWCBmoXBi3CgtK7DJxentZZeTkeUnaSDvyro9dq7Sd1C3dC4

$ cleos wallet import 5Jmsawgsp1tQ3GD6JyGCwy1dcvqKZgX6ugMVMdjirx85iv5VyPR
imported private key for: EOS7ijWCBmoXBi3CgtK7DJxentZZeTkeUnaSDvyro9dq7Sd1C3dC4

$ cleos wallet list
$ cleos wallet keys
```
- 사용자 계정 생성
```
$ cleos create account eosio user EOS7ijWCBmoXBi3CgtK7DJxentZZeTkeUnaSDvyro9dq7Sd1C3dC4 EOS7ijWCBmoXBi3CgtK7DJxentZZeTkeUnaSDvyro9dq7Sd1C3dC4
executed transaction: 8aedb926cc1ca31642ada8daf4350833c95cbe98b869230f44da76d70f6d6242  364 bytes  1000 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"user","owner":{"threshold":1,"keys":[{"key":"EOS7ijWCBmoXBi3CgtK7DJxentZZ...

$ cleos create account eosio tester EOS7ijWCBmoXBi3CgtK7DJxentZZeTkeUnaSDvyro9dq7Sd1C3dC4 EOS7ijWCBmoXBi3CgtK7DJxentZZeTkeUnaSDvyro9dq7Sd1C3dC4
executed transaction: 414cf0dc7740d22474992779b2416b0eabdbc91522c16521307dd682051af083 366 bytes  1000 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"tester","owner":{"threshold":1,"keys":[{"key":"EOS7ijWCBmoXBi3CgtK7DJxentZZ...
```

## eosio.token 계약
## exchange 계약
## HelloWorld 계약

## Reference
- https://github.com/EOSIO/eos/wiki/Tutorial-Getting-Started-With-Contracts
- https://objectcomputing.com/resources/publications/sett/february-2018-eos-smart-contracts
