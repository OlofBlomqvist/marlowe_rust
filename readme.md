# Marlowe Lang

[![crates.io](https://img.shields.io/crates/v/marlowe_lang.svg)](https://crates.io/crates/marlowe_lang)
[![Documentation](https://docs.rs/marlowe_lang/badge.svg)](https://docs.rs/marlowe_lang)
[![BuildAndTest](https://github.com/OlofBlomqvist/marlowe_rust/actions/workflows/rust.yml/badge.svg?branch=master)](https://github.com/OlofBlomqvist/marlowe_rust/actions/workflows/rust.yml)
[![npm version](https://badge.fury.io/js/marlowe_lang.svg)](https://www.npmjs.com/package/marlowe_lang)
[![PyPI version](https://badge.fury.io/py/marlowe.svg)](https://pypi.org/project/marlowe/)

> If you just want to decode some marlowe datum from cborHex to json, [go here](https://marlowe-rs.cruma.io/)


An **experimental** Rust implementation of  Marlowe for Cardano smart (financial) contracts. See the examples dir for use with node/deno/react etc.

Note that while there is support for encoding and decoding on-chain data, this crate focuses on the off-chain parts, making it as easy as possible to create, manage and understand contracts in Rust; there will not be any support for creating actual transactions.

There is also no support for directly communicating with any Cardano or Marlowe infrastructure - this is purely an implementation of the datatypes, semantics and serialization for Marlowe.

### Main Features
- Encode/Decode Marlowe types between: MarloweDSL/Rust/Json/CborHex
- List contract parameters used in a contract (extended marlowe)
- Initialization of contract parameters (extended-marlowe).

### Unstable features
* enabled via the 'unstable' feature.
- Contract simulation (semantics::ContractInstance)
- List expected input actions (semantics::ContractInstance)

### Consuming the library

This crate can be used in Rust, React, Node, Python, Deno, wasmtime/wasmer etc., see the examples directory for more details. 

## CLI Tool:

### Installation:
```bash
rustup default nightly
cargo install marlowe_lang
```

### Examples 

#### marlowe_lang_cli -h
```text
Usage: marlowe_lang_cli <COMMAND>

Commands:
  datum        Tools for working with datums
  state        Tools for working with state
  redeemer     Tools for working with inputs/redeemers (marlowe actions)
  contract     Tools for working with contracts
  plutus-data  Tools for working with unknown plutus data
  help         Print this message or the help of the given subcommand(s)

Options:
  -h, --help     Print help information
  -V, --version  Print version information
```

#### marlowe_lang_cli decoding a datum
```text
./marlowe_lang datum from-string d8799fd8799f40ffd8799fa1d8799fd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffd8799f4040ffff1a002dc6c0a0a001ffd87c9f9fd8799fd8799fd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffd8799f581ca7f7e57db27c9e2f80c205ccb30f73e57f0ee8fc21aff7b86b5daf7845476c6f6265ffd87a9f19012cffffd87c9f9fd8799fd8799fd8799fd87a80d8799fd8799f581cfd37884bbd044c72e5f29de1b777a9c1c1d531773535cd5b55e2f6ffffd87a80ffffd8799fd87a80d8799fd8799f581cfd37884bbd044c72e5f29de1b777a9c1c1d531773535cd5b55e2f6ffffd87a80ffffd8799f581cecc8ad61b973946ee1cc666b259acabb3edf38a73f1b8779d93ba28a445377616effd87a9f1901f4ffffd87a9fd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffd87a9fd8799fd87a80d8799fd8799f581cfd37884bbd044c72e5f29de1b777a9c1c1d531773535cd5b55e2f6ffffd87a80ffffffd8799f581ca7f7e57db27c9e2f80c205ccb30f73e57f0ee8fc21aff7b86b5daf7845476c6f6265ffd87a9f19012cffd87a9fd8799fd87a80d8799fd8799f581cfd37884bbd044c72e5f29de1b777a9c1c1d531773535cd5b55e2f6ffffd87a80ffffd87a9fd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffffd8799f581cecc8ad61b973946ee1cc666b259acabb3edf38a73f1b8779d93ba28a445377616effd87a9f1901f4ffd87980ffffffff1b0000018386dd2358d87980ffffff1b000001838449f558d87980ffff cbor-hex detailed-text`

State: (MarloweDatumState Accounts([{ (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx"),(Token "" ""),3000000 },]) Bound_Values({}) Choices({}) MinTime(1))    

Continuation: Contract (Marlowe-DSL): When [ (Case (Deposit (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx") (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx") (Token "a7f7e57db27c9e2f80c205ccb30f73e57f0ee8fc21aff7b86b5daf78" "Globe") (Constant 300)) (When [ (Case (Deposit (Address "addr1v87n0zzth5zycuh972w7rdmh48qur4f3wu6ntn2m2h30dlchhlqt3") (Address "addr1v87n0zzth5zycuh972w7rdmh48qur4f3wu6ntn2m2h30dlchhlqt3") (Token "ecc8ad61b973946ee1cc666b259acabb3edf38a73f1b8779d93ba28a" "Swan") (Constant 500)) (Pay (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx") (Party (Address "addr1v87n0zzth5zycuh972w7rdmh48qur4f3wu6ntn2m2h30dlchhlqt3")) (Token "a7f7e57db27c9e2f80c205ccb30f73e57f0ee8fc21aff7b86b5daf78" "Globe") (Constant 300) (Pay (Address "addr1v87n0zzth5zycuh972w7rdmh48qur4f3wu6ntn2m2h30dlchhlqt3") (Party (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx")) (Token "ecc8ad61b973946ee1cc666b259acabb3edf38a73f1b8779d93ba28a" "Swan") (Constant 500) Close))) ] 1664414983000 Close)) ] 1664371783000 Close
```
#### marlowe_lang_cli decoding redeemer / input actions
```text 
./marlowe_lang redeemer from-string 9fd8799fd8799fd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffd8799fd87a80d8799fd8799f581c1cb51be3ab4e4b540e86bd4c9be02682db8150f69c3cded2422cc1bfffd87a80ffffd8799f581ca7f7e57db27c9e2f80c205ccb30f73e57f0ee8fc21aff7b86b5daf7845476c6f6265ff19012cffffff cbor-hex marlowe-dsl

RESULT:
 (Deposit (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx") (Address "addr1vywt2xlr4d8yk4qws675exlqy6pdhq2s76wrehkjggkvr0czta9gx") (Token "a7f7e57db27c9e2f80c205ccb30f73e57f0ee8fc21aff7b86b5daf78" "Globe") 300)
```

#### marlowe_lang_cli query contract for expected inputs
```
marlowe_lang_clicontract from-file .\test_data\swap.marlowe marlowe-dsl expected-actions -i "Timeout for Ada deposit=9999999999,Amount of Ada=4994,Amount of dollars=99,Timeout for dollar deposit=994"`
```

    Log output:
    --> INITIALIZED BY MARLOWE LANG STATE MACHINE AT 1672581873
    --> Processing When contract

**Result (current contract state):**
```json
{
  "WaitingForInput": [
    {
      "Deposit": {
        "who_is_expected_to_pay": {
          "role_token": "Ada provider"
        },
        "expected_asset_type": {
          "token_name": "",
          "currency_symbol": ""
        },
        "expected_amount": {
          "and": 4994,
          "add": 1000000
        },
        "expected_target_account": {
          "account": {
            "role_token": "Ada provider"
          }
        },
        "continuation": {
          "when": [
            ... // removed from example output for brevity 
          ],
          "timeout_continuation": "close",
          "timeout": 994
        }
      }
    }
  ]
}
```
