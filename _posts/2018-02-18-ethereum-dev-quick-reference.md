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

[TOC]: # " "

- [Set Up A Local Development Environment](#set-up-a-local-development-environment)
    - [Configure Local Environment to Create Test Ether](#configure-local-environment-to-create-test-ether)
    - [Check How Many Accounts You Have](#check-how-many-accounts-you-have)
    - [Check Balances and Transfer Between Accounts](#check-balances-and-transfer-between-accounts)
- [Install Solidity And Create a Simple Contract](#install-solidity-and-create-a-simple-contract)
    - [Install](#install)
    - [Create A Contract](#create-a-contract)
- [Use web3.py To Interact with Geth from Python](#use-web3py-to-interact-with-geth-from-python)
- [Connect to a Local Development Environment With Remix](#connect-to-a-local-development-environment-with-remix)




## Set Up A Local Development Environment
Install and set up a local development account like this (Ubuntu):

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

### Configure Local Environment to Create Test Ether
The `--mine` option produces test ether:

    geth --dev --rpc --datadir "~/.ethereum-dev" --mine --minerthreads 1 console 2>> ~/.ethereum-dev.log

In another session, check logs for mining activity:

    tail -f ~/.ethereum-dev.log

In dev mode, the node only mines if there are transactions. So to see activity here, send a transaction as below. Logging should then show:

    INFO [02-18|14:43:14] Submitted transaction                    fullhash=0x7b847e1811f6369b67e747f1896ae8638fc61d228d57a7d5e3bf02bcd88ab3d4 recipient=0x293101d657761cADF9C353AD8F1d09A5820eD677
    INFO [02-18|14:43:14] Commit new mining work                   number=1 txs=1 uncles=0 elapsed=1.067ms
    INFO [02-18|14:43:14] Successfully sealed new block            number=1 hash=dbae4b…5cf9a8
    INFO [02-18|14:43:14] 🔨 mined potential block                  number=1 hash=dbae4b…5cf9a8
    INFO [02-18|14:43:14] Commit new mining work                   number=2 txs=0 uncles=0 elapsed=1.237ms

### Check How Many Accounts You Have
Go to the geth console and try a few commands:

     > personal.newAccount()
    Passphrase:
    Repeat passphrase:
    "0x293101d657761cadf9c353ad8f1d09a5820ed677"
    > personal.listAccounts
    ["0x926cdd37c279f38e941bde52003f865859aabb76"]
    > personal.unlockAccount(eth.coinbase)
    Unlock account 0x926cdd37c279f38e941bde52003f865859aabb76
    Passphrase:
    true

The first account is referred to as the coinbase and can be accessed with `eth.coinbase`. This address will earn the mining rewards:

    > web3.fromWei(eth.getBalance(eth.coinbase))
    1.15792

### Check Balances and Transfer Between Accounts
This shows the commands for sending between two accounts and checking balances. Note you first need to unlock the account:

    > var from = eth.accounts[0]
    undefined
    > var to   = eth.accounts[1]
    undefined
    > personal.unlockAccount(from)
    Unlock account 0x926cdd37c279f38e941bde52003f865859aabb76
    Passphrase:
    true
    > eth.sendTransaction({from:from, to:to, value: web3.toWei(1, "ether")})
    "0x4c169af406aed32d5b072c2ee2ac246a22b650c68aa29b1b7ff0dfd2b7f56813"
    > web3.fromWei(eth.getBalance(from))
    1.15792
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
These instructions are summarized from [here](https://ethereum.stackexchange.com/a/15436/8317) and [here](https://ethereum.stackexchange.com/a/3520/8317).

Create a new file, e.g. Test.sol:

    contract Test {  function double(int a) constant returns(int) { return 2*a; } }

Use a tool like this [Line Break Removal Tool](https://www.textfixer.com/tools/remove-line-breaks.php) to remove newlines.

Compile (in a terminal session, not geth console):

    $ echo "var testOutput=`solc --optimize --combined-json abi,bin,interface Test.sol`" > test.js

Check what's in test.js:

    $ cat test.js
    var testOutput={"contracts":{"Test.sol:test":{"abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"multiply\",\"outputs\":[{\"name\":\"d\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"}]","bin":"60606040523415600e57600080fd5b609a8061001c6000396000f300606060405260043610603e5763ffffffff7c0100000000000000000000000000000000000000000000000000000000600035041663c6888fa181146043575b600080fd5b3415604d57600080fd5b60566004356068565b60405190815260200160405180910390f35b600702905600a165627a7a72305820b9bacfe234b71a880cdb653740e531bdd55f588943fb54de22a2b4ce0a3c08ea0029"}},"version":"0.4.19+commit.c4cbbb05.Linux.g++"}

Load the file in the geth console:

    > loadScript("test.js");
    true

Check the content of `testOutput`:

    > testOutput
    {
      contracts: {
        Test.sol:Test: {
          abi: "[{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"int256\"}],\"name\":\"double\",\"outputs\":[{\"name\":\"\",\"type\":\"int256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]",
          bin: "60606040523415600e57600080fd5b609a8061001c6000396000f300606060405260043610603e5763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416636ffa1caa81146043575b600080fd5b3415604d57600080fd5b60566004356068565b60405190815260200160405180910390f35b600202905600a165627a7a72305820ad7e119166a4fd50657c9ebf64b81136cd76e83e22460b6c24dfa0c0a4e5e8ee0029"
        }
      },
      version: "0.4.19+commit.c4cbbb05.Linux.g++"
    }

Create a contract with the content of `testOutput`:

    > var testContract = web3.eth.contract(JSON.parse(testOutput.contracts["Test.sol:Test"].abi));
    undefined
    > var test = testContract.new({ from: eth.accounts[0], data: "0x" +     testOutput.contracts["Test.sol:Test"].bin, gas: 4700000},
    function (e, contract) {
     console.log(e, contract);
     if (typeof contract.address !== 'undefined') {
          console.log('Contract mined! address: ' + contract.address + ' transactionHash: ' + contract.transactionHash);
         }
       }
    );
    > null [object Object]
    Contract mined! address: 0xabae73839a51b8dc54466a9f5fa9f600f0067108 transactionHash: 0x211bc0086424d5f3f646b17f18393ac806ee96523f5be1b8d3ebf4d957562652

Save the address if you want to later be able to run this contract from outside your geth session.

You should now be able to call the `double` function from within the geth session:

    > test.double(5)
    10

## Use web3.py To Interact with Geth from Python
Assuming geth is running on `localhost:8545`, use [web3.py](https://github.com/ethereum/web3.py) to get some basic information from outside the geth console.

Note that in order to access some of the API methods, you need to specify an additional parameter to geth on startup:  `--rpcapi="db,eth,net,web3,personal,web3"`.

Without this, you may see an error like `method personal_listAccounts does not exist/is not available`.

    pip install web3

    from web3 import Web3, HTTPProvider
    web3 = Web3(HTTPProvider('http://localhost:8545'))
    print(web3.eth.blockNumber)
    print(web3.eth.coinbase)
    print(web3.personal.listAccounts)



## Connect to a Local Development Environment With Remix

    geth --mine --minerthreads 1 --dev --datadir "~/.ethereum-dev" --unlock 0 --rpc --rpcport "8545"  --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --rpccorsdomain "http://remix.ethereum.org" console 2>> ~/.ethereum-dev.log

- Go to [http://remix.ethereum.org](http://remix.ethereum.org)
- On the 'Run' tab in top right, change the Environment to Web3 Provider
- Enter 'http://localhost:8545' as the Web3 Provider Endpoint