---
description: Learn more about Avalanche's node information API
---

# Info API

## Source documentation

\*\*\*\*[**The Info API's source documentation can be found here**](https://docs.avax.network/build/apis/info-api).

This API can be used to access basic information about the node.

## Endpoint

```javascript
/ext/info
```

## Methods

### `info.getBlockchainID`

**Description**

Given a blockchain’s alias, get its ID. \(See [`admin.aliasChain`](https://docs.avax.network/build/apis/admin-api) method for more context.\)

**Signature**

```javascript
info.getBlockchainID({alias:string}) -> {blockchainID:string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getBlockchainID",
    "params": {
        "alias":"X"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "blockchainID":"sV6o671RtkGBcno1FiaDbVcFv2sG5aVXMZYzKdP4VQAWmJQnM"
    }
}
```

### `info.getNetworkID`

**Description**

Get the ID of the network this node is participating in.

**Signature**

```javascript
info.getNetworkID() -> {networkID:int}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNetworkID"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "networkID":"2"
    }
}
```

### `info.getNetworkName`

**Description**

Get the name of the network this node is participating in.

**Signature**

```javascript
info.getNetworkName() -> {networkName:string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNetworkName"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "networkName":"local"
    }
}
```

### `info.getNodeID`

**Description**

Get the ID of this node.

**Signature**

```javascript
info.getNodeID() -> {nodeID: string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNodeID"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "nodeID": "NodeID-5mb46qkSBj81k9g9e4VFjGGSbaaSLFRzD"
    },
    "id": 1
}
```

### `info.getNodeVersion`

**Description**

Get the version of this node.

**Signature**

```javascript
info.getNodeVersion() -> {version: string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNodeVersion"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "version": "avalanche/0.5.7"
    },
    "id": 1
}
```

### `info.isBootstrapped`

**Description**

Check whether a given chain is done bootstrapping

**Signature**

```javascript
info.isBootstrapped(chain: string) -> {isBootstrapped: bool}
```

* `chain` is the ID or alias of a chain.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.isBootstrapped",
    "params": {
        "chain":"X"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "isBootstrapped": true
    },
    "id": 1
}
```

### `info.peers`

**Description**

Get description of peer connections.

**Signature**

```javascript
info.peers() -> {peers:[]{
    ip: string,
    publicIP: string,
    nodeID: string,
    version: string,
    lastSent: string,
    lastRecevied: string
}}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.peers"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "peers":[
          {
             "ip":"206.189.137.87:9651",
             "publicIP":"206.189.137.87:9651",
             "nodeID":"NodeID-8PYXX47kqLDe2wD4oPbvRRchcnSzMA4J4",
             "version":"avalanche/0.5.0",
             "lastSent":"2020-06-01T15:23:02Z",
             "lastReceived":"2020-06-01T15:22:57Z"
          },
          {
             "ip":"158.255.67.151:9651",
             "publicIP":"158.255.67.151:9651",
             "nodeID":"NodeID-C14fr1n8EYNKyDfYixJ3rxSAVqTY3a8BP",
             "version":"avalanche/0.5.0",
             "lastSent":"2020-06-01T15:23:02Z",
             "lastReceived":"2020-06-01T15:22:34Z"
          },
          {
             "ip":"83.42.13.44:9651",
             "publicIP":"83.42.13.44:9651",
             "nodeID":"NodeID-LPbcSMGJ4yocxYxvS2kBJ6umWeeFbctYZ",
             "version":"avalanche/0.5.0",
             "lastSent":"2020-06-01T15:23:02Z",
             "lastReceived":"2020-06-01T15:22:55Z"
          }
        ]
    }
}
```

### `info.getTxFee`

**Description**

Get the transaction fee of the network.

**Signature**

```javascript
info.getTxFee() -> {txFee:uint64}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getTxFee"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "txFee": "1000000"
    }
}
```

