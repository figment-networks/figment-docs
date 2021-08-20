---
description: Learn how to interact with Avalanche's X-Chain
---

# X-Chain \(AVM\) API

## Source documentation

\*\*\*\*[**The AVM API's source documentation can be found here**](https://docs.avax.network/build/apis/exchange-chain-x-chain-api).

The X-Chain, Avalanche’s native platform for creating and trading assets, is an instance of the Avalanche Virtual Machine \(AVM\). This API allows clients to create and trade assets on the X-Chain and other instances of the AVM.

## Endpoints

`/ext/bc/X` to interact with the X-Chain.

`/ext/bc/blockchainID` to interact with other AVM instances, where `blockchainID` is the ID of a blockchain running the AVM.

## Methods

### `avm.buildGenesis`

**Description**

Given a JSON representation of this Virtual Machine’s genesis state, create the byte representation of that state.

**Endpoint**

This call is made to the AVM’s static API endpoint:

`/ext/vm/avm`

Note: addresses should not include a chain prefix \(ie. X-\) in calls to the static API endpoint because these prefixes refer to a specific chain.

**Signature**

```javascript
avm.buildGenesis(genesisData:JSON) -> {bytes:string}
```

where `genesisData` has this form:

```javascript
{
"genesisData" :
    {
        "assetAlias1": {               // Each object defines an asset
            "name": "human readable name",
            "symbol":"AVAL",           // Symbol is between 0 and 4 characters
            "initialState": {
                "fixedCap" : [         // Choose the asset type.
                    {                  // Can be "fixedCap", "variableCap", "limitedTransfer", "nonFungible"
                        "amount":1000, // At genesis, address A has
                        "address":"A"  // 1000 units of asset
                    },
                    {
                        "amount":5000, // At genesis, address B has
                        "address":"B"  // 1000 units of asset
                    },
                    ...                // Can have many initial holders
                ]
            }
        },
        "assetAliasCanBeAnythingUnique": { // Asset alias can be used in place of assetID in calls
            "name": "human readable name", // names need not be unique
            "symbol": "AVAL",              // symbols need not be unique
            "initialState": {
                "variableCap" : [          // No units of the asset exist at genesis
                    {
                        "minters": [       // The signature of A or B can mint more of
                            "A",           // the asset.
                            "B"
                        ],
                        "threshold":1
                    },
                    {
                        "minters": [       // The signatures of 2 of A, B and C can mint
                            "A",           // more of the asset
                            "B",
                            "C"
                        ],
                        "threshold":2
                    },
                    ...                    // Can have many minter sets
                ]
            }
        },
        ...                                // Can list more assets
    }
}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id"     : 1,
    "method" : "avm.buildGenesis",
    "params" : {
        "genesisData": {
            "asset1": {
                "name": "myFixedCapAsset",
                "symbol":"MFCA",
                "initialState": {
                    "fixedCap" : [
                        {
                            "amount":100000,
                            "address": "avax13ery2kvdrkd2nkquvs892gl8hg7mq4a6ufnrn6"
                        },
                        {
                            "amount":100000,
                            "address": "avax1rvks3vpe4cm9yc0rrk8d5855nd6yxxutfc2h2r"
                        },
                        {
                            "amount":50000,
                            "address": "avax1ntj922dj4crc4pre4e0xt3dyj0t5rsw9uw0tus"
                        },
                        {
                            "amount":50000,
                            "address": "avax1yk0xzmqyyaxn26sqceuky2tc2fh2q327vcwvda"
                        }
                    ]
                }
            },
            "asset2": {
                "name": "myVarCapAsset",
                "symbol":"MVCA",
                "initialState": {
                    "variableCap" : [
                        {
                            "minters": [
                                "avax1kcfg6avc94ct3qh2mtdg47thsk8nrflnrgwjqr",
                                "avax14e2s22wxvf3c7309txxpqs0qe9tjwwtk0dme8e"
                            ],
                            "threshold":1
                        },
                        {
                            "minters": [
                                "avax1y8pveyn82gjyqr7kqzp72pqym6xlch9gt5grck",
                                "avax1c5cmm0gem70rd8dcnpel63apzfnfxye9kd4wwe",
                                "avax12euam2lwtwa8apvfdl700ckhg86euag2hlhmyw"
                            ],
                            "threshold":2
                        }
                    ]
                }
            }
        }
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/vm/avm
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "bytes":"11111BcSrCUj7fX2ZiHNVgPnTXSiS1bB1vWo7QMaZ61vcyR7LHgFURR95N4TR6Tnu9u4dUW8M1ERahfCrexDbZr6A7d3dfRkbhJyhyspHdLsxUj8Vxn3pmGt5iTCtJwPggjxy5EEqrK9EZGgTprKFonWY8EkE1hAfp1yLqKRNj64Yii4w6uqoMeiECV4h7nD2YmdXmDkKEPT3MuKesXKjFkpfK9nAMfVJx7JMAjNnS418zSbvjxs6kbbd8TYKna8CYwo8PgjGAqhWE4FkLKcF7vGjZobCkDqbYMmazqeDtHnQLdwEzdjMMCcstvRKG7a7WdCxTt1LDVviVY5DmbsbzZoAwh9b95dvhJCMZS5DfQkuNFrhyfnwqMR49jPdU7tnqisd2fXq75kcaumST2y3SHGVgGRDmuQeZeEUnnVRjeejNcCUdraTj8U5cNb91mKDhL36MkmWZgTaA3pPj2RHJQuBBTbtuHdtpgjZGAPZixX6btg328xUEyvhHzmoVBPswC6BpwXCLhZz1zTPz5XVeu5qEzKoUZesu5Ud6ExAG5R29J5ubdkvoDjNn5VacXRgYX3yxfxtdUmjKQGsqRV23YNJcoTHveSy8HHnPtPXcP6mf6aDoWY2i6pbKoG8ixxZoqZDqDsEbbAhzMjar7yob1B1f5Scm92HfpThKsAWd3iWbyabBLxhT3g54ohm6SjjQKkzRS8Z"
    },
    "id": 1
}
```

### `avm.createAddress`

**Description**

Create a new address controlled by the given user.

**Signature**

```javascript
avm.createAddress({
    username: string,
    password:string
}) -> {address: string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc": "2.0",
    "method": "avm.createAddress",
    "params": {
        "username":"myUsername",
        "password":"myPassword"
    },
    "id": 1
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "address": "X-avax12c6n252g5v3w6a6v69f0mnnzwr77jxzr3q3u7d"
    },
    "id": 1
}
```

### `avm.createFixedCapAsset`

**Description**

Create a new fixed-cap, fungible asset. A quantity of it is created at initialization and then no more is ever created. The asset can be sent with `avm.send`.

**Signature**

```javascript
avm.createFixedCapAsset({
    name: string,
    symbol: string,
    denomination: int,  
    initialHolders: []{
        address: string,
        amount: int
    },
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,  
    password: string
}) ->
{
    assetID: string,
    changeAddr: string
}
```

* `name` is a human-readable name for the asset. Not necessarily unique.
* `symbol` is a shorthand symbol for the asset. Between 0 and 4 characters. Not necessarily unique. May be omitted.
* `denomination` determines how balances of this asset are displayed by user interfaces. If `denomination` is 0, 100 units of this asset are displayed as 100. If `denomination` is 1, 100 units of this asset are displayed as 10.0. If `denomination` is 2, 100 units of this asset are displays as .100, etc. Defaults to 0.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* `username` and `password` denote the user paying the transaction fee.
* Each element in `initialHolders` specifies that `address` holds `amount` units of the asset at genesis.
* `assetID` is the ID of the new asset.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.createFixedCapAsset",
    "params" :{
        "name": "myFixedCapAsset",
        "symbol":"MFCA",
        "initialHolders": [
            {
                "address": "X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp",
                "amount": 10000
            },
            {
                "address":"X-avax1y0h66sjk0rlnh9kppnfskwpw2tpcluzxh9png8",
                "amount":50000
            }
        ],
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username":"myUsername",
        "password":"myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "assetID":"ZiKfqRXCZgHLgZ4rxGU9Qbycdzuq5DRY4tdSNS9ku8kcNxNLD",
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    }
}
```

### `avm.mint`

**Description**

Mint units of a variable-cap asset \(an asset created with `avm.createVariableCapAsset`.\)

**Signature**

```javascript
avm.mint({
    amount: int,
    assetID: string,
    to: string,
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,
    password: string
}) ->
{
    txID: string,
    changeAddr: string,
}
```

* `amount` units of `assetID` will be created and controlled by address `to`.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* `username` is the user that pays the transaction fee. `username` must hold keys giving it permission to mint more of this asset. That is, it must control at least _threshold_ keys for one of the minter sets.
* `txID` is this transaction’s ID.
* `changeAddr` in the result is the address where any change was sent.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.mint",
    "params" :{
        "amount":10000000,
        "assetID":"i1EqsthjiFTxunrj8WD2xFSrQ5p2siEKQacmCCB5qBFVqfSL2",
        "to":"X-avax1ap39w4a7fk0au083rrmnhc2pqk20yjt6s3gzkx",
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username":"USERNAME GOES HERE",
        "password":"PASSWORD GOES HERE"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "txID":"2oGdPdfw2qcNUHeqjw8sU2hPVrFyNUTgn6A8HenDra7oLCDtja",
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    }
}
```

