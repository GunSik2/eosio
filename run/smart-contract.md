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
- 구좌 용 키 생성
```
$ cleos create key
Private key: 5HpMAapnBSSusqediNddgnTa4kSxxeoPiHHnWqmhQGgbp8ZzUbh
Public key: EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
```
- 지갑에 키 등록
```
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
- 사용자 구좌 생성
```
$ cleos create account eosio user EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
executed transaction: 2cb828cb8f95774f442ded5a6f51e4d5b89cc80e64daba3a7961a03c8b5fa68e  352 bytes  102400 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"user","owner":{"threshold":1,"keys":[{"key":"EOS7nbHJCKH1ofvSjmb9Aw77ajjG...

$ cleos create account eosio tester EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
executed transaction: ddd4dbeae2e439f920dd5fbc76f64669334d21ff2844efbb19a0b77a66dd0089  352 bytes  102400 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"tester","owner":{"threshold":1,"keys":[{"key":"EOS7nbHJCKH1ofvSjmb9Aw77aj...
```

- 사용자 계정 조회
```
$ cleos get account user
```

## eosio.token 계약 배포
- token 계약용 account 생성 
```
$ cleos create account eosio eosio.token EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
executed transaction: ada493cb8035438af9cc26080653e0f0daa0c81dcc167b60d4048487ef436a7a  352 bytes  102400 cycles
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"eosio.token","owner":{"threshold":1,"keys":[{"key":"EOS7nbHJCKH1ofvSjmb9A...
```
- token 계약 배포
```
$ cleos set contract eosio.token build/contracts/eosio.token -p eosio.token
Reading WAST/WASM from contracts/eosio.token/eosio.token.wast...
Assembling WASM...
Publishing contract...
executed transaction: fb83dc0ea9a10927bf5a164490922851b32006cd68b36b398d259880250689d4  8288 bytes  2200576 cycles
#         eosio <= eosio::setcode               {"account":"eosio.token","vmtype":0,"vmversion":0,"code":"0061736d010000000183011560067f7e7f7f7f7f00...
#         eosio <= eosio::setabi                {"account":"eosio.token","abi":{"types":[],"structs":[{"name":"transfer","base":"","fields":[{"name"...
```
- token 계약 인터페이스: contracts/eosio.token/eosio.token.hpp
```
   void create( account_name issuer,
                asset        maximum_supply,
                uint8_t      can_freeze,
                uint8_t      can_recall,
                uint8_t      can_whitelist );


   void issue( account_name to, asset quantity, string memo );

   void transfer( account_name from,
                  account_name to,
                  asset        quantity,
                  string       memo );
```
- EOS 토큰 생성
```
$ cleos push action eosio.token create '[ "eosio", "1000000000.0000 EOS", 0, 0, 0]' -p eosio.token
executed transaction: dd11dd99cc24d9307072dc8e00aa2499f96bb181c8eaf481b04aa4add7d6d1de  248 bytes  104448 cycles
#   eosio.token <= eosio.token::create          {"issuer":"eosio","maximum_supply":"1000000000.0000 EOS","can_freeze":0,"can_recall":0,"can_whitelis...
```
- 'user' 구좌에 토큰 발행
```
$ cleos push action eosio.token issue '[ "user", "100.0000 EOS", "memo" ]' -p eosio
executed transaction: 2e341457384db6b09df2213dcd80f08dfedfd48974cc14050cea651239442161  256 bytes  126976 cycles
#   eosio.token <= eosio.token::issue           {"to":"user","quantity":"100.0000 EOS","memo":"memo"}
>> issue
#   eosio.token <= eosio.token::transfer        {"from":"eosio","to":"user","quantity":"100.0000 EOS","memo":"memo"}
>> transfer
#         eosio <= eosio.token::transfer        {"from":"eosio","to":"user","quantity":"100.0000 EOS","memo":"memo"}
#          user <= eosio.token::transfer        {"from":"eosio","to":"user","quantity":"100.0000 EOS","memo":"memo"}
```
- 'test' 구좌에 토큰 이체 (from user 구좌)
```
$ cleos push action eosio.token transfer '[ "user", "tester", "25.0000 EOS", "m" ]' -p user
executed transaction: 4ff33c42dcd221693ba8b7f4b13dafabd37ed731d5d008b2d071e1b6add9de14  256 bytes  111616 cycles
#   eosio.token <= eosio.token::transfer        {"from":"user","to":"tester","quantity":"25.0000 EOS","memo":"m"}
>> transfer
#          user <= eosio.token::transfer        {"from":"user","to":"tester","quantity":"25.0000 EOS","memo":"m"}
#        tester <= eosio.token::transfer        {"from":"user","to":"tester","quantity":"25.0000 EOS","memo":"m"}

```

## exchange 계약 배포
```
$ cleos create account eosio exchange EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
$ cleos set contract exchange build/contracts/exchange -p exchange
```
## Eosio.msig 계약 배포
```
$ cleos create account eosio eosio.msig EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
$ cleos set contract eosio.msig build/contracts/eosio.msig -p eosio.msig
```
## HelloWorld 계약 배포
- hello/hello.cpp
```
#include <eosiolib/eosio.hpp>
#include <eosiolib/print.hpp>
using namespace eosio;

class hello : public eosio::contract {
  public:
      using contract::contract;

      /// @abi action 
      void hi( account_name user ) {
         print( "Hello, ", name{user} );
      }
};

EOSIO_ABI( hello, (hi) )
```
- Compile
```
$ eosiocpp -o hello.wast hello.cpp
```
- Generate the abi
```
$ eosiocpp -g hello.abi hello.cpp
```
- account 생성 및 계약 배포
```
$ cleos create account eosio hello.code EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v EOS7nbHJCKH1ofvSjmb9Aw77ajjGAzsexuSJ8TGTVm9FgDDGyqm8v
$ cleos set contract hello.code ../hello -p hello.code
```
- 계약 실행
```
$ cleos push action hello.code hi '["user"]' -p user
$ cleos push action hello.code hi '["user"]' -p tester
```
- 사용자 인증 기능 추가 후 컴파일, 배포
```
void hi( account_name user ) {
   require_auth( user );
   print( "Hello, ", name{user} );
}
```
- 계약 실행 : 유저와 권한이 다른 경우
```
$ cleos push action hello.code hi '["tester"]' -p user
```
- 계약 실행 : 유저와 권한이 같은 경우
```
$ cleos push action hello.code hi '["tester"]' -p tester
```

## Reference
- https://github.com/EOSIO/eos/wiki/Tutorial-Getting-Started-With-Contracts
- https://github.com/EOSIO/eos/wiki/Tutorial-eosio-token-Contract
- https://github.com/EOSIO/eos/wiki/Tutorial-Hello-World-Contract
- https://objectcomputing.com/resources/publications/sett/february-2018-eos-smart-contracts
