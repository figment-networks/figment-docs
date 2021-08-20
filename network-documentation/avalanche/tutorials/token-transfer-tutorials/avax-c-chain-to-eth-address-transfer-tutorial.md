---
description: >-
  Learn how to Transfer AVAX native tokens from Avalanche C-Chain to an Ethereum
  address
---

# Transfer AVAX tokens from the C-Chain to an ETH address

## Introduction

In this tutorial, we are going to learn how to programatically transfer native AVAX tokens from the Avalanche C-Chain to an ETH wallet.

## Transfer AVAX 

We need to import the appropriate libraries \(web3 and ethers\). So, let's begin by installing them first. Both web3.js and ethers.js are Ethereum Javascript APIs designed to help interact with the Ethereum blockchain. The C-Chain of Avalanche shares the same libraries. This allows Ethereum developers to migrate over to Avalanche with minimal effort.

We will install the ethers.js library by entering the following line into the terminal

```bash
$ npm install ethers web3
```

After installing the dependencies, we need to import them in order to use their functionality to interact with the Avalanche C-Chain:

```javascript
const Web3 = require("web3")
const { ethers } = require('ethers')
```

The mnemonic key from your AVAX wallet needs to go between the quotation marks below. This is later used to extract the C-Chain wallet address.

```javascript
let mnemonic = "";
```

This code below is pointing to the Fuji network. Alternatively, we can point it to the Datahub AVAX node.

```javascript
const web3 = new Web3(new Web3.providers.HttpProvider("https://api.avax-test.network/ext/bc/C/rpc"))
```

The private key is needed to execute a transfer later on. With the mnemonic phrase provided earlier, we can obtain the private key to your AVAX wallet in the ETH address format.

```javascript
const wallet = new ethers.Wallet.fromMnemonic(mnemonic);
AVAX_privatekey = wallet.privateKey;
```

The web3 package is designed to interact with an Ethereum blockchain and Ethereum smart contracts. The web3 module is capable of acting upon the AVAX implementation of the EVM. So, when interacting with the C chain, the web3 module is used. Here, `web3.eth.getBalance` fetches the AVAX balance. `result` in `web3.utils.fromWei` below is the balance of the account in the units of wei \(the minimum unit of Ether is called wei and 1 Ether is 10^18 wei\). `fromWei` is a method in web3.utils, converting a number from one unit to another. So, `web3.utils.fromWei(result, "ether")` in the code below converts the balance from wei to ether. Since we are viewing the AVAX token balance, we will print AVAX at the end.

```javascript
async function main(){
    web3.eth.getBalance(wallet.address, function(err, result) {    
        if (err) {
          console.log(err)
        } else {
          console.log(web3.utils.fromWei(result, "ether") + " AVAX")
        }
    })
```

The block below is to view the \# of transactions associated with the wallet address \(not necessary for the purpose of AVAX transfer from C chain to an ETH address\) but could be useful when you later want to transfer an ERC20 token.

```javascript
    web3.eth.getTransactionCount(wallet.address)       
    .then(console.log);                                               
    const createTransaction = await web3.eth.accounts.signTransaction(           
        {
           gas: 21000,
```

Copy and paste your ETH destination address beween the quotation marks below

```javascript
           to:"",
```

Below, we need to input how many tokens are to be transferred out of your AVAX wallet off the C chain. Currently the amount is arbitrarily set to 0.15 AVAX tokens as an example \(0.15 tokens in the line below\).

```javascript
           value: web3.utils.toWei('0.15', 'ether'),     
        },
        AVAX_privatekey                                 
     );
     const createReceipt = await web3.eth.sendSignedTransaction(
        createTransaction.rawTransaction
     );
     console.log(
        `Transaction successful with hash: ${createReceipt.transactionHash}`
     );
  };
main().catch((err) => {
    console.log("We have encountered an error!")
    console.error(err)
})
```

## Wrapping Up

That’s it! This tutorial has taught you how to transfer AVAX native tokens from the C chain to an ETH wallet. Also, this has shown how Avalanche blockchain C chain is compatible with the usual web3 library. This is a powerful aspect of the Avalanche blockchain, as it allows Ethereum developers to easily port their work over to the Avalanche side.

Try transferring your Fuji AVAX tokens by running this script and see if it worked.

## About the author

This tutorial was created by [Seongwoo Oh](https://github.com/blackwidoq). He is a student and an Avalanche novice.