### `avm.createVariableCapAsset`

**Description**

Create a new variable-cap, fungible asset. No units of the asset exist at initialization. Minters can mint units of this asset using `mint`.

See [this tutorial](https://learn.figment.io/network-documentation/avalanche/tutorials/creating-a-fixed-cap-asset) for an example of usage.

**Signature**

```javascript
avm.createVariableCapAsset({
    name: string,
    symbol: string,
    denomination: int,  
    minterSets []{
        minters: []string,
        threshold: int
    },
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,  
    password: string
}) ->
 {
    assetID: string,
    changeAddr: string,
}
```

* `name` is a human-readable name for the asset. Not necessarily unique.
* `symbol` is a shorthand symbol for the asset. Between 0 and 4 characters. Not necessarily unique. May be omitted.
* `denomination` determines how balances of this asset are displayed by user interfaces. If denomination is 0, 100 units of this asset are displayed as 100. If denomination is 1, 100 units of this asset are displayed as 10.0. If denomination is 2, 100 units of this asset are displays as .100, etc.
* `minterSets` is a list where each element specifies that `threshold` of the addresses in `minters` may together mint more of the asset by signing a minting transaction.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* `username` pays the transaction fee.
* `assetID` is the ID of the new asset.
* `changeAddr` in the result is the address where any change was sent.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.createVariableCapAsset",
    "params" :{
        "name":"myVariableCapAsset",
        "symbol":"MFCA",
        "minterSets":[
            {
                "minters":[
                    "X-avax14q0p6y4yzweuugz9p080kapajwvac3ur755n7d"
                ],
                "threshold": 1
            },
            {
                "minters": [
                    "X-avax1fzyldr3mwn6lj7y46edhua6vr5ayx0ruuhezpv",
                    "X-avax1x5mrgxj0emysnnzyszamqxhq95t2kwcp9n3fy3",
                    "X-avax13zmrjvj75h3578rn3sfth8p64t2ll4gm4tv2rp"
                ],
                "threshold": 2
            }
        ],
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username":"myUsername",
        "password":"myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "assetID":"2QbZFE7J4MAny9iXHUwq8Pz8SpFhWk3maCw4SkinVPv6wPmAbK",
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    }
}
```

### `avm.createNFTAsset`

**Description**

Create a new non-fungible asset. No units of the asset exist at initialization. Minters can mint units of this asset using `mintNFT`.

**Signature**

```javascript
avm.createNFTAsset({
    name: string,
    symbol: string,
    minterSets []{
        minters: []string,
        threshold: int
    },
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,  
    password: string
}) ->
 {
    assetID: string,
    changeAddr: string,
}
```

* `name` is a human-readable name for the asset. Not necessarily unique.
* `symbol` is a shorthand symbol for the asset. Between 0 and 4 characters. Not necessarily unique. May be omitted.
* `minterSets` is a list where each element specifies that `threshold` of the addresses in `minters` may together mint more of the asset by signing a minting transaction.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* `username` pays the transaction fee.
* `assetID` is the ID of the new asset.
* `changeAddr` in the result is the address where any change was sent.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.createNFTAsset",
    "params" :{
        "name":"Coincert",
        "symbol":"TIXX",
        "minterSets":[
            {
                "minters":[
                    "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
                ],
                "threshold": 1
            }
        ],
        "from": ["X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"],
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username":"myUsername",
        "password":"myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "assetID": "2KGdt2HpFKpTH5CtGZjYt5XPWs6Pv9DLoRBhiFfntbezdRvZWP",
        "changeAddr": "X-local18jma8ppw3nhx5r4ap8clazz0dps7rv5u00z96u"
    },
    "id": 1
}
```

