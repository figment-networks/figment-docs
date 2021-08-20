---
description: Learn how to call Matic.js methods
---

# Matic.js

\*\*\*\*[**The official documentation for matic.js can be found here.** ](https://github.com/maticnetwork/matic.js#balanceOfERC20)\*\*\*\*

## **Overview**

`maticjs` makes it easy for developers, who may not be deeply familiar with smart contract development, to interact with the various components of Polygon \(Matic\) Network.

This library will help developers to move assets from Ethereum chain to Polygon \(Matic\) chain, and withdraw from Polygon \(Matic\) to Ethereum using fraud proofs.

You can download the library by following [these steps](https://github.com/maticnetwork/matic.js#balanceOfERC20).

## API

### **new Matic\(options\)**

**Description**

Creates Matic SDK instance with give options. It returns a MaticSDK object.

```javascript
import Matic from 'maticjs'

const matic = new Matic(options)
matic.initialize()
```

* `options` is simple Javascript `object` which can have following fields:
  * `network` can be `string`
  * `version` can be `string`
  * `maticProvider` can be `string` or `Web3.providers` instance. This provider must connect to Matic chain. Value can be anyone of following:
    * `network.Matic.RPC`
    * `new Web3.providers.HttpProvider(network.Matic.RPC)`
    * [WalletConnect Provider instance](https://github.com/WalletConnect/walletconnect-monorepo#for-web3-provider-web3js)
  * `parentProvider` can be `string` or `Web3.providers` instance. This provider must connect to Ethereum chain \(testnet or mainchain\). Value can be anyone of following:
    * `network.Main.RPC`
    * `new Web3.providers.HttpProvider(network.Main.RPC)`
    * [WalletConnect Provider instance](https://github.com/WalletConnect/walletconnect-monorepo#for-web3-provider-web3js)
  * `parentDefaultOptions` is simple Javascript `object` with following options
    * `from` must be valid account address\(required\)
  * `maticDefaultOptions` is simple Javascript `object` with following options
    * `from` must be valid account address\(required\)

### **matic.balanceOfERC20\(userAddress, token, options\)**

**Description**

get balance of ERC20 `token` for `address`.

* `token` must be valid token address
* `userAddress` must be valid user address
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `parent` must be boolean value. For balance on Main chain, use `parent: true`

This returns `balance`.

**Example Output:**

```javascript
matic
  .balanceOfERC20('0xABc578455...', '0x5E9c4ccB05...', {
    from: '0xABc578455...',
  })
  .then(balance => {
    console.log('balance', balance)
  })
```

### **matic.balanceOfERC721\(userAddress, token, options\)**

**Description:**

get balance of ERC721 `token` for `address`.

* `token` must be valid token address
* `userAddress` must be valid user address
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `parent` must be boolean value. For balance on Main chain, use `parent: true`

This returns `balance`.

**Example Output:**

```javascript
matic
  .balanceOfERC721('0xABc578455...', '0x5E9c4ccB05...', {
    from: '0xABc578455...',
  })
  .then(balance => {
    console.log('balance', balance)
  })
```

### **matic.tokenOfOwnerByIndexERC721\(userAddress, token, index, options\)**

**Description**

get ERC721 tokenId at `index` for `token` and for `address`.

* `token` must be valid token address
* `userAddress` must be valid user address
* `index` index of tokenId

This returns matic `tokenId`.

**Example Output:**

```javascript
matic
  .tokenOfOwnerByIndexERC721('0xfeb14b...', '21', 0, {
    from: '0xABc578455...',
  })
  .then(tokenID => {
    console.log('Token ID', tokenID)
  })
```

### **matic.depositEthers\(amount, options\)**

**Description**

Deposit `options.value`

* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit).
  * `from` must be valid account address\(required\)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.depositEthers(amount, {
  from: '0xABc578455...',
})
```

### **matic.approveERC20TokensForDeposit\(token, amount, options\)**

**Description:**

Approves given `amount` of `token` to `rootChainContract`.

* `token` must be valid ERC20 token address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` \(optional\) must be valid javascript object containing `from`, `gasPrice`, `gasLimit`, `nonce`, `value`, `onTransactionHash`, `onReceipt` or `onError`
  * `from` must be valid account address\(required\)
  * `gasPrice` same as Ethereum `sendTransaction`
  * `gasLimit` same as Ethereum `sendTransaction`
  * `nonce` same as Ethereum `sendTransaction`
  * `value` contains ETH value. Same as Ethereum `sendTransaction`. This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.approveERC20TokensForDeposit('0x718Ca123...', '1000000000000000000', {
  from: '0xABc578455...',
})
```

### **matic.depositERC20ForUser\(token, user, amount, options\)**

**Description**

Deposit given `amount` of `token` with user `user`.

* `token` must be valid ERC20 token address
* `user` must be value account address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
const user = <your-address> or <any-account-address>

matic.depositToken('0x718Ca123...', user, '1000000000000000000', {
  from: '0xABc578455...'
})
```

### **matic.safeDepositERC721Tokens\(token, tokenId, options\)**

**Description**

Deposit given `TokenID` of `token` with user `user`.

* `token` must be valid ERC20 token address
* `tokenId` must be valid token ID
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.safeDepositERC721Tokens('0x718Ca123...', '70000000000', {
  from: '0xABc578455...',
})
```

### **matic.transferERC20Tokens\(token, user, amount, options\)**

**Description**

Transfer given `amount` of `token` to `user`.

* `token` must be valid ERC20 token address
* `user` must be value account address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `parent` must be boolean value. For token transfer on Main chain, use `parent: true`
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```text
const user = <your-address> or <any-account-address>

matic.transferERC20Tokens('0x718Ca123...', user, '1000000000000000000', {
  from: '0xABc578455...',

  // For token transfer on Main network
  // parent: true
})
```

### **matic.transferERC721Tokens\(token, user, tokenId, options\)**

Transfer given `tokenId` of `token` to `user`.

* `token` must be valid ERC721 token address
* `user` must be value account address
* `tokenId` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `parent` must be boolean value. For token transfer on Main chain, use `parent: true`
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
const user = <your-address> or <any-account-address>

matic.transferERC721Tokens('0x718Ca123...', user, '100006500000000000000', {
  from: '0xABc578455...',

  // For token transfer on Main network
  // parent: true
})
```

### **matic.getTransferSignature\(toSell, toBuy\)**

**Description**

Off-chain signature generation for [transferWithSig](https://github.com/maticnetwork/contracts/blob/a9b77252ece25adcd3f74443411821883bb970e6/contracts/child/BaseERC20.sol#L35) function call

* `toSell` object
  * `token`: address of token owned,
  * `amount`: amount/tokenId of the token to sell,
  * `expiry`: expiry \(block number after which the signature should be invalid\),
  * `orderId`: a random 32 byte hex string,
  * `spender`: the address approved to execute this transaction
* `toBuy` object
  * `token`: address of token to buy
  * `amount`: amount/tokenId of token to buy
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)

  * `from`: owner of the token \(toSell\) 

  **Example Output:**

  ```text
  // sell order
  let toSell = {
    token: token2,
    amount: value2,
    expiry: expire,
    orderId: orderId,
    spender: spender,
  }

  // buy order
  let toBuy = {
    token: token1,
    amount: value1,
  }

  const sig = await matic.getTransferSignature(toSell, toBuy, {
    from: tokenOwner,
  })
  ```

### **matic.transferWithSignature\(sig, toSell, toBuy, orderFiller\)**

**Description**

Executes [transferWithSig](https://github.com/maticnetwork/contracts/blob/a9b77252ece25adcd3f74443411821883bb970e6/contracts/child/BaseERC20.sol#L35) on child token \(erc20/721\). Takes input as signature generated from `matic.getTransferSignature`

* `sig`: signature generated with matic.getTransferSignature
* `toSell`: object
  * `token`: address of token owned,
  * `amount`: amount/tokenId of the token to sell,
  * `expiry`: expiry \(block number after which the signature should be invalid\),
  * `orderId`: a random 32 byte hex string,
  * `spender`: the address approved to execute this transaction
* `toBuy`: object
  * `token`: address of token to buy
  * `amount`: amount/tokenId of token to buy
* `orderFiller`: address of user to transfer the tokens to
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `from`: the approved spender in the `toSell` object by the token owner

transfers `toSell.token` from `tokenOwner` to `orderFiller`

**Example Output:**

```javascript
// sell order
let toSell = {
  token: token2,
  amount: value2,
  expiry: expire,
  orderId: orderId,
  spender: spender,
}

// buy order
let toBuy = {
  token: token1,
  amount: value1,
}

let sig = await matic.getTransferSignature(toSell, toBuy, { from: tokenOwner })

const tx = await matic.transferWithSignature(
  sig, // signature with the intent to buy tokens
  toSell, // sell order
  toBuy, // buy order
  orderFiller, // order fulfiller
  {
    from: spender, // approved spender
  }
)
```

### **matic.startWithdraw\(token, amount, options\)**

**Description**

Start withdraw process with given `amount` for `token`.

* `token` must be valid ERC20 token address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.startWithdraw('0x718Ca123...', '1000000000000000000', {
  from: '0xABc578455...',
})
```

### **matic.startWithdrawForNFT\(token, tokenId, options\)**

**Description**

Start withdraw process with given `tokenId` for `token`.

* `token` must be valid ERC721 token address
* `tokenId` must be token tokenId \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.startWithdrawForNFT('0x718Ca123...', '1000000000000000000', {
  from: '0xABc578455...',
})
```

### **matic.withdraw\(txId, options\)**

**Description**

Withdraw tokens on mainchain using `txId` from `startWithdraw` method after header has been submitted to mainchain.

* `txId` must be valid tx hash
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.withdraw('0xabcd...789', {
  from: '0xABc578455...',
})
```

### **matic.withdrawNFT\(txId, options\)**

**Description**

Withdraw tokens on mainchain using `txId` from `startWithdraw` method after header has been submitted to mainchain.

* `txId` must be valid tx hash
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.withdrawNFT('0xabcd...789', {
  from: '0xABc578455...',
})
```

### **matic.processExits\(rootTokenAddress, options\)**

**Description**

Call processExits after completion of challenge period, after that withdrawn funds get transfered to your account on mainchain

* `rootTokenAddress` RootToken address
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
matic.processExits('0xabcd...789', {
  from: '0xABc578455...',
})
```

## **WithdrawManager**

### **matic.withdrawManager.startExitForMintableBurntToken\(burnTxHash, predicate: address, options\)**

```javascript
/**
  * Start an exit for a token that was minted and burnt on the side chain
  * Wrapper over contract call: MintableERC721Predicate.startExitForMintableBurntToken
  * @param burnTxHash Hash of the burn transaction on Matic
  * @param predicate address of MintableERC721Predicate
  */
```

See [MintableERC721Predicate.startExitForMintableBurntToken](https://github.com/maticnetwork/contracts/blob/e2cb462b8487921463090b0bdcdd7433db14252b/contracts/root/predicates/MintableERC721Predicate.sol#L31)

```javascript
const burn = await this.maticClient.startWithdrawForNFT(childErc721.address, tokenId)
await this.maticClient.withdrawManager.startExitForMintableBurntToken(burn.transactionHash, predicate.address)
```

### **matic.withdrawManager.startExitForMintableBurntToken\(burnTxHash, predicate: address, options\)**

```javascript
/**
  * Start an exit for a token with metadata (token uri) that was minted and burnt on the side chain
  * Wrapper over contract call: MintableERC721Predicate.startExitForMetadataMintableBurntToken
  * @param burnTxHash Hash of the burn transaction on Matic
  * @param predicate address of MintableERC721Predicate
  */
```

See [MintableERC721Predicate.startExitForMetadataMintableBurntToken](https://github.com/maticnetwork/contracts/blob/e2cb462b8487921463090b0bdcdd7433db14252b/contracts/root/predicates/MintableERC721Predicate.sol#L66)

```javascript
const burn = await this.maticClient.startWithdrawForNFT(childErc721.address, tokenId)
await this.maticClient.withdrawManager.startExitForMetadataMintableBurntToken(burn.transactionHash, predicate.address)
```

## **POS Portal**

### **maticPOSClient.approveERC20ForDeposit\(rootToken, amount, options\)**

**Description**

Approves given `amount` of `rootToken` to POS Portal contract.

* `rootToken` must be valid ERC20 token address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
maticPOSClient.approveERC20ForDeposit('0x718Ca123...', '1000000000000000000', {
  from: '0xABc578455...',
})
```

### **maticPOSClient.depositERC20ForUser\(rootToken, user, amount, options\)**

**Description**

Deposit given `amount` of `rootToken` for `user` via POS Portal.

* `rootToken` must be valid ERC20 token address
* `user` must be valid account address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

The given amount must be [approved](https://github.com/maticnetwork/matic.js#pos-approveERC20ForDeposit) for deposit beforehand. This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
const user = <your-address> or <any-account-address>

maticPOSClient.depositERC20ForUser('0x718Ca123...', user, '1000000000000000000', {
  from: '0xABc578455...'
})
```

### **maticPOSClient.depositEtherForUser\(rootToken, user, amount, options\)**

**Description**

Deposit given `amount` of ETH for `user` via POS Portal. ETH is an ERC20 token on Polygon \(Matic\) chain, follow ERC20 [burn](https://github.com/maticnetwork/matic.js#pos-burnERC20) and [exit](https://github.com/maticnetwork/matic.js#pos-exitERC20) to withdraw it.

* `user` must be valid account address
* `amount` must be ETH amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
const user = <your-address> or <any-account-address>

maticPOSClient.depositEtherForUser(user, '1000000000000000000', {
  from: '0xABc578455...'
})
```

### **maticPOSClient.burnERC20\(childToken, amount, options\)**

**Description**

Burn given `amount` of `childToken` to be exited from POS Portal.

* `childToken` must be valid ERC20 token address
* `amount` must be token amount in wei \(string, not in Number\)
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)
  * `encodeAbi` must be boolean value. For Byte code of transaction, use `encodeAbi: true`

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
maticPOSClient.burnERC20('0x718Ca123...', '1000000000000000000', {
  from: '0xABc578455...',
})
```

### **maticPOSClient.exitERC20\(burnTxHash, options\)**

**Description**

Exit tokens from POS Portal. This can be called after checkpoint has been submitted for the block containing burn tx.

* `burnTxHash` must be valid tx hash for token burn using [burnERC20](https://github.com/maticnetwork/matic.js#pos-burnERC20).
* `options` see [more infomation here](https://github.com/maticnetwork/matic.js#approveERC20TokensForDeposit)

This returns `Promise` object, which will be fulfilled when transaction gets confirmed \(when receipt is generated\).

**Example Output:**

```javascript
maticPOSClient.exitERC20('0xabcd...789', {
  from: '0xABc578455...',
})
```

