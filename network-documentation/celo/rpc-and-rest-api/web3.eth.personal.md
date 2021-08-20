---
description: Learn how to interact with the web3.eth.personal package
---

# Web3.eth.personal

## Source documentation

[**The web3.eth.personal package's source documentation can be found here**](https://web3js.readthedocs.io/en/v1.3.0/web3-eth-personal.html).

## web3.eth.personal

The `web3-eth-personal` package allows you to interact with the Ethereum node’s accounts.

**Note**

Many of these functions send sensitive information like passwords. Never call these functions over a unsecured Websocket or HTTP provider, as your password will be sent in plain text!

```javascript
var Personal = require('web3-eth-personal');

// "Personal.providers.givenProvider" will be set if in an Ethereum supported browser.
var personal = new Personal(Personal.givenProvider || 'ws://some.local-or-remote.node:8546');


// or using the web3 umbrella package

var Web3 = require('web3');
var web3 = new Web3(Web3.givenProvider || 'ws://some.local-or-remote.node:8546');

// -> web3.eth.personal
```

### `setProvider`

```javascript
web3.setProvider(myProvider)
web3.eth.setProvider(myProvider)
web3.shh.setProvider(myProvider)
web3.bzz.setProvider(myProvider)
...
```

Will change the provider for its module.

**Note**

When called on the umbrella package `web3` it will also set the provider for all sub modules `web3.eth`, `web3.shh`, etc. EXCEPT `web3.bzz` which needs a separate provider at all times.

#### Parameters

1. `Object` - `myProvider`: a valid provider.

#### Returns

`Boolean`

#### Example

```javascript
var Web3 = require('web3');
var web3 = new Web3('http://localhost:8545');
// or
var web3 = new Web3(new Web3.providers.HttpProvider('http://localhost:8545'));

// change provider
web3.setProvider('ws://localhost:8546');
// or
web3.setProvider(new Web3.providers.WebsocketProvider('ws://localhost:8546'));

// Using the IPC provider in node.js
var net = require('net');
var web3 = new Web3('/Users/myuser/Library/Ethereum/geth.ipc', net); // mac os path
// or
var web3 = new Web3(new Web3.providers.IpcProvider('/Users/myuser/Library/Ethereum/geth.ipc', net)); // mac os path
// on windows the path is: "\\\\.\\pipe\\geth.ipc"
// on linux the path is: "/users/myuser/.ethereum/geth.ipc"
```

### `providers`

```javascript
web3.providers
web3.eth.providers
web3.shh.providers
web3.bzz.providers
...
```

Contains the current available providers.

#### Value

`Object` with the following providers:

> * `Object` - `HttpProvider`: The HTTP provider is **deprecated**, as it won’t work for subscriptions.
> * `Object` - `WebsocketProvider`: The Websocket provider is the standard for usage in legacy browsers.
> * `Object` - `IpcProvider`: The IPC provider is used node.js dapps when running a local node. Gives the most secure connection.

#### Example

```javascript
var Web3 = require('web3');
// use the given Provider, e.g in Mist, or instantiate a new websocket provider
var web3 = new Web3(Web3.givenProvider || 'ws://remotenode.com:8546');
// or
var web3 = new Web3(Web3.givenProvider || new Web3.providers.WebsocketProvider('ws://remotenode.com:8546'));

// Using the IPC provider in node.js
var net = require('net');

var web3 = new Web3('/Users/myuser/Library/Ethereum/geth.ipc', net); // mac os path
// or
var web3 = new Web3(new Web3.providers.IpcProvider('/Users/myuser/Library/Ethereum/geth.ipc', net)); // mac os path
// on windows the path is: "\\\\.\\pipe\\geth.ipc"
// on linux the path is: "/users/myuser/.ethereum/geth.ipc"
```

#### Configuration

```javascript
// ====
// Http
// ====

var Web3HttpProvider = require('web3-providers-http');

var options = {
    keepAlive: true,
    withCredentials: false,
    timeout: 20000, // ms
    headers: [
        {
            name: 'Access-Control-Allow-Origin',
            value: '*'
        },
        {
            ...
        }
    ],
    agent: {
        http: http.Agent(...),
        baseUrl: ''
    }
};

var provider = new Web3HttpProvider('http://localhost:8545', options);

// ==========
// Websockets
// ==========

var Web3WsProvider = require('web3-providers-ws');

var options = {
    timeout: 30000, // ms

    // Useful for credentialed urls, e.g: ws://username:password@localhost:8546
    headers: {
      authorization: 'Basic username:password'
    },

    clientConfig: {
      // Useful if requests are large
      maxReceivedFrameSize: 100000000,   // bytes - default: 1MiB
      maxReceivedMessageSize: 100000000, // bytes - default: 8MiB

      // Useful to keep a connection alive
      keepalive: true,
      keepaliveInterval: 60000 // ms
    },

    // Enable auto reconnection
    reconnect: {
        auto: true,
        delay: 5000, // ms
        maxAttempts: 5,
        onTimeout: false
    }
};

var ws = new Web3WsProvider('ws://localhost:8546', options);
```

More information for the Http and Websocket provider modules can be found here:

> * [HttpProvider](https://github.com/ethereum/web3.js/tree/1.x/packages/web3-providers-http#usage)
> * [WebsocketProvider](https://github.com/ethereum/web3.js/tree/1.x/packages/web3-providers-ws#usage)

### `givenProvider`

```javascript
web3.givenProvider
web3.eth.givenProvider
web3.shh.givenProvider
web3.bzz.givenProvider
...
```

When using web3.js in an Ethereum compatible browser, it will set with the current native provider by that browser. Will return the given provider by the \(browser\) environment, otherwise `null`.

#### Returns

`Object`: The given provider set or `null`;

#### Example

### `currentProvider`

```javascript
web3.currentProvider
web3.eth.currentProvider
web3.shh.currentProvider
web3.bzz.currentProvider
...
```

Will return the current provider, otherwise `null`.

#### Returns

`Object`: The current provider set or `null`.

#### Example

### `BatchRequest`

```javascript
new web3.BatchRequest()
new web3.eth.BatchRequest()
new web3.shh.BatchRequest()
new web3.bzz.BatchRequest()
```

Class to create and execute batch requests.

#### Parameters

none

#### Returns

`Object`: With the following methods:

> * `add(request)`: To add a request object to the batch call.
> * `execute()`: Will execute the batch request.

#### Example

```javascript
var contract = new web3.eth.Contract(abi, address);

var batch = new web3.BatchRequest();
batch.add(web3.eth.getBalance.request('0x0000000000000000000000000000000000000000', 'latest', callback));
batch.add(contract.methods.balance(address).call.request({from: '0x0000000000000000000000000000000000000000'}, callback2));
batch.execute();
```

### `extend`

```javascript
web3.extend(methods)
web3.eth.extend(methods)
web3.shh.extend(methods)
web3.bzz.extend(methods)
...
```

Allows extending the web3 modules.

**Note**

You also have `*.extend.formatters` as additional formatter functions to be used for input and output formatting. Please see the [source file](https://github.com/ethereum/web3.js/blob/1.x/packages/web3-core-helpers/src/formatters.js) for function details.

#### Parameters

1. `methods` - `Object`: Extension object with array of methods description objects as follows:
   * `property` - `String`: \(optional\) The name of the property to add to the module. If no property is set it will be added to the module directly.
   * `methods` - `Array`: The array of method descriptions:
     * `name` - `String`: Name of the method to add.
     * `call` - `String`: The RPC method name.
     * `params` - `Number`: \(optional\) The number of parameters for that function. Default 0.
     * `inputFormatter` - `Array`: \(optional\) Array of inputformatter functions. Each array item responds to a function parameter, so if you want some parameters not to be formatted, add a `null` instead.
     * ```outputFormatter - ``Function```: \(optional\) Can be used to format the output of the method.

#### Returns

`Object`: The extended module.

#### Example

```javascript
web3.extend({
    property: 'myModule',
    methods: [{
        name: 'getBalance',
        call: 'eth_getBalance',
        params: 2,
        inputFormatter: [web3.extend.formatters.inputAddressFormatter, web3.extend.formatters.inputDefaultBlockNumberFormatter],
        outputFormatter: web3.utils.hexToNumberString
    },{
        name: 'getGasPriceSuperFunction',
        call: 'eth_gasPriceSuper',
        params: 2,
        inputFormatter: [null, web3.utils.numberToHex]
    }]
});

web3.extend({
    methods: [{
        name: 'directCall',
        call: 'eth_callForFun',
    }]
});

console.log(web3);
> Web3 {
    myModule: {
        getBalance: function(){},
        getGasPriceSuperFunction: function(){}
    },
    directCall: function(){},
    eth: Eth {...},
    bzz: Bzz {...},
    ...
}
```

### `newAccount`

```javascript
web3.eth.personal.newAccount(password, [callback])
```

Creates a new account.

**Note**

Never call this function over a unsecured Websocket or HTTP provider, as your password will be sent in plain text!

#### Parameters

1. `password` - `String`: The password to encrypt this account with.

#### Returns

`Promise` returns `String`: The address of the newly created account.

#### Example

```javascript
web3.eth.personal.newAccount('!@superpassword')
.then(console.log);
> '0x1234567891011121314151617181920212223456'
```

### `sign`

```javascript
web3.eth.personal.sign(dataToSign, address, password [, callback])
```

The sign method calculates an Ethereum specific signature with:

```javascript
sign(keccak256("\x19Ethereum Signed Message:\n" + dataToSign.length + dataToSign)))
```

Adding a prefix to the message makes the calculated signature recognisable as an Ethereum specific signature.

If you have the original message and the signed message, you can discover the signing account address using web3.eth.personal.ecRecover. See example below.

**Note**

Sending your account password over an unsecured HTTP RPC connection is highly unsecure.

#### Parameters

1. `String` - Data to sign. If String it will be converted using [web3.utils.utf8ToHex](https://web3js.readthedocs.io/en/v1.3.0/web3-utils.html#utils-utf8tohex).
2. `String` - Address to sign data with.
3. `String` - The password of the account to sign data with.
4. `Function` - \(optional\) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String` - The signature.

#### Example

```javascript
web3.eth.personal.sign("Hello world", "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "test password!")
.then(console.log);
> "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400"

// the below is the same
web3.eth.personal.sign(web3.utils.utf8ToHex("Hello world"), "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "test password!")
.then(console.log);
> "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400"

// recover the signing account address using original message and signed message
web3.eth.personal.ecRecover("Hello world", "0x30755ed65396...etc...")
.then(console.log);
> "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe"
```

### `ecRecover`

```javascript
web3.eth.personal.ecRecover(dataThatWasSigned, signature [, callback])
```

Recovers the account that signed the data.

#### Parameters

1. `String` - Data that was signed. If String it will be converted using [web3.utils.utf8ToHex](https://web3js.readthedocs.io/en/v1.3.0/web3-utils.html#utils-utf8tohex).
2. `String` - The signature.
3. `Function` - \(optional\) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String` - The account.

#### Example

```javascript
web3.eth.personal.ecRecover("Hello world", "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400").then(console.log);
> "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe"
```

### `signTransaction`

```javascript
web3.eth.personal.signTransaction(transaction, password [, callback])
```

Signs a transaction. This account needs to be unlocked.

**Note**

Sending your account password over an unsecured HTTP RPC connection is highly unsecure.

#### Parameters

1. `Object` - The transaction data to sign [web3.eth.sendTransaction\(\)](https://web3js.readthedocs.io/en/v1.3.0/web3-eth.html#eth-sendtransaction) for more.
2. `String` - The password of the `from` account, to sign the transaction with.
3. `Function` - \(optional\) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - The RLP encoded transaction. The `raw` property can be used to send the transaction using [web3.eth.sendSignedTransaction](https://web3js.readthedocs.io/en/v1.3.0/web3-eth.html#eth-sendsignedtransaction).

#### Example

```javascript
web3.eth.signTransaction({
    from: "0xEB014f8c8B418Db6b45774c326A0E64C78914dC0",
    gasPrice: "20000000000",
    gas: "21000",
    to: '0x3535353535353535353535353535353535353535',
    value: "1000000000000000000",
    data: ""
}, 'MyPassword!').then(console.log);
> {
    raw: '0xf86c808504a817c800825208943535353535353535353535353535353535353535880de0b6b3a76400008025a04f4c17305743700648bc4f6cd3038ec6f6af0df73e31757007b7f59df7bee88da07e1941b264348e80c78c4027afc65a87b0a5e43e86742b8ca0823584c6788fd0',
    tx: {
        nonce: '0x0',
        gasPrice: '0x4a817c800',
        gas: '0x5208',
        to: '0x3535353535353535353535353535353535353535',
        value: '0xde0b6b3a7640000',
        input: '0x',
        v: '0x25',
        r: '0x4f4c17305743700648bc4f6cd3038ec6f6af0df73e31757007b7f59df7bee88d',
        s: '0x7e1941b264348e80c78c4027afc65a87b0a5e43e86742b8ca0823584c6788fd0',
        hash: '0xda3be87732110de6c1354c83770aae630ede9ac308d9f7b399ecfba23d923384'
    }
}
```

### `sendTransaction`

```javascript
web3.eth.personal.sendTransaction(transactionOptions, password [, callback])
```

This method sends a transaction over the management API.

**Note**

Sending your account password over an unsecured HTTP RPC connection is highly unsecure.

#### Parameters

1. `Object` - The transaction options
2. `String` - The passphrase for the current account
3. `Function` - \(optional\) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise<string>` - The transaction hash.

#### Example

```javascript
web3.eth.sendTransaction({
    from: "0xEB014f8c8B418Db6b45774c326A0E64C78914dC0",
    gasPrice: "20000000000",
    gas: "21000",
    to: '0x3535353535353535353535353535353535353535',
    value: "1000000000000000000",
    data: ""
}, 'MyPassword!').then(console.log);
> '0xda3be87732110de6c1354c83770aae630ede9ac308d9f7b399ecfba23d923384'
```

### `unlockAccount`

```javascript
web3.eth.personal.unlockAccount(address, password, unlockDuraction [, callback])
```

Signs data using a specific account.

**Note**

Sending your account password over an unsecured HTTP RPC connection is highly unsecure.

#### Parameters

1. `address` - `String`: The account address.
2. `password` - `String` - The password of the account.
3. `unlockDuration` - `Number` - The duration for the account to remain unlocked.

#### Example

```javascript
web3.eth.personal.unlockAccount("0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "test password!", 600)
.then(console.log('Account unlocked!'));
> "Account unlocked!"
```

### `lockAccount`

```javascript
web3.eth.personal.lockAccount(address [, callback])
```

Locks the given account.

**Note**

Sending your account password over an unsecured HTTP RPC connection is highly unsecure.

#### Parameters

1. `address` - `String`: The account address. 4. `Function` - \(optional\) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise<boolean>`

#### Example

```javascript
web3.eth.personal.lockAccount("0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe")
.then(console.log('Account locked!'));
> "Account locked!"
```

### `getAccounts`

```javascript
web3.eth.personal.getAccounts([callback])
```

Returns a list of accounts the node controls by using the provider and calling the RPC method `personal_listAccounts`. Using [web3.eth.accounts.create\(\)](https://web3js.readthedocs.io/en/v1.3.0/web3-eth-accounts.html#accounts-create) will not add accounts into this list. For that use web3.eth.personal.newAccount\(\).

The results are the same as web3.eth.getAccounts\(\) except that calls the RPC method `eth_accounts`.

#### Returns

`Promise<Array>` - An array of addresses controlled by node.

#### Example

```javascript
web3.eth.personal.getAccounts()
.then(console.log);
> ["0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "0xDCc6960376d6C6dEa93647383FfB245CfCed97Cf"]
```

### `importRawKey`

```javascript
web3.eth.personal.importRawKey(privateKey, password)
```

Imports the given private key into the key store, encrypting it with the passphrase.

Returns the address of the new account.

**Note**

Sending your account password over an unsecured HTTP RPC connection is highly unsecure.

#### Parameters

1. `privateKey` - `String` - An unencrypted private key \(hex string\).
2. `password` - `String` - The password of the account.

#### Returns

`Promise<string>` - The address of the account.

#### Example

```javascript
web3.eth.personal.importRawKey("cd3376bb711cb332ee3fb2ca04c6a8b9f70c316fcdf7a1f44ef4c7999483295e", "password1234")
.then(console.log);
> "0x8f337bf484b2fc75e4b0436645dcc226ee2ac531"
```