### `avm.mintNFT`

**Description**

Mint non-fungible tokens which were created with `avm.createNFTAsset`.

**Signature**

```javascript
avm.mintNFT({
    assetID: string,
    payload: string,
    to: string,
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,
    password: string
}) ->
{
    txID: string,
    changeAddr: string,
}
```

* `assetID` is the assetID of the newly created NFT asset.
* `payload` is an arbitrary CB58 encoded payload of up to 1024 bytes.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* `username` is the user that pays the transaction fee. `username` must hold keys giving it permission to mint more of this asset. That is, it must control at least _threshold_ keys for one of the minter sets.
* `txID` is this transaction’s ID.
* `changeAddr` in the result is the address where any change was sent.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.mintNFT",
    "params" :{
        "assetID":"2KGdt2HpFKpTH5CtGZjYt5XPWs6Pv9DLoRBhiFfntbezdRvZWP",
        "payload":"2EWh72jYQvEJF9NLk",
        "to":"X-avax1ap39w4a7fk0au083rrmnhc2pqk20yjt6s3gzkx",
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username":"USERNAME GOES HERE",
        "password":"PASSWORD GOES HERE"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "txID":"2oGdPdfw2qcNUHeqjw8sU2hPVrFyNUTgn6A8HenDra7oLCDtja",
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    }
}
```

### `avm.exportAVAX`

**Description**

Send AVAX from the X-Chain to another chain.  
After calling this method, you must call `importAVAX` on the other chain to complete the transfer.

**Signature**

```javascript
avm.exportAVAX({
    to: string,
    amount: int,
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,
    password:string,
}) ->
{
    txID: string,
    changeAddr: string,
}
```

* `to` is the P-Chain address the AVAX is sent to.
* `amount` is the amount of nAVAX to send.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* The AVAX is sent from addresses controlled by `username`
* `txID` is this transaction’s ID.
* `changeAddr` in the result is the address where any change was sent.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.exportAVAX",
    "params" :{
        "to":"P-avax1q9c6ltuxpsqz7ul8j0h0d0ha439qt70sr3x2m0",
        "amount": 500,
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr":"X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username":"myUsername",
        "password":"myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "txID": "25VzbNzt3gi2vkE3Kr6H9KJeSR2tXkr8FsBCm3vARnB5foLVmx",
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    },
    "id": 1
}
```

