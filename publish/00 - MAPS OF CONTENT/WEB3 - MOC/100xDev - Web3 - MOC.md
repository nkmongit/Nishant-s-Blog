---
date created: Saturday, August 3rd 2024, 3:29:58 pm
date modified: Sunday, August 4th 2024, 1:56:27 am
tags:
  - 100xdevs
  - moc/web3
  - web3
---
# Web3 - Client side

Pre-requisite - **Basic Javascript/Node.js**

## General

| Easy                                                                                                               | Medium                                                      | Hard |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------- | ---- |
| Intro to blockchains, decentralization, BTC, ETH and SOL                                                           |                                                             |      |
|                                                                                                                    | Basic cryptography, hashing, encryption, sha256, keccak256, |      |
|                                                                                                                    | Gas, txns, public and private keys, edd25119, pneumonics    |      |
|                                                                                                                    | RPCs, common RPC methods on SOL and ETH                     |      |
| Gas, Native tokens, Transactions, Programs, Instructions, Airdropping, Block explorers, Creating wallets, pvt keys |                                                             |      |

## Ethereum

|Easy|Medium|Hard|
|---|---|---|
||What is eth, proof of stake||
|||EVM Architecture, State, Bytecode, Opcodes, ABIs, transaction processing and gas, EOAs vs Contract accounts|
||Wallet adapters in ETH||
||ETH on the server, etherjs||
||ETH with React and Next.js||

## Solana

| Easy                                      | Medium                                     | Hard |
| ----------------------------------------- | ------------------------------------------ | ---- |
|                                           | Creating a token, atas, attaching metadata |      |
| Create NFTs, attaching metadata, metaplex | Basics of a DEX, AMMs, liquidity pools     |      |
|                                           | Creating a token                           |      |
|                                           | Creating a swap pool, funding it.          |      |
|                                           | Wallet adapters on Solana,                 |      |
|                                           | Solana on the backend, @solana/web3.js     |      |
|                                           | Solana with Next.js                        |      |

### Projects

1. Create a client side wallet in JS, supporting transfers, txns and swaps
2. Create a token launch and transfer program on solana
3. Create a cloud wallet in Node.js
4. Creating BonkBot on SOL

# Web3 - Contracts

## Solidity basics (Remix)

| Easy                                                                    | Medium                 | Hard |
| ----------------------------------------------------------------------- | ---------------------- | ---- |
| What is solidity, what are contracts?                                   |                        |      |
| Solidity builds, abis, binaries and EVM                                 |                        |      |
| Storing state, variables, types, visibility (public, private), loops    |                        |      |
| array, structs, mappings                                                |                        |      |
| require, modifiers, Ownable contract                                    |                        |      |
| Inheritence                                                             |                        |      |
| Events                                                                  |                        |      |
|                                                                         | Interfaces and CPIs    |      |
|                                                                         | Gas optimisations      |      |
|                                                                         | Native payment support |      |
|                                                                         | abis, bytecode         |      |
| Sepolia test network, airdrop yourself some tokens, contract deployment |                        |      |

## Solidity Advance

| Easy                                                                 | Medium                                             | Hard |
| -------------------------------------------------------------------- | -------------------------------------------------- | ---- |
| Intro to ganache, truffle, Foundry                                   |                                                    |      |
| Writing contracts in Foundry, setting up, testing a project locally. |                                                    |      |
|                                                                      | Testing contract locally, deploying using Fourndry |      |
|                                                                      | Gas optimisations                                  |      |
|                                                                      | Proxy contracts                                    |      |
|                                                                      | Upgradable contracts                               |      |

## Writing contracts in Solidity

| Easy           | Medium                                                   | Hard |
| -------------- | -------------------------------------------------------- | ---- |
| ERC20, ERC 720 | proxy contracts                                          |      |
|                | marketplace contract                                     |      |
|                | DEX, AMM and liquidity pools, constant product algorithm |      |
|                | Exploring OpenZeppelin contracts                         |      |
|                | Staking in leiu of tokens                                |      |

## Rust basics

|Easy|Medium|Hard|
|---|---|---|
|Installing rust, IDE Setup|||
|Variables, data types, loops, functions, struct|||
|enums, pattern matching,|||
|package management (packages, crates, modules),|||
||Mutability||
||Memory management||
||ownership,||
|referencing and borrowing|||
||Options, Errors, Error Handling||

## Rust advance

|Easy|Medium|Hard|
|---|---|---|
|||Lifetimes|
|||Traits|
|Generics|||
||async await syntax||
|||Iterators|
||Multi threading, concurrency||
|||Macros|

## Programs on Solana

| Easy | Medium                                          | Hard                             |
| ---- | ----------------------------------------------- | -------------------------------- |
|      | Programs in solana                              |                                  |
|      | Accounts vs programs vs instructions, Owners    | Decoding a transaction on solana |
|      | Programs vs. Smart Contract                     | Data model on Solana, PDAs, bump |
|      | Writing a simple raw program in solana.         |                                  |
|      | Token program , ATA, metadata program, metaplex |                                  |
|      | Anchor vs raw programs                          |                                  |
|      | web2 like program                               |                                  |
|      | Staking program                                 |                                  |

## Web2 + Web3

| Easy | Medium                                             | Hard                                             |
| ---- | -------------------------------------------------- | ------------------------------------------------ |
|      | Private key management on a server. Shamir secrets |                                                  |
|      |                                                    | Indexing blockchains                             |
|      |                                                    | Transaction parsing, Logs and indexed parameters |
|      |                                                    | Sweeping wallets, new wallet creation logic      |

**Projects**

Creating a crypto payment gateway (web3 stripe).
Creating a Centralised exchange / Creating a crypto gambling website.