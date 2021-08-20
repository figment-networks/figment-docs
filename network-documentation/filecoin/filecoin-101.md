---
description: Learn how Filecoin works and what makes it special
---

# ✏️ Filecoin 101

## **What is Filecoin?**

Filecoin is a peer-to-peer network that stores files, with built-in economic incentives to ensure files are stored reliably over time.

In Filecoin, users pay to store their files on storage miners. Storage miners are computers responsible for storing files and proving they have stored the files correctly over time. Anyone who wants to store their files or get paid for storing other users’ files can join Filecoin. Available storage, and the price of that storage, is not controlled by any single company. Instead, Filecoin facilitates open markets for storing and retrieving files that anyone can participate in.

Filecoin includes a blockchain and native cryptocurrency \(FIL\). Storage miners earn units of FIL for storing files. Filecoin’s blockchain records transactions to send and receive FIL, along with proofs from storage miners that they are storing their files correctly.

### **Why build on Filecoin?**

This is an overview of features offered by Filecoin that make it a compelling system for storing files. This overview is intended for people already involved in large-scale data storage, for example, cloud storage or peer-to-peer storage networks.

#### Reliable storage <a id="reliable-storage"></a>

Because storage is paid for, Filecoin provides a viable economic reason for files to stay available over time. Files are stored on computers that are reliable and well-connected to the internet.

#### Self-healing <a id="self-healing"></a>

The Filecoin network continually verifies that files are stored correctly. The Filecoin blockchain has a built-in self-healing process where faulty miners are detected, and their files are redistributed to reliable miners.

#### Verifiable traces <a id="verifiable-traces"></a>

In the process of self-healing, Filecoin generates verifiable traces that files have been stored correctly over time. Clients can efficiently scan these traces to confirm that their files have been stored correctly, even if the client was offline at the time. Any observer can check any miner’s track record and will notice if the miner has been faulty or offline in the past.

#### Reputation, not marketing <a id="reputation-not-marketing"></a>

In Filecoin, storage providers prove their reliability through their track record published on the blockchain, not through marketing claims published by the providers themselves. Users don’t need to rely on status pages or self-reported statistics from storage providers

#### Choice of tradeoffs <a id="choice-of-tradeoffs"></a>

Users get to choose their own tradeoffs between cost, redundancy, and speed. Users are not limited to a set group of data centers offered by their provider but can choose to store their files on any miner participating in Filecoin.

#### Censorship resistance <a id="censorship-resistance"></a>

Filecoin resists censorship because no central provider can be coerced into deleting files or withholding service. The network is made up of many different computers run by many different people and organizations. Faulty or malicious actors are noticed by the network and removed automatically.

#### Provides storage to other blockchains <a id="provides-storage-to-other-blockchains"></a>

Filecoin’s blockchain is designed to store large files, whereas other blockchains can typically only store tiny amounts of data, very expensively. Filecoin can provide storage to other blockchains, allowing them to store large files. In the future, mechanisms will be added to Filecoin, enabling Filecoin’s blockchain to interoperate with transactions on other blockchains.

#### Single protocol <a id="single-protocol"></a>

Applications implementing Filecoin can store their data on any miner using the same protocol. There isn’t a different API to implement for each provider. Applications wishing to support several different providers aren’t limited to the lowest-common-denominator set of features supported by all their providers.

#### No lock-in <a id="no-lock-in"></a>

Migrating to a different storage provider is made easier because they all offer the same services and APIs. Users aren’t locked into providers because they rely on a particular feature of the provider. Also, files are content-addressed, enabling them to be transferred directly between miners without the user having to download and re-upload the files.

Traditional cloud storage providers lock users by making it cheap to store files but expensive to retrieve them again. Filecoin avoids this by facilitating a retrieval market where miners compete to give users their files back as fast as possible, at the lowest possible price.

### **What can you build on Filecoin?**