### `avm.exportKey`

**Description**

Get the private key that controls a given address.  
The returned private key can be added to a user with `avm.importKey`.

**Signature**

```javascript
avm.exportKey({
    username: string,
    password:string,
    address:string
}) -> {privateKey: string}
```

* `username` must control `address`.
* `privateKey` is the string representation of the private key that controls `address`.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.exportKey",
    "params" :{
        "username" :"myUsername",
        "password":"myPassword",
        "address": "X-avax1jggdngzc9l87rgurmfu0z0n0v4mxlqta0h3k6e"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "privateKey":"PrivateKey-2w4XiXxPfQK4TypYqnohRL8DRNTz9cGiGmwQ1zmgEqD9c9KWLq"
    }
}
```

### `avm.getAllBalances`

**Description**

Get the balances of all assets controlled by a given address.

**Signature**

```javascript
avm.getAllBalances({address:string}) -> {
    balances: []{
        asset: string,
        balance: int
    }
}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.getAllBalances",
    "params" :{
        "address":"X-avax1c79e0dd0susp7dc8udq34jgk2yvve7haclsz5r"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "balances": [
            {
                "asset": "AVAX",
                "balance": "102"
            },
            {
                "asset": "2sdnziCz37Jov3QSNMXcFRGFJ1tgauaj6L7qfk7yUcRPfQMC79",
                "balance": "10000"
            }
        ]
    },
    "id": 1
}
```

### `avm.getAssetDescription`

**Description**

Get information about an asset.

**Signature**

```javascript
avm.getAssetDescription({assetID: string}) -> {name: string, symbol: string, denomination:int}
```

* `name` is the asset’s human-readable, not necessarily unique name.
* `symbol` is the asset’s symbol.
* `denomination` determines how balances of this asset are displayed by user interfaces. If denomination is 0, 100 units of this asset are displayed as 100. If denomination is 1, 100 units of this asset are displayed as 10.0. If denomination is 2, 100 units of this asset are displays as .100, etc.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.getAssetDescription",
    "params" :{
        "assetID" :"ZiKfqRXCZgHLgZ4rxGU9Qbycdzuq5DRY4tdSNS9ku8kcNxNLD"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "name":"My asset name",
        "symbol":"MyAN"
    }
}
```

### `avm.getBalance`

**Description**

Get the balance of an asset controlled by a given address.

**Signature**

```javascript
avm.getBalance({
    address:string,
    assetID: string
}) -> {balance: int}
```

