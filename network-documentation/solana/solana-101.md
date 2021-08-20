---
description: Learn how Solana works and what makes it special
---

# ✏ Solana 101

## **What is Solana?**

Solana is an open-source project implementing a new, high-performance, permissionless blockchain. From [Messari's Solana profile](https://messari.io/asset/solana/profile), its goal is to provide a platform that enables developers to create DApps without needing to design around performance bottlenecks. Solana features a new timestamp system called Proof-of-History \(PoH\) that enables automatically ordered transactions. It also uses a Proof of Stake \(PoS\) consensus algorithm to help secure the network. Additional design goals include sub-second settlement times, low transaction costs, and support for all LLVM compatible smart contract languages.

### **Why build on Solana?**

Solana ensures composability between ecosystem projects by maintaining a single global state as the network scales. Solana’s blazing speed and low fees scale as the ecosystem grows without sacrificing censorship resistance or security.

Here are the advantages of the Solana network:

1. **Code in your language:** Solana programs can be written in Rust, C or C++ and clients can use the Javascript or Rust SDKs \(written by Solana\) or the Python, Java or C\# \(written by the community\). And you always have the option to use the JSON RPC API if your native language isn’t supported!
2. **Avoid long wait times for your users:** Blazing fast speeds and no mempool. 400ms blocktimes and sub-second finality. Web 3.0 with Web 2.0 speed.
3. **Capital efficient as the ecosystem grows:** Solana scales thanks to Moore’s Law — there's no need to integrate with multiple shards or layer 2 solutions.
4. **Enterprise-grade security:** Audited by a Fortune 500-preferred security firm. Iron-clad immutability for global scale.

### **What can you build on Solana?**

Solana offers a highly scalable platform for Web 3 applications which can now unlock mainstream usage. There are already over 150 projects live on Solana, with a majority of DeFi projects, although NFTs, social apps, and games are starting to launch on the network.

## **Network Specifications**

### **Transaction Fees**

The network Cluster sets transaction fees based on recent processing history. Transactions currently include a fee field that indicates the maximum fee field a slot leader can charge for processing a transaction.  
Transaction fees on Solana are estimated at $10 for 1 million transactions.

### **Transaction Speed & Finality**

Solana’s built-in mechanism for synchronizing time across nodes helps the network support a theoretical peak capacity of 65,000 transactions per second and block times at 400ms. This makes Solana one of the fastest production blockchain available, and 4,000 times faster than Ethereum.

### **Languages supported**

Solana applications are built on Rust, but also support C and C++.

### **EVM compatibility**

Solana is not EVM compatible but it offers [a bidirectional token bridge](https://solana.com/wormhole) between Solana and Ethereum so projects can move tokenized assets across blockchains.

### **Role of the SOL token**

There are two primary uses of the SOL token:

1. The token is used to pay for the transaction fees in the network
2. The token is used for staking to participate in the Proof of Stake consensus 

