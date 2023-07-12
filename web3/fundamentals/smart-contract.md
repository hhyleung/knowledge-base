# Smart Contract

> An arrangement between two or more parties exchanging digital assets, where at least one of these parties allocates digital assets at the contracts initiation which are then redistributed to all involved parties in accordance with a predefined protocol encoded in logic and a state that is initialised at the start of the contract.

> Programs running on the blockchain that can execute automatically when certain conditions are met.

## Use cases

* Supply chain: simplify paper work and increase efficiency
* Decentralised finance (DeFi): decentralised autonomous organisation (DAO)
* Gambling: bets processed fairly and predictably
* Social networks: free from bots and fake accounts
* Gaming: prevent cheating and establish score keeping functionality

## Platforms

* Ethereum: most popular smart contract platform, Ether - second largest cryptocurrency
* EOS.IO: fast protocol elmintating transaction fee powered by cryptocurrency EOS
* Hyperledger: started by Linux Foundation, contributed by IBM, Intel, SAP
* Corda: permissioned blockchain by R3

## Lifecycle

1. Write in Solidity
2. Compile into EVM bytecode
3. Deployment transaction: local to peer node, until mining node
4. Mining node writes to next block

## Vulnerability

* Reentrancy / recusive call attacks
* Integer over/underflow / arithmetic attacks
* Transaction order dependence
* Denial of service with block gas limit
* Unprotected self-destruct
* Timestamp manipulation
* Delegatecall