**Example Call**

```javascript
curl -X POST --data '{
  "jsonrpc":"2.0",
  "id"     : 1,
  "method" :"avm.getBalance",
  "params" :{
      "address":"X-avax1ns3jzhqyk7parg29qan56k0fcxwstc76cjqq2s",
      "assetID": "2pYGetDWyKdHxpFxh2LHeoLNCH6H5vxxCxHQtFnnFaYxLsqtHC"
  }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "balance":"299999999999900",
        "utxoIDs":[
            {
                "txID":"WPQdyLNqHfiEKp4zcCpayRHYDVYuh1hqs9c1RqgZXS4VPgdvo",
                "outputIndex":1
            }
        ]
    }
}
```

### `avm.getTx`

**Description**

Returns the specified transaction

**Signature**

```javascript
avm.getTx({txID: string}) -> {tx: string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.getTx",
    "params" :{
        "txID":"2QouvFWUbjuySRxeX5xMbNCuAaKWfbk5FeEa2JmoF85RKLk2dD"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "tx":"1111111vQFqEEHkkAGwJnpdAJgga28zHk9pFARHp1VWe3QM5wC7ztGA5cZAPanFWXHkhbWEbFs9qsEpNZ7QHrzucUUZqLEPrAwJZLrZBik4dEhbsTCF3nS6s2fXVzc5ar2esLFD92WVMZmJNuTUQuKjVkjag2Gy3HHYSqm6bojrG62KrazywKPhrYx8QF9AqNfYYwD3XcSUV1g46r7sQ1WqzM8nyG4qL517JS1YVuTC3aWPeN5cxP6FdvbYexwHcgaBtiQsYbCEeZ9cuJqhE2Pxx8BJFpicLN8FBexb6fzQyBLiFR7yx6v6YBjq7dtu9MBczFdNCnDE4MsG2SyPZsdUv1XxQYVVwDqgqi8Zto5esJKph72YZbrXX3SHVSZBFZXkKbTzyEQFWHCF1jC"
    }
}
```

### `avm.getTxStatus`

**Description**

Get the status of a transaction sent to the network.

**Signature**

```javascript
avm.getTxStatus({txID: string}) -> {status: string}
```

`status` is one of:

* `Accepted`: The transaction is \(or will be\) accepted by every node
* `Processing`: The transaction is being voted on by this node
* `Rejected`: The transaction will never be accepted by any node in the network
* `Unknown`: The transaction hasn’t been seen by this node

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.getTxStatus",
    "params" :{
        "txID":"2QouvFWUbjuySRxeX5xMbNCuAaKWfbk5FeEa2JmoF85RKLk2dD"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "status":"Accepted"
    }
}
```

### `avm.getUTXOs`

**Description**

Gets the UTXOs that reference a given address. If sourceChain is specified, then it will retrieve the atomic UTXOs exported from that chain to the X Chain.

**Signature**

```javascript
avm.getUTXOs(
    {
        addresses: string,
        limit: int, (optional)
        startIndex: { (optional)
            address: string,
            utxo: string
        },
        sourceChain: string (optional)
    },
) -> 
{
    numFetched: int
    utxos: []string,
    endIndex: {
        address: string,
        utxo: string
    }
}
```

* `utxos` is a list of UTXOs such that each UTXO references at least one address in `addresses`.
* At most `limit` UTXOs are returned. If `limit` is omitted or greater than 1024, it is set to 1024.
* This method supports pagination. `endIndex` denotes the last UTXO returned. To get the next set of UTXOs, use the value of `endIndex` as `startIndex` in the next call.
* If `startIndex` is omitted, will fetch all UTXOs up to `limit`.
* When using pagination \(ie when `startIndex` is provided\), UTXOs are not guaranteed to be unique across multiple calls. That is, a UTXO may appear in the result of the first call, and then again in the second call.
* When using pagination, consistency is not guaranteed across multiple calls. That is, the UTXO set of the addresses may have changed between calls.

**Example**

Suppose we want all UTXOs that reference at least one of `X-avax1yzt57wd8me6xmy3t42lz8m5lg6yruy79m6whsf` and `X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz`.

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.getUTXOs",
    "params" :{
        "addresses":["X-avax1yzt57wd8me6xmy3t42lz8m5lg6yruy79m6whsf", "X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz"],
        "limit":5
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

This gives response:

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "numFetched": "5",
        "utxos": [
            "11PQ1sNw9tcXjVki7261souJnr1TPFrdVCu5JGZC7Shedq3a7xvnTXkBQ162qMYxoerMdwzCM2iM1wEQPwTxZbtkPASf2tWvddnsxPEYndVSxLv8PDFMwBGp6UoL35gd9MQW3UitpfmFsLnAUCSAZHWCgqft2iHKnKRQRz",
            "11RCDVNLzFT8KmriEJN7W1in6vB2cPteTZHnwaQF6kt8B2UANfUkcroi8b8ZSEXJE74LzX1mmBvtU34K6VZPNAVxzF6KfEA8RbYT7xhraioTsHqxVr2DJhZHpR3wGWdjUnRrqSSeeKGE76HTiQQ8WXoABesvs8GkhVpXMK",
            "11GxS4Kj2od4bocNWMQiQhcBEHsC3ZgBP6edTgYbGY7iiXgRVjPKQGkhX5zj4NC62ZdYR3sZAgp6nUc75RJKwcvBKm4MGjHvje7GvegYFCt4RmwRbFDDvbeMYusEnfVwvpYwQycXQdPFMe12z4SP4jXjnueernYbRtC4qL",
            "11S1AL9rxocRf2NVzQkZ6bfaWxgCYch7Bp2mgzBT6f5ru3XEMiVZM6F8DufeaVvJZnvnHWtZqocoSRZPHT5GM6qqCmdbXuuqb44oqdSMRvLphzhircmMnUbNz4TjBxcChtks3ZiVFhdkCb7kBNLbBEmtuHcDxM7MkgPjHw",
            "11Cn3i2T9SMArCmamYUBt5xhNEsrdRCYKQsANw3EqBkeThbQgAKxVJomfc2DE4ViYcPtz4tcEfja38nY7kQV7gGb3Fq5gxvbLdb4yZatwCZE7u4mrEXT3bNZy46ByU8A3JnT91uJmfrhHPV1M3NUHYbt6Q3mJ3bFM1KQjE"
        ],
        "endIndex": {
            "address": "X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz",
            "utxo": "kbUThAUfmBXUmRgTpgD6r3nLj7rJUGho6xyht5nouNNypH45j"
        }
    },
    "id": 1
}
```

