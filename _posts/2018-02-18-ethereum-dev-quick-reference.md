---
ID: 724
post_title: Ethereum Dev Quick Reference
author: Luc
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/ethereum-dev-quick-reference/
published: true
tags:
  - ethereum
categories:
  - ethereum
post_date: 2018-02-18 12:48:56
---
## Set Up Local Dev Account for Development
Install and set up a local dev account like this (Ubuntu):

    sudo apt-get install software-properties-common
    sudo add-apt-repository -y ppa:ethereum/ethereum
    sudo apt-get update
    sudo apt-get install ethereum

    $ geth --dev account new
    Passphrase:
    Repeat passphrase:
    Address: {7ebf0b662cc56a6d6ff8ae6a31efcefeb9014996}
    $ geth --dev --rpc --datadir "~/.ethereum-dev" --mine --minerthreads 1 console 2>> ~/.ethereum-dev.log
    Welcome to the Geth JavaScript console!

    instance: Geth/v1.8.0-stable-5f540757/linux-amd64/go1.9.4
    coinbase: 0x54e963cb2001e6370bef4b18c4ab9991618c68e2
    at block: 0 (Wed, 31 Dec 1969 19:00:00 EST)
     datadir: /home/.ethereum-dev
     modules: admin:1.0 clique:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 shh:1.0 txpool:1.0 web3:1.0
    >

## Get Some Test Ether
Start geth with the `--mine` option:

    geth --testnet --datadir "~/.ethereum-testnet" --mine console 2>> ~/.ethereum-testnet.log

In another session, check logs for mining activity:

    tail -f ~/.ethereum-testnet.log | grep -i 'mined'

## Check How Many Accounts You Have
Go to the geth console and try a few commands:

    > personal.listAccounts
    ["0x926cdd37c279f38e941bde52003f865859aabb76"]
    > personal.unlockAccount(eth.coinbase)
    Unlock account 0x926cdd37c279f38e941bde52003f865859aabb76
    Passphrase:
    true

The first one in the list is referred to as the coinbase and can be referred to with `eth.coinbase`. This will earn the ether mining rewards.

## Check Balances and Transfer Between Accounts

This shows the commands for sending between two accounts and checking balances. Note you first need to unlock the account:


    > var from = eth.accounts[0];
    undefined
    > var to   = eth.accounts[1];
    undefined
    > personal.unlockAccount(from)
    Unlock account 0x926cdd37c279f38e941bde52003f865859aabb76
    Passphrase:
    true
    > eth.sendTransaction({from:from, to:to, value: web3.toWei(1, "ether")})
    "0x4c169af406aed32d5b072c2ee2ac246a22b650c68aa29b1b7ff0dfd2b7f56813"
    > web3.fromWei(eth.getBalance(from))
    1772
    > web3.fromWei(eth.getBalance(to))
    1


## Install Solidity And Create a Simple Contract
Note that some Ethereum documentation is out of date, and refers to using Solidity directly from geth, which is not currently possible. See [this issue](https://github.com/ethereum/go-ethereum/issues/3793). If you attempt this, you may see:

    > web3.eth.getCompilers()
    Error: The method eth_getCompilers does not exist/is not available


### Install
There are several options for creating a contract on your local machine. One is to install the Solidity compiler, and import compiled files into geth. For Ubuntu:

    sudo add-apt-repository ppa:ethereum/ethereum
    sudo apt-get update
    sudo apt-get install solc
    which solc

Further instructions [here](http://solidity.readthedocs.io/en/develop/installing-solidity.html):

### Create A Contract
These instructions are summarized from [this answer](https://ethereum.stackexchange.com/a/15436/8317).

Create a new file, e.g. Test.sol:

    pragma solidity ^0.4.8;

    contract Test {
        uint256 public value;

        function Test() {
            value = 123;
        }
    }

Compile with:

    echo "var testOutput=`solc --optimize --combined-json abi,bin,interface Test.sol`" > test.js

Check what's in test.js:

    $ cat test.js
    var testOutput={"contracts":{"Test.sol:Test":{"abi":"[{"constant":true,"inputs":[],"name":"value","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"inputs":[],"payable":false,"type":"constructor"}]","bin":"60606040523415600b57fe5b5b607b6000819055505b5b608f806100246000396000f30060606040526000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680633fa4f24514603a575bfe5b3415604157fe5b6047605d565b6040518082815260200191505060405180910390f35b600054815600a165627a7a72305820d0e71d151634ac6ae7626860a17881104022e5cd6d3a088eb8f941d9aa8e3bd20029"}},"version":"0.4.9+commit.364da425.Darwin.appleclang"}

Load the file in the geth console:

    > loadScript("test.js");
    true

Check the contract was loaded successfully by printing content of `testOutput`, which is part of the original test.js:

    > testOutput
{
  contracts: {
    Test.sol:Test: {
      abi: "[{\"constant\":true,\"inputs\":[],\"name\":\"value\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
      bin: "60606040523415600e57600080fd5b607b6000556097806100216000396000f300606060405260043610603e5763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416633fa4f24581146043575b600080fd5b3415604d57600080fd5b60536065565b60405190815260200160405180910390f35b600054815600a165627a7a723058202f93ec48a1ccfa576ade88c20cabe03f331b44581df974fd98057a27607a30df0029"
    }
  },
  version: "0.4.19+commit.c4cbbb05.Linux.g++"
}


