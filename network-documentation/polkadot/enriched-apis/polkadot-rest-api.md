---
description: Learn how to interact with Figment's Polkadot REST API
---

# Indexer API

## Source Documentation

You can review the full documentation on [**Figment's Github here**](https://github.com/figment-networks/polkadothub-indexer/tree/master#available-endpoints).

## Methods

### `GET /account/:stash_account`

**Description**

Gets account balance details for given height

**Parameters**

| **Parameter**      | Type   | Description                                             |
| ------------------ | ------ | ------------------------------------------------------- |
| **stash\_account** | string | account (required)                                      |
| **height**         | int    | block height (optional- if unspecified, returns latest) |

**Example Request**

```javascript
polkadot--indexer.datahub.figment.io/account/138QdRbUTB9eNY94Q4Mj5r39FkgMiyHCAy8UFMNA5gvtrfSB
```

**Example JSON output**

```javascript
{
    "nonce": 14,
    "free": "1018474380754",
    "reserved": "804170000000",
    "misc_frozen": "1018249380627",
    "fee_frozen": "1018249380627"
}
```

### `GET /account_details/:stash_account`

**Description**

Gets latest account balances, latest identity associated with the account (display name, email, social medias, etc), and all balance related events.

**Parameters**

| **Parameter**      | Type   | Description        |
| ------------------ | ------ | ------------------ |
| **stash\_account** | string | account (required) |

**Example Request**

```javascript
polkadot--indexer.datahub.figment.io/account_details/138QdRbUTB9eNY94Q4Mj5r39FkgMiyHCAy8UFMNA5gvtrfSB
```

**Example JSON output**

```javascript
{
    "address": "138QdRbUTB9eNY94Q4Mj5r39FkgMiyHCAy8UFMNA5gvtrfSB",
    "account": {
        "free": "1018474380754",
        "reserved": "804170000000",
        "misc_frozen": "1018249380627",
        "fee_frozen": "1018249380627"
    },
    "deposit": "202580000000",
    "display_name": "\bFigment",
    "legal_name": "Figment Inc.",
    "web_name":"https://figment.io",
    "riot_name": "",
    "email_name": "",
    "twitter_name": "@Figment_io",
    "image": "",
    "transfers": [
        {
            "transaction_hash": "0x90dbd1e75aa1e1e0481f8e4af7e557a13eecd39ab70b57e3d867239895bcff6b",
            "height": 2453048,
            "amount": "2696000000000",
            "kind": "out",
            "participant": "13mEAYL8iU3ixqRTLsbwNGc9js1wMd99GuLJXcst9KZcPfuU"
        },
        {
            "transaction_hash": "0xe916759fe510d1990af2467ad3756ba439a17129e1bfc50618670e15fde52ab2",
            "height": 3100446,
            "amount": "10107460000000",
            "kind": "out",
            "participant": "1PDHLovMTdXeQXPWRAEnHXcoqoDEJegCyTa1aX7G3RYn4ZH"
        },
        {
            "transaction_hash": "0xa8c79f0c11f7749045799caeba8f350eff8f902e1ffb2cfc65d6dc807eb17520",
            "height": 3100453,
            "amount": "6258540000000",
            "kind": "out",
            "participant": "16BPfNA5pVPs9KDWML4cds1dHrUxtRLeozMWqXEwHjqTn6YU"
        },
        {
            "transaction_hash": "0xba05f423ee2b4ce67515d010f761f098cbe472a2a9bdc9fa2668e3d93987030a",
            "height": 4344960,
            "amount": "800000000000",
            "kind": "out",
            "participant": "16c1VJXScECuyCgcsJGJ4CvbfA8tTMKh8qhrwZQjs7cDNska"
        }
    ],
    "deposits": [
        {
            "amount": "31400000",
            "transaction_hash": "0x5b2712e0b6fe166e180760d5037c5a59979c246a3ef50c22b54dd791a324667a",
            "height": 3584670
        },
        {
            "amount": "31000000",
            "transaction_hash": "0x60921c8eeb50308e3811a7759654b55aa01f2de12431865da8ec32348406e2ae",
            "height": 3584687
        },
        {
            "amount": "30800000",
            "transaction_hash": "0x64b6983cd79ccc7e37c47c75bedb19f6212331e2ac3b4ec200febf41d0f34170",
            "height": 3584687
        },
        {
            "amount": "31400000",
            "transaction_hash": "0xe06774ad832a05adea2a1faa597196347ff36c1dbb1b90b1b348425db05629f9",
            "height": 3578637
        }
    ],
    "bonded": [],
    "unbonded": [],
    "withdrawn": [
        {
            "amount": "20000000000000",
            "transaction_hash": "0x1e683d1a0df763e203a6d0416227d102b4bc2ad6c282f31c7f3404836abb5c53",
            "height": 2340696
        }
    ],
    "delegations": [
        {
            "era": 71,
            "validator_stash": "138QdRbUTB9eNY94Q4Mj5r39FkgMiyHCAy8UFMNA5gvtrfSB",
            "amount": 10000000000
        }
    ]
}
```

### `GET /rewards/:stash_account`

**Description**

Get daily rewards for account

**Parameters**

| **Parameter**      | Type   | Description                                               |
| ------------------ | ------ | --------------------------------------------------------- |
| **stash\_account** | string | account (required)                                        |
| **start**          | int    | the starting era \[Default: 1 = first] (optional)         |
| **end**            | int    | the ending era (if unspecified, returns latest)(optional) |

**Example Request**

```javascript
polkadot--indexer.datahub.figment.io/rewards/14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6?start=515
```

**Example JSON output**

```javascript
[
    {
        "era": 515,
        "start_height": 7470032,
        "end_height": 7484284,
        "time": "2021-10-30T11:36:18Z",
        "stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "validator_stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "amount": "271425882428",
        "kind": "commission",
        "claimed": false,
        "tx_hash": ""
    },
    {
        "era": 515,
        "start_height": 7470032,
        "end_height": 7484284,
        "time": "2021-10-30T11:36:18Z",
        "stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "validator_stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "amount": "467783870",
        "kind": "reward",
        "claimed": false,
        "tx_hash": ""
    },
    {
        "era": 516,
        "start_height": 7484284,
        "end_height": 7498534,
        "time": "2021-10-31T11:36:18Z",
        "stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "validator_stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "amount": "287268430670",
        "kind": "commission",
        "claimed": false,
        "tx_hash": ""
    },
    {
        "era": 516,
        "start_height": 7484284,
        "end_height": 7498534,
        "time": "2021-10-31T11:36:18Z",
        "stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "validator_stash_account": "14j3azi9gKGx2de7ADL3dkzZXFzTTUy1t3RND21PymHRXRp6",
        "amount": "499703722",
        "kind": "reward",
        "claimed": false,
        "tx_hash": ""
    }
]
```