Since `numFetched` is the same as `limit`, we can tell that there may be more UTXOs that were not fetched. We call the method again, this time with `startIndex`:

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :2,
    "method" :"avm.getUTXOs",
    "params" :{
        "addresses":["X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz"],
        "limit":5,
        "endIndex": {
            "address": "X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz",
            "utxo": "kbUThAUfmBXUmRgTpgD6r3nLj7rJUGho6xyht5nouNNypH45j"
        }
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

This gives response:

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "numFetched": "4",
        "utxos": [
            "115ZLnNqzCsyugMY5kbLnsyP2y4se4GJBbKHjyQnbPfRBitqLaxMizsaXbDMU61fHV2MDd7fGsDnkMzsTewULi94mcjk1bfvP7aHYUG2i3XELpV9guqsCtv7m3m3Kg4Ya1m6tAWqT7PhvAaW4D3fk8W1KnXu5JTWvYBqD2",
            "11QASUuhw9M1r52maTFUZ4fnuQby9inX77VYxePQoNavEyCPuHN5cCWPQnwf8fMrydFXVMPAcS4UJAcLjSFskNEmtVPDMY4UyHwh2MChBju6Y7V8yYf3JBmYt767NPsdS3EqgufYJMowpud8fNyH1to4pAdd6A9CYbD8KG",
            "11MHPUWT8CsdrtMWstYpFR3kobsvRrLB4W8tP9kDjhjgLkCJf9aaJQM832oPcvKBsRhCCxfKdWr2UWPztRCU9HEv4qXVwRhg9fknAXzY3a9rXXPk9HmArxMHLzGzRECkXpXb2dAeqaCsZ637MPMrJeWiovgeAG8c5dAw2q",
            "11K9kKhFg75JJQUFJEGiTmbdFm7r1Uw5zsyDLDY1uVc8zo42WNbgcpscNQhyNqNPKrgtavqtRppQNXSEHnBQxEEh5KbAEcb8SxVZjSCqhNxME8UTrconBkTETSA23SjUSk8AkbTRrLz5BAqB6jo9195xNmM3WLWt7mLJ24"
        ],
        "endIndex": {
            "address": "X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz",
            "utxo": "21jG2RfqyHUUgkTLe2tUp6ETGLriSDTW3th8JXFbPRNiSZ11jK"
        }
    },
    "id": 1
}
```

Since `numFetched` is less than `limit`, we know that we are done fetching UTXOs and don’t need to call this method again.

Suppose we want to fetch the UTXOs exported from the P Chain to the X Chain in order to build an ImportTx. Then we need to call GetUTXOs with the sourceChain argument in order to retrieve the atomic UTXOs:

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.getUTXOs",
    "params" :{
        "addresses":["X-avax1yzt57wd8me6xmy3t42lz8m5lg6yruy79m6whsf", "X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz"],
        "limit":5,
        "sourceChain": "P"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

This gives response:

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "numFetched": "1",
        "utxos": [
            "115P1k9aSVFBfi9siZZz135jkrBCdEMZMbZ82JaLLuML37cgVMuxgu73ukQbPjXtDgyBCE1cgrJjqDPgboUswV5BGAYhnuxunkHS3xncB599V3mxyvWnwVwNPmq3mKQwF5EWhfTaXkhqE5VFr92yQBk9Nh5ekZBDSFGCSC"
        ],
        "endIndex": {
            "address": "X-avax1x459sj0ssujguq723cljfty4jlae28evjzt7xz",
            "utxo": "2Sz2XwRYqUHwPeiKoRnZ6ht88YqzAF1SQjMYZQQaB5wBFkAqST"
        }
    },
    "id": 1
}
```

