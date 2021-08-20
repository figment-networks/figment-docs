---
description: Learn how to interact with the Web3 API
---

# Web3

## Source documentation

[**The Web3 API's source documentation can be found here**](https://web3js.readthedocs.io/en/v1.3.0/web3.html).

## Web3

This is the main \(or ‘umbrella’\) class of the web3.js library.

```javascript
var Web3 = require('web3');

> Web3.utils
> Web3.version
> Web3.givenProvider
> Web3.providers
> Web3.modules
```

### Web3.modules

```javascript
Web3.modules
```

Will return an object with the classes of all major sub modules, to be able to instantiate them manually.

#### Returns

`Object`: A list of module constructors:

* `Eth` - `Constructor`: The Eth module for interacting with the Ethereum network \([web3.eth](https://web3js.readthedocs.io/en/v1.3.0/web3-eth.html#eth)\).
* `Net` - `Constructor`: The Net module for interacting with network properties \([web3.eth.net](https://web3js.readthedocs.io/en/v1.3.0/web3-eth-net.html#eth-net)\).
* `Personal` - `Constructor`: The Personal module for interacting with the Ethereum accounts \(web3.eth.personal\).
* `Shh` - `Constructor`: The Shh module for interacting with the whisper protocol \([web3.shh](https://web3js.readthedocs.io/en/v1.3.0/web3-shh.html#shh)\).
* `Bzz` - `Constructor`: The Bzz module for interacting with the swarm network \([web3.bzz](https://web3js.readthedocs.io/en/v1.3.0/web3-bzz.html#bzz)\).

#### Example

```javascript
Web3.modules
> {
    Eth: Eth(provider),
    Net: Net(provider),
    Personal: Personal(provider),
    Shh: Shh(provider),
    Bzz: Bzz(provider),
}
```

### Web3 Instance

The Web3 class is an umbrella package to house all Ethereum related modules.

```javascript
var Web3 = require('web3');

// "Web3.providers.givenProvider" will be set if in an Ethereum supported browser.
var web3 = new Web3(Web3.givenProvider || 'ws://some.local-or-remote.node:8546');

> web3.eth
> web3.shh
> web3.bzz
> web3.utils
> web3.version
```

### `version`

Static accessible property of the Web3 class and property of the instance as well.

```javascript
Web3.version
web3.version
```

Contains the current package version of the web3.js library.

#### Returns

`String`: The current version.

#### Example

```javascript
web3.version;
> "1.2.3"
```

### `utils`

Static accessible property of the Web3 class and property of the instance as well.

```javascript
Web3.utils
web3.utils
```

Utility functions are also exposes on the `Web3` class object directly.

[See web3.utils for more](https://figment-learn.gitbook.io/learn-docs/network-documentation/celo/rpc-and-rest-api/web3.utils).

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