Filecoin is a protocol that provides core primitives, enabling a truly trustless decentralized storage network. These primitives and features include publicly verifiable cryptographic storage proofs, [crypto-economic mechanisms \(opens new window\)](https://filecoin.io/blog/filecoin-cryptoeconomic-constructions/), and a public blockchain. Filecoin provides these primitives to solve the really hard problem of creating a trustless decentralized storage network.

On top of the core Filecoin protocol, there are a number of layer 2 solutions that enable a broad array of use cases and applications, many of which also use [IPFS \(opens new window\)](https://ipfs.io/). These solutions include [Powergate \(opens new window\)](https://docs.textile.io/powergate/), [Textile Hub \(opens new window\)](https://blog.textile.io/announcing-the-textile-protocol-hub/), and more. Using these solutions, any use case that can be built on top of IPFS can also be built on Filecoin!

Some of the primary areas for development expected on Filecoin around mainnet launch are:

* Additional developer tools and layer-2 solutions and libraries that strengthen Filecoin as a developer platform and ecosystem.
* IPFS apps that rely on decentralized storage solutions and want a decentralized data persistence solution as well.
* Financial tools and services on Filecoin, like wallets, signing libraries, and more.
* Applications that use Filecoin's publicly verifiable cryptographic proofs in order to provide trustless and timestamped guarantees of storage to their users

## **Network Specifications**

### **Transaction Fees**

As Filecoin is a free market, the price will be determined by a number of variables related to the supply and demand for storage. It's difficult to predict before launch. However, a few design elements of the network help support inexpensive storage.

Along with revenue from active storage deals, Storage Miners receive block rewards, where the expected value of winning a given block reward is proportional to the amount of storage they have on the network. These block rewards are weighted heavily towards the early days of the network \(with the frequency of block rewards exponentially decaying over time\). As a result, Storage Miners are relatively incentivized to charge less for storage to win more deals, which would increase their expected block reward.

### **Transaction Speed & Finality**

**Financial transfers**

A message that requires [transferring FIL](https://docs.filecoin.io/get-started/lotus/send-and-receive-fil/#sending-fil) is often extremely fast, and will take on average ~1 blocktime \(or around 30 seconds\) to be reflected on chain. We consider 120 blocks \(1 hour\) a conservative number of confirmations for high-value transfers.

**Data Storage**

The Filecoin [data storage protocol](https://docs.filecoin.io/store/lotus/store-data/) has a few key components once a deal is proposed and accepted:

1. Funding the storage market actor: This process takes ~1-2 minutes and ensures that both the client and the miner have funds and collateral to pay for the deal.
2. Data transfer: This portion of the deal flow involves the client's node sending the relevant pieces of data to the mining node. The data transfer rate varies widely, depending on the network and disk bandwidths of both the client and the miner. Usually, the network speed between client and miner will be the key determining factor.
3. Deal shows up on-chain: once the data is received by the miner, it will be verified to make sure it matches the deal parameters and the deal with be published on the chain.
4. Sector sealing: Once the deal shows up on-chain, the miner must still complete [generating a Proof-of-Replication and sealing the sector \(opens new window\)](https://spec.filecoin.io/#systems__filecoin_mining__sector__adding_storage). This process is currently estimated to take ~1.5hours for a 32GB sector on a machine that meets these [minimum hardware requirements for mining](https://docs.filecoin.io/mine/hardware-requirements/#general-hardware-requirements).

For most storage clients, the storage performance that matters is the time it takes from deal acceptance to deal appearance on-chain. This is the sum of steps \(1\) to \(3\) above. Based on current high-level benchmarks, these steps are estimated to take around ~5-10 minutes for a 1MiB file.

### **Languages supported**

Both Lotus and IPFS have several implementations for development in different environments, such as Go, JavaScript, Rust, etc.

### **EVM compatibility**

Filecoin \_\*\*\_compatible with the EVM.

### **Role of the FIL token**

Filecoin’s cryptocurrency, FIL, is the native token powering its network. That means FIL is used to pay for storage and retrieval, and for any other transactions on the network.