### `avm.importAVAX`

**Description**

Finalize a transfer of AVAX from the P-Chain to the X-Chain. Before this method is called, you must call the P-Chain’s `exportAVAX` method to initiate the transfer.

**Signature**

```javascript
avm.importAVAX({
    to: string,
    sourceChain: string,
    username: string,
    password:string,
}) -> {txID: string}
```

* `to` is the address the AVAX is sent to. This must be the same as the `to` argument in the corresponding call to the P-Chain’s `exportAVAX`.
* `sourceChain` is the ID or alias of the chain the AVAX is being imported from. To import funds from the P-Chain, use `"P"`.
* `username` is the user that controls `to`.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.importAVAX",
    "params" :{
        "to":"X-avax1s7aygrkrtxflmrlyadlhqu70a6f4a4n8l2tru8",
        "sourceChain":"P",
        "username":"myUsername",
        "password":"myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "txID": "MqEaeWc4rfkw9fhRMuMTN7KUTNpFmh9Fd7KSre1ZqTsTQG73h"
    },
    "id": 1
}
```

### `avm.importKey`

**Description**

Give a user control over an address by providing the private key that controls the address.

**Signature**

```javascript
avm.importKey({
    username: string,
    password:string,
    privateKey:string
}) -> {address: string}
```

* Add `privateKey` to `username`‘s set of private keys. `address` is the address `username` now controls with the private key.

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.importKey",
    "params" :{
        "username" :"myUsername",
        "password":"myPassword",
        "privateKey":"PrivateKey-2w4XiXxPfQK4TypYqnohRL8DRNTz9cGiGmwQ1zmgEqD9c9KWLq"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "address":"X-avax1mwlnrzv0ezdycx4qhqj77j55cwgcvtf29zvmpy"
    }
}
```

### `avm.issueTx`

**Description**

Send a signed transaction to the network.

**Signature**

```javascript
avm.issueTx({tx: string}) -> {txID: string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     : 1,
    "method" :"avm.issueTx",
    "params" :{
        "tx":"6sTENqXfk3gahxkJbEPsmX9eJTEFZRSRw83cRJqoHWBiaeAhVbz9QV4i6SLd6Dek4eLsojeR8FbT3arFtsGz9ycpHFaWHLX69edJPEmj2tPApsEqsFd7wDVp7fFxkG6HmySR"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "txID":"NUPLwbt2hsYxpQg4H2o451hmTWQ4JZx2zMzM4SinwtHgAdX1JLPHXvWSXEnpecStLj"
    }
}
```

### `avm.listAddresses`

**Description**

List addresses controlled by the given user.

**Signature**

