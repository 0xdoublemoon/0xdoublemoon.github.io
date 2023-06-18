---
layout: default
title: Development Tools
parent: Web3
nav_order: 2
---

# Ganache

## Introduction

Ganache is a local development blockchain used to develop decentralized applications on the Ethereum blockchain. It simulates the Ethereum network, and you can see how your DApp will perform before you release it to production.


By default, Ganache provides 10 test accounts, each with 1000 (fake) Ether along with the corresponding private keys and the mnemonic phrase used to generate them. As a result,  we can deploy our smart contract to local blockchain to test with those fake Ether. It is convinient to use. 



## Installation
1. install via image: https://trufflesuite.com/ganache/
2. install & run via cli:
```
npm install ganache
ganache
```

prerequiste:  `Node.js >= v12.0.0 and NPM >= 6.4.1`



# Hardhat

1. install the hardhat in the project:
```
yarn add hardhat
```
2. In addition to ganache, hardhat also provides a way to start a local ethereum node
```
npx hardhat node
```



# IPFS

install ipfs locally:

```
wget https://dist.ipfs.io/go-ipfs/v0.4.18/go-ipfs_v0.4.18_linux-amd64.tar.gz
tar xvfz go-ipfs_v0.4.18_linux-amd64.tar.gz
sudo mv go ipfs/ipfs /usr/local/bin/ipfs
ipfs init
ipfs version
```

---

# Example

Step 1: switch to use node 18: 
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash 
nvm install 18 
nvm use 18 
nvm alias default 18 
npm install npm --global # Upgrade npm to the latest version
```



Step 2: init a project:
```
mkdir <yourprojectname> && cd <yourprojectname>
yarn init
yarn add --dev hardhat
npx hardhat
```


Step 3: install plugins: 
```
yarn add --dev @nomicfoundation/hardhat-toolbox @nomicfoundation/hardhat-network-helpers @nomicfoundation/hardhat-chai-matchers @nomiclabs/hardhat-ethers @nomiclabs/hardhat-etherscan chai ethers hardhat-gas-reporter solidity-coverage @typechain/hardhat typechain @typechain/ethers-v5 @ethersproject/abi @ethersproject/providers
```


Step4: compile sample smart contract

```
npx hardhat compile
```


Step 5: run deployment script

```
npx hardhat run scripts/deploy.ts
```


*You might have error below:*
```
#HH303: Unrecognized task
```

so downgrade `ethers` version to `^5.4.7`  and rerun.

You will get the successful result like this:
![[npx hardhat run command.png]]



# Alternatively 

## Foundry

```
curl -L https://foundry.paradigm.xyz | bash

foundryup
```
