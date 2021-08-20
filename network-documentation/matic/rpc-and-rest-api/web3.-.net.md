---
description: Learn how to interact with the web3.*.net package
---

# Web3.\*.net

## Source documentation

[**The web3.\*.net package's source documentation can be found here**](https://web3js.readthedocs.io/en/v1.3.0/web3-net.html).

## web3.\*.net

The `web3-net` package allows you to interact with an Ethereum node’s network properties.

```javascript
var Net = require('web3-net');

// "Personal.providers.givenProvider" will be set if in an Ethereum supported browser.
var net = new Net(Net.givenProvider || 'ws://some.local-or-remote.node:8546');


// or using the web3 umbrella package

var Web3 = require('web3');
var web3 = new Web3(Web3.givenProvider || 'ws://some.local-or-remote.node:8546');

// -> web3.eth.net
// -> web3.bzz.net
// -> web3.shh.net
```

### `getId`

```javascript
web3.eth.net.getId([callback])
web3.bzz.net.getId([callback])
web3.shh.net.getId([callback])
```

Gets the current network ID.

#### Parameters

none

#### Returns

`Promise` returns `Number`: The network ID.

#### Example

```javascript
web3.eth.net.getId()
.then(console.log);
> 1
```

### `isListening`

```javascript
web3.eth.net.isListening([callback])
web3.bzz.net.isListening([callback])
web3.shh.net.isListening([callback])
```

Checks if the node is listening for peers.

#### Parameters

none

#### Returns

`Promise` returns `Boolean`

#### Example

```javascript
web3.eth.net.isListening()
.then(console.log);
> true
```

### `getPeerCount`

```javascript
web3.eth.net.getPeerCount([callback])
web3.bzz.net.getPeerCount([callback])
web3.shh.net.getPeerCount([callback])
```

Get the number of peers connected to.

#### Parameters

none

#### Returns

`Promise` returns `Number`

#### Example

```javascript
web3.eth.net.getPeerCount()
.then(console.log);
> 25
```