```javascript
avm.listAddresses({
    username: string,
    password: string
}) -> {addresses: []string}
```

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc": "2.0",
    "method": "avm.listAddresses",
    "params": {
        "username":"myUsername",
        "password":"myPassword"
    },
    "id": 1
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "addresses": ["X-avax1rt4vac58crp0p59yf640c4gycm6creg2rt8hc6"]
    },
    "id": 1
}
```

### `avm.send`

**Description**

Send a quantity of an asset to an address.

**Signature**

```javascript
avm.send({
    amount: int,
    assetID: string,
    to: string,
    from: []string, (optional)
    changeAddr: string, (optional)
    memo: string, (optional)
    username: string,
    password: string
}) -> {txID: string, changeAddr: string}
```

* Sends `amount` units of asset with ID `assetID` to address `to`. `amount` is denominated in the smallest increment of the asset. For AVAX this is 1 nAVAX \(one billionth of 1 AVAX.\)
* `to` is the X-Chain address the asset is sent to.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* You can attach a `memo`, whose length can be up to 256 bytes.
* The asset is sent from addresses controlled by user `username`. \(Of course, that user will need to hold at least the balance of the asset being sent.\)

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.send",
    "params" :{
        "assetID"   : "AVAX",
        "amount"    : 10000,
        "to"        : "X-avax1yzt57wd8me6xmy3t42lz8m5lg6yruy79m6whsf",
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "memo"      : "hi, mom!",
        "username"  : "userThatControlsAtLeast10000OfThisAsset",
        "password"  : "myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "txID":"2iXSVLPNVdnFqn65rRvLrsu8WneTFqBJRMqkBJx5vZTwAQb8c1",
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    }
}
```

### `avm.sendMultiple`

**Description**

Sends an amount of assetID to an array of specified addresses from a list of owned of addresses.

**Signature**

```javascript
avm.sendMultiple({
    outputs: []{
      assetID: string,
      amount: int,
      to: string
    }
    from: []string, (optional)
    changeAddr: string, (optional)
    memo: string, (optional)
    username: string,
    password: string
}) -> {txID: string, changeAddr: string}
```

* `outputs` is an array of object literals which each contain an `assetID`, `amount` and `to`.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed.
* `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* You can attach a `memo`, whose length can be up to 256 bytes.
* The asset is sent from addresses controlled by user `username`. \(Of course, that user will need to hold at least the balance of the asset being sent.\)

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.sendMultiple",
    "params" :{
        "outputs": [
            {
                "assetID" : "AVAX",
                "to"      : "X-avax1yzt57wd8me6xmy3t42lz8m5lg6yruy79m6whsf",
                "amount"  : 1000000000
            }
        ],
        "from":["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "memo"      : "hi, mom!",
        "username"  : "userThatControlsAtLeast10000OfThisAsset",
        "password"  : "myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc":"2.0",
    "id"     :1,
    "result" :{
        "txID":"2iXSVLPNVdnFqn65rRvLrsu8WneTFqBJRMqkBJx5vZTwAQb8c1",
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8"
    }
}
```

### `avm.sendNFT`

**Description**

Send a non-fungible token.

**Signature**

```javascript
avm.sendNFT({
    assetID: string,
    groupID: number,
    to: string,
    from: []string, (optional)
    changeAddr: string, (optional)
    username: string,
    password: string
}) -> {txID: string}
```

* `assetID` is the asset ID of the NFT of the NFT being sent.
* `groupID` is the NFT group from which to send the NFT. NFT creation allows multiple groups under each NFT ID. You can issue multiple NFTs to each group.
* `to` is the X-Chain address the NFT is sent to.
* `from` are the addresses that you want to use for this operation. If omitted, uses any of your addresses as needed. `changeAddr` is the address any change will be sent to. If omitted, change is sent to one of the addresses controlled by the user.
* The asset is sent from addresses controlled by user `username`. \(Of course, that user will need to hold at least the balance of the NFT being sent.\)

**Example Call**

```javascript
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"avm.sendNFT",
    "params" :{
        "assetID"   : "2KGdt2HpFKpTH5CtGZjYt5XPWs6Pv9DLoRBhiFfntbezdRvZWP",
        "groupID"   : 0,
        "to"        : "X-avax1yzt57wd8me6xmy3t42lz8m5lg6yruy79m6whsf",
        "from"      :["X-avax1s65kep4smpr9cnf6uh9cuuud4ndm2z4jguj3gp"],
        "changeAddr": "X-avax1turszjwn05lflpewurw96rfrd3h6x8flgs5uf8",
        "username"  : "myUsername",
        "password"  : "myPassword"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/bc/X
```

**Example Response**

```javascript
{
    "jsonrpc": "2.0",
    "result": {
        "txID": "DoR2UtG1Trd3Q8gWXVevNxD666Q3DPqSFmBSMPQ9dWTV8Qtuy",
        "changeAddr": "X-local18jma8ppw3nhx5r4ap8clazz0dps7rv5u00z96u"
    },
    "id": 1
}
```

