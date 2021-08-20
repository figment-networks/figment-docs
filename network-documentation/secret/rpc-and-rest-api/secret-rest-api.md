---
description: Learn how to interact with the Secret REST API
---

# Secret REST API

## Source documentation <a id="source-documentation"></a>

​[**The Secret REST API source documentation can be found here**](https://secretapi.io/#/).

A REST interface for state queries, transaction generation and broadcasting.

## **Transactions** <a id="transactions"></a>

**Search, encode, or broadcast transactions.**

### `GET/txs/{hash}` <a id="get-txs-hash"></a>

**Description**

Get a transaction by hash

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **hash** | string \* required | Transaction hash |

**Example JSON Output**

```javascript
{
  "hash": "D085138D913993919295FF4B0A9107F1F2CDE0D37A87CE0644E217CBF3B49656",
  "height": 368,
  "tx": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "stake",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signatures": [
      {
        "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
        "pub_key": {
          "type": "tendermint/PubKeySecp256k1",
          "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
        },
        "account_number": "0",
        "sequence": "0"
      }
    ]
  },
  "result": {
    "log": "string",
    "gas_wanted": "200000",
    "gas_used": "26354",
    "tags": [
      {
        "key": "string",
        "value": "string"
      }
    ]
  }
}
```

### `GET/txs` <a id="get-txs"></a>

**Description**

Search transactions

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **message.action** | string | Transaction events such as 'message.action=send' which results in the following /txs?message.action=send' |
| **message.sender** | string | Transaction tags with sender: 'GET /txs message.action=send&message.sender=cosmos16xyempempp92x9hyzz9wrgf94r6j9h5f06pxxv' |
| **page** | integer | Page number |
| **limit** | integer | Maximum number of items per page |
| **tx.minheight** | integer | Transactions on blocks with height greater or equal this value |
| **tx.maxheight** | integer | Transactions on blocks with height less than or equal this value |

**Example JSON Output**

```javascript
{
  "total_count": 1,
  "count": 1,
  "page_number": 1,
  "page_total": 1,
  "limit": 30,
  "txs": [
    {
      "hash": "D085138D913993919295FF4B0A9107F1F2CDE0D37A87CE0644E217CBF3B49656",
      "height": 368,
      "tx": {
        "msg": [
          "string"
        ],
        "fee": {
          "gas": "string",
          "amount": [
            {
              "denom": "stake",
              "amount": "50"
            }
          ]
        },
        "memo": "string",
        "signatures": [
          {
            "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
            "pub_key": {
              "type": "tendermint/PubKeySecp256k1",
              "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
            },
            "account_number": "0",
            "sequence": "0"
          }
        ]
      },
      "result": {
        "log": "string",
        "gas_wanted": "200000",
        "gas_used": "26354",
        "tags": [
          {
            "key": "string",
            "value": "string"
          }
        ]
      }
    }
  ]
}
```

### `POST/txs` <a id="post-txs"></a>

**Description**

Broadcast a signed transaction

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **txBroadcast** | object | The transaction must be signed StdTx. The supported broadcast modes include `"block"`\(return after tx commit\), `"sync"`\(return afer CheckTx\) and `"async"`\(return right away\). |

**Example JSON Output**

```javascript
{
  "check_tx": {
    "code": 0,
    "data": "data",
    "log": "log",
    "gas_used": 5000,
    "gas_wanted": 10000,
    "info": "info",
    "tags": [
      "",
      ""
    ]
  },
  "deliver_tx": {
    "code": 5,
    "data": "data",
    "log": "log",
    "gas_used": 5000,
    "gas_wanted": 10000,
    "info": "info",
    "tags": [
      "",
      ""
    ]
  },
  "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
  "height": 0
}
```

### `POST/txs/encode` <a id="post-txs-encode"></a>

**Description**

Encode a transaction to the Amino wire format

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **tx** | object | The transaction to encode |

**Example JSON Output**

```javascript
{
  "tx": "The base64-encoded Amino-serialized bytes for the tx"
}
```

### `POST/txs/decode`

**Description**

Decode a transaction \(signed or not\) from base64-encoded Amino serialized bytes to JSON**.**

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **tx** | body \* required | The transaction to decode |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

## **Tendermint RPC** <a id="tendermint-rpc"></a>

**Tendermint APIs, such as query blocks, transactions and validator set**

### `GET/syncing` <a id="get-syncing"></a>

**Description**

Syncing state of node

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "syncing": true
}
```

### `GET/blocks/latest` <a id="get-blocks-latest"></a>

**Description**

Get the latest block

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "block_meta": {
    "header": {
      "chain_id": "secret-1",
      "height": 1,
      "time": "2017-12-30T05:53:09.287+01:00",
      "num_txs": 0,
      "last_block_id": {
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "parts": {
          "total": 0,
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
        }
      },
      "total_txs": 35,
      "last_commit_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "data_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "next_validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "consensus_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "app_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "last_results_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "evidence_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "proposer_address": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27",
      "version": {
        "block": 10,
        "app": 0
      }
    },
    "block_id": {
      "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "parts": {
        "total": 0,
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
      }
    }
  },
  "block": {
    "header": {
      "chain_id": "secret-1",
      "height": 1,
      "time": "2017-12-30T05:53:09.287+01:00",
      "num_txs": 0,
      "last_block_id": {
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "parts": {
          "total": 0,
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
        }
      },
      "total_txs": 35,
      "last_commit_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "data_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "next_validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "consensus_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "app_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "last_results_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "evidence_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "proposer_address": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27",
      "version": {
        "block": 10,
        "app": 0
      }
    },
    "txs": [
      "string"
    ],
    "evidence": [
      "string"
    ],
    "last_commit": {
      "block_id": {
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "parts": {
          "total": 0,
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
        }
      },
      "precommits": [
        {
          "validator_address": "string",
          "validator_index": "0",
          "height": "0",
          "round": "0",
          "timestamp": "2017-12-30T05:53:09.287+01:00",
          "type": 2,
          "block_id": {
            "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
            "parts": {
              "total": 0,
              "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
            }
          },
          "signature": "7uTC74QlknqYWEwg7Vn6M8Om7FuZ0EO4bjvuj6rwH1mTUJrRuMMZvAAqT9VjNgP0RA/TDp6u/92AqrZfXJSpBQ=="
        }
      ]
    }
  }
}
```

### `GET/blocks/{height}` <a id="get-blocks-height"></a>

**Description**

Get a block at a certain height

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **height** | number \* required | Block height |

**Example JSON Output**

```javascript
{
  "block_meta": {
    "header": {
      "chain_id": "secret-1",
      "height": 1,
      "time": "2017-12-30T05:53:09.287+01:00",
      "num_txs": 0,
      "last_block_id": {
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "parts": {
          "total": 0,
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
        }
      },
      "total_txs": 35,
      "last_commit_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "data_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "next_validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "consensus_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "app_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "last_results_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "evidence_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "proposer_address": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27",
      "version": {
        "block": 10,
        "app": 0
      }
    },
    "block_id": {
      "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "parts": {
        "total": 0,
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
      }
    }
  },
  "block": {
    "header": {
      "chain_id": "secret-1",
      "height": 1,
      "time": "2017-12-30T05:53:09.287+01:00",
      "num_txs": 0,
      "last_block_id": {
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "parts": {
          "total": 0,
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
        }
      },
      "total_txs": 35,
      "last_commit_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "data_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "next_validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "consensus_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "app_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "last_results_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "evidence_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
      "proposer_address": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27",
      "version": {
        "block": 10,
        "app": 0
      }
    },
    "txs": [
      "string"
    ],
    "evidence": [
      "string"
    ],
    "last_commit": {
      "block_id": {
        "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "parts": {
          "total": 0,
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
        }
      },
      "precommits": [
        {
          "validator_address": "string",
          "validator_index": "0",
          "height": "0",
          "round": "0",
          "timestamp": "2017-12-30T05:53:09.287+01:00",
          "type": 2,
          "block_id": {
            "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
            "parts": {
              "total": 0,
              "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
            }
          },
          "signature": "7uTC74QlknqYWEwg7Vn6M8Om7FuZ0EO4bjvuj6rwH1mTUJrRuMMZvAAqT9VjNgP0RA/TDp6u/92AqrZfXJSpBQ=="
        }
      ]
    }
  }
}
```

### `GET/validatorsets/latest` <a id="get-validatorsets-latest"></a>

**Description**

Get the latest validator set

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "block_height": "string",
  "validators": [
    {
      "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
      "pub_key": "secretvalconspub1zcjduepq0vu2zgkgk49efa0nqwzndanq5m4c7pa3u4apz4g2r9gspqg6g9cs3k9cuf",
      "voting_power": "1000",
      "proposer_priority": "1000"
    }
  ]
}
```

### `GET/validatorsets/{height}` <a id="get-validatorsets-height"></a>

**Description**

Get a validator set a certain height

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **height** | number \* required | Block height |

**Example JSON Output**

```javascript
{
  "block_height": "string",
  "validators": [
    {
      "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
      "pub_key": "secretvalconspub1zcjduepq0vu2zgkgk49efa0nqwzndanq5m4c7pa3u4apz4g2r9gspqg6g9cs3k9cuf",
      "voting_power": "1000",
      "proposer_priority": "1000"
    }
  ]
}
```

## **Authentication** <a id="authentication"></a>

**Authenticate accounts**

### `GET/auth/accounts/{address}` <a id="get-auth-accounts-address"></a>

**Description**

Get the account information on blockchain

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address |

**Example JSON Output**

```javascript
{
  "type": "string",
  "value": {
    "account_number": "string",
    "address": "string",
    "coins": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "public_key": {
      "type": "string",
      "value": "string"
    },
    "sequence": "string"
  }
}
```

## **Bank** <a id="bank"></a>

**Create and broadcast transactions**

### `GET/bank/balances/{address}` <a id="get-bank-balances-address"></a>

**Description**

Get the account balances

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address \_\*\*\_in bech32 format |

**Example JSON Output**

```javascript
[
  {
    "denom": "stake",
    "amount": "50"
  }
]
```

### `POST/bank/accounts/{address}/transfers` <a id="post-bank-accounts-address-transfers"></a>

**Description**

Send coins from one account to another

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address in bech32 format |
| **account** | object \* required | The sender and transaction information |

**Example JSON Output**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "amount": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ]
}
```

## **Staking** <a id="staking"></a>

**Stake module APIs**

### `GET/staking/delegators/{delegatorAddr}​/delegations` <a id="get-staking-delegators-delegatoraddr-delegations"></a>

**Description**

Get all delegations from a delegator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_address": "string",
    "shares": "string",
    "balance": {
      "denom": "stake",
      "amount": "50"
    }
  }
]
```

### `POST/staking/delegators/{delegatorAddr}​/delgations` <a id="post-staking-delegators-delegatoraddr-delgations"></a>

**Description**

Submit delegation

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegation** | object | The password of the account to remove from the KMS |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/staking/delegators/{delegatorAddr}​/delegations/{validatorAddr}` <a id="get-staking-delegators-delegatoraddr-delegations-validatoraddr"></a>

**Description**

Query the current delegation between a delegator and a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
{
  "delegator_address": "string",
  "validator_address": "string",
  "shares": "string",
  "balance": {
    "denom": "stake",
    "amount": "50"
  }
}
```

### `GET/staking/delegators/{delegatorAddr}/unbonding_delegations` <a id="get-staking-delegators-delegatoraddr-unbonding_delegations"></a>

**Description**

Get all unbonding delegations

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |

**Example JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_address": "string",
    "initial_balance": "string",
    "balance": "string",
    "creation_height": 0,
    "min_time": 0
  }
]
```

### `POST/staking/delegators/{delegatorAddr}/unbonding_delegations` <a id="post-staking-delegators-delegatoraddr-unbonding_delegations"></a>

**Description**

Submit an unbonding delegation

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegation** | object | The password of the account to remove from the KMS |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/staking/delegators/{delegatorAddr}/unbonding_delegations/ {validatorAddr}` <a id="get-staking-delegators-delegatoraddr-unbonding_delegations-validatoraddr"></a>

**Description**

Query all unbonding delegations between a delegator and a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
{
  "delegator_address": "string",
  "validator_address": "string",
  "entries": [
    {
      "initial_balance": "string",
      "balance": "string",
      "creation_height": "string",
      "min_time": "string"
    }
  ]
}
```

### `GET/staking/redelegations` <a id="get-staking-redelegations"></a>

**Description**

Get all redelegations \(filter by query params\)

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegator** | string | Bech32 AccAddress of Delegator |
| **validator\_from** | string | Bech32 ValAddress of SrcValidator |
| **validator\_to** | string | Bech32 ValAddress of DstValidator |

**Example JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_src_address": "string",
    "validator_dst_address": "string",
    "entries": [
      null
    ]
  }
]
```

### `POST/staking/delegators/{delegatorAddr}​/redelegations` <a id="post-staking-delegators-delegatoraddr-redelegations"></a>

**Description**

Submit a redelegation

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegation** | object | The sender and transaction information |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/staking/delegators/{delegatorAddr}​/validators` <a id="get-staking-delegators-delegatoraddr-validators"></a>

**Description**

Query all validators that a delegator is bonded to

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example JSON Output**

```javascript
[
  {
    "operator_address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
    "consensus_pubkey": "secretvalconspub1zcjduepq0vu2zgkgk49efa0nqwzndanq5m4c7pa3u4apz4g2r9gspqg6g9cs3k9cuf",
    "jailed": true,
    "status": 0,
    "tokens": "string",
    "delegator_shares": "string",
    "description": {
      "moniker": "string",
      "identity": "string",
      "website": "string",
      "security_contact": "string",
      "details": "string"
    },
    "bond_height": "0",
    "bond_intra_tx_counter": 0,
    "unbonding_height": "0",
    "unbonding_time": "1970-01-01T00:00:00Z",
    "commission": {
      "rate": "0",
      "max_rate": "0",
      "max_change_rate": "0",
      "update_time": "1970-01-01T00:00:00Z"
    }
  }
]
```

### `GET/staking/delegators/{delegatorAddr}/validators/{validatorAddr}` <a id="get-staking-delegators-delegatoraddr-validators-validatoraddr"></a>

**Description**

Query a validator that a delegator is bonded to

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 ValAddress of Delegator |

**Example JSON Output**

```javascript
{
  "operator_address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
  "consensus_pubkey": "secretvalconspub1zcjduepq0vu2zgkgk49efa0nqwzndanq5m4c7pa3u4apz4g2r9gspqg6g9cs3k9cuf",
  "jailed": true,
  "status": 0,
  "tokens": "string",
  "delegator_shares": "string",
  "description": {
    "moniker": "string",
    "identity": "string",
    "website": "string",
    "security_contact": "string",
    "details": "string"
  },
  "bond_height": "0",
  "bond_intra_tx_counter": 0,
  "unbonding_height": "0",
  "unbonding_time": "1970-01-01T00:00:00Z",
  "commission": {
    "rate": "0",
    "max_rate": "0",
    "max_change_rate": "0",
    "update_time": "1970-01-01T00:00:00Z"
  }
}
```

### `GET/staking/validators` <a id="get-staking-validators"></a>

**Description**

Get all validator candidates. By default it returns only the bonded validators

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **status** | string | The validator bond status. Must be either 'bonded', 'unbonded', or 'unbonding' |
| **page** | integer | The page number |
| **limit** | integer | The maximum number of items per page |

**Example JSON Output**

```javascript
[
  {
    "operator_address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
    "consensus_pubkey": "secretvalconspub1zcjduepq0vu2zgkgk49efa0nqwzndanq5m4c7pa3u4apz4g2r9gspqg6g9cs3k9cuf",
    "jailed": true,
    "status": 0,
    "tokens": "string",
    "delegator_shares": "string",
    "description": {
      "moniker": "string",
      "identity": "string",
      "website": "string",
      "security_contact": "string",
      "details": "string"
    },
    "bond_height": "0",
    "bond_intra_tx_counter": 0,
    "unbonding_height": "0",
    "unbonding_time": "1970-01-01T00:00:00Z",
    "commission": {
      "rate": "0",
      "max_rate": "0",
      "max_change_rate": "0",
      "update_time": "1970-01-01T00:00:00Z"
    }
  }
]
```

### `GET/staking/validators/{validatorAddr}` <a id="get-staking-validators-validatoraddr"></a>

**Description**

Query the information from a single validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
{
  "operator_address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
  "consensus_pubkey": "secretvalconspub1zcjduepq0vu2zgkgk49efa0nqwzndanq5m4c7pa3u4apz4g2r9gspqg6g9cs3k9cuf",
  "jailed": true,
  "status": 0,
  "tokens": "string",
  "delegator_shares": "string",
  "description": {
    "moniker": "string",
    "identity": "string",
    "website": "string",
    "security_contact": "string",
    "details": "string"
  },
  "bond_height": "0",
  "bond_intra_tx_counter": 0,
  "unbonding_height": "0",
  "unbonding_time": "1970-01-01T00:00:00Z",
  "commission": {
    "rate": "0",
    "max_rate": "0",
    "max_change_rate": "0",
    "update_time": "1970-01-01T00:00:00Z"
  }
}
```

### `GET/staking/validators/{validatorAddr}​/delegations` <a id="get-staking-validators-validatoraddr-delegations"></a>

**Description**

Get all delegations from a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_address": "string",
    "shares": "string",
    "balance": {
      "denom": "stake",
      "amount": "50"
    }
  }
]
```

### `GET/staking/validators{validatorAddr}/unbonding_delegations` <a id="get-staking-validators-validatoraddr-unbonding_delegations"></a>

**Description**

Get all unbonding delegations from a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_address": "string",
    "initial_balance": "string",
    "balance": "string",
    "creation_height": 0,
    "min_time": 0
  }
]
```

### `GET/staking/pool` <a id="get-staking-pool"></a>

**Description**

Get the current state of the staking pool

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "loose_tokens": "string",
  "bonded_tokens": "string",
  "inflation_last_time": "string",
  "inflation": "string",
  "date_last_commission_reset": "string",
  "prev_bonded_shares": "string"
}
```

### `GET/staking/parameters` <a id="get-staking-parameters"></a>

**Description**

Get the current staking parameter values

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "inflation_rate_change": "string",
  "inflation_max": "string",
  "inflation_min": "string",
  "goal_bonded": "string",
  "unbonding_time": "string",
  "max_validators": 0,
  "bond_denom": "string"
}
```

## **Governance** <a id="governance"></a>

**Governance module APIs**

### `POST/gov/proposals` <a id="post-gov-proposals"></a>

**Description**

Submit a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | object \* required | Valid value of `"proposal_type"` can be `"text"`, `"parameter_change"`, `"software_upgrade"` |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/gov/proposals` <a id="get-gov-proposals"></a>

**Description**

Query proposals

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **voter** | string | Transaction hash |
| **deposit** | string | Depositor address |
| **status** | string | Proposal status, valid values can be `"deposit_period"`, `"voting_period"`, `"passed"`, `"rejected"` |

**Example JSON Output**

```javascript
[
  {
    "proposal_id": 0,
    "title": "string",
    "description": "string",
    "proposal_type": "string",
    "proposal_status": "string",
    "final_tally_result": {
      "yes": "0.0000000000",
      "abstain": "0.0000000000",
      "no": "0.0000000000",
      "no_with_veto": "0.0000000000"
    },
    "submit_time": "string",
    "total_deposit": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "voting_start_time": "string"
  }
]
```

### `POST/gov/proposals/param_change` <a id="post-gov-proposals-param_change"></a>

**Description**

Generate a parameter change proposal transaction

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | object \* required | The parameter change proposal body that contains all parameter changes |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/gov/proposals/{proposalId}` <a id="get-gov-proposals-proposalid"></a>

**Description**

Query a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example JSON Output**

```javascript
{
  "proposal_id": 0,
  "title": "string",
  "description": "string",
  "proposal_type": "string",
  "proposal_status": "string",
  "final_tally_result": {
    "yes": "0.0000000000",
    "abstain": "0.0000000000",
    "no": "0.0000000000",
    "no_with_veto": "0.0000000000"
  },
  "submit_time": "string",
  "total_deposit": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ],
  "voting_start_time": "string"
}
```

### `GET/gov/proposals/{proposalId}/proposer` <a id="get-gov-proposals-proposalid-proposer"></a>

**Description**

Query a proposer

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example JSON Output**

```javascript
{
  "proposal_id": "string",
  "proposer": "string"
}
```

### `GET/gov/proposals/{proposalId}/deposits` <a id="get-gov-proposals-proposalid-deposits"></a>

**Description**

Query deposits \_\*\*\_by proposalID

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example JSON Output**

```javascript
[
  {
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "proposal_id": "string",
    "depositor": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27"
  }
]
```

### `POST/gov/proposals/{proposalId}/deposits` <a id="post-gov-proposals-proposalid-deposits"></a>

**Description**

Deposit tokens to a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| **post\_deposit\_body** | object \* required | ​ |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/gov/proposals/{proposalId}​/deposits/{depositor}` <a id="get-gov-proposals-proposalid-deposits-depositor"></a>

**Description**

Query deposit

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| depositor | string \* required | Bech32 depositor address |

**Example JSON Output**

```javascript
{
  "amount": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ],
  "proposal_id": "string",
  "depositor": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27"
}
```

### `GET/gov/proposals/{proposalId}/votes` <a id="get-gov-proposals-proposalid-votes"></a>

**Description**

Query voters

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example JSON Output**

```javascript
[
  {
    "voter": "string",
    "proposal_id": "string",
    "option": "string"
  }
]
```

### `POST/gov/proposals/{proposalId}/votes` <a id="post-gov-proposals-proposalid-votes"></a>

**Description**

Vote a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Transaction hash |
| **post\_vote\_body** | object \* required | Valid value of `"option"` field can be `"yes"`, `"no"`, `"no_with_veto"` and `"abstain"` |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/gov/proposals/{proposalId}/votes/{voter}` <a id="get-gov-proposals-proposalid-votes-voter"></a>

**Description**

Query vote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| **voter** | string \* required | Bech32 voter address |

**Example JSON Output**

```javascript
{
  "voter": "string",
  "proposal_id": "string",
  "option": "string"
}
```

### `GET/gov/proposals/{proposalId}/tally` <a id="get-gov-proposals-proposalid-tally"></a>

**Description**

Get a proposal's tally result at the current time

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example JSON Output**

```javascript
{
  "yes": "0.0000000000",
  "abstain": "0.0000000000",
  "no": "0.0000000000",
  "no_with_veto": "0.0000000000"
}
```

### `GET/gov/parameters/deposit` <a id="get-gov-parameters-deposit"></a>

**Description**

Query governance deposit parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "min_deposit": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ],
  "max_deposit_period": "86400000000000"
}
```

### `GET/gov/parameters/tallying` <a id="get-gov-parameters-tallying"></a>

**Description**

Query governance tally parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "threshold": "0.5000000000",
  "veto": "0.3340000000",
  "governance_penalty": "0.0100000000"
}
```

### `GET/gov/parameters/voting` <a id="get-gov-parameters-voting"></a>

**Description**

Query governance parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "voting_period": "86400000000000"
}
```

## **Slashing** <a id="slashing"></a>

**Slashing module APIs**

### `GET/slashing/signing_infos` <a id="get-slashing-signing_infos"></a>

**Description**

Get sign info of all given validators

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **page** | integer \* required | Page number |
| **limit** | integer \* required | Maximum number of items per page |

**Example JSON Output**

```javascript
[
  {
    "start_height": "string",
    "index_offset": "string",
    "jailed_until": "string",
    "missed_blocks_counter": "string"
  }
]
```

### `POST/slashing/validators/{validatorAddr}/unjail` <a id="post-slashing-validators-validatoraddr-unjail"></a>

**Description**

Unjail a jailed validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 validator address |
| **UnjailBody** | object \* required | ​ |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/slashing/parameters` <a id="get-slashing-parameters"></a>

**Description**

Get the current slashing parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "max_evidence_age": "string",
  "signed_blocks_window": "string",
  "min_signed_per_window": "string",
  "double_sign_unbond_duration": "string",
  "downtime_unbond_duration": "string",
  "slash_fraction_double_sign": "string",
  "slash_fraction_downtime": "string"
}
```

## **Distribution** <a id="distribution"></a>

**Fee distribution module APIs**

### `GET/distribution/delegators/{delegatorAddr}/rewards` <a id="get-distribution-delegators-delegatoraddr-rewards"></a>

**Description**

Get the total rewards balance from all delegations

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example JSON Output**

```javascript
{
  "rewards": [
    {
      "validator_address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
      "reward": [
        {
          "denom": "stake",
          "amount": "50"
        }
      ]
    }
  ],
  "total": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ]
}
```

### `POST/distribution/delegators/{delegatorAddr}/rewards` <a id="post-distribution-delegators-delegatoraddr-rewards"></a>

**Description**

Withdraw all the delegator's delegation rewards

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **Withdraw request body** | body | ​ |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/distribution/delegators/{delegatorAddr}/rewards/{validatorAddr}` <a id="get-distribution-delegators-delegatoraddr-rewards-validatoraddr"></a>

**Description**

Query a delegation reward

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
[
  {
    "denom": "stake",
    "amount": "50"
  }
]
```

### `POST/distribution/delegators/{delegatorAddr}​/rewards/{validatorAddr}` <a id="post-distribution-delegators-delegatoraddr-rewards-validatoraddr"></a>

**Description**

Withdraw a delegation reward

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |
| **Withdraw request body** | body | ​ |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/distribution/delegators/{delegatorAddr}/withdraw_address` <a id="get-distribution-delegators-delegatoraddr-withdraw_address"></a>

**Description**

Get the rewards withdrawal address

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27
```

### `POST/distribution/delegators/{delegatorAddr}/withdraw_address` <a id="post-distribution-delegators-delegatoraddr-withdraw_address"></a>

**Description**

Replace the rewards withdrawal address

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **Withdraw request body** | body | ​ |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/distribution/validators/{validatorAddr}` <a id="get-distribution-validators-validatoraddr"></a>

**Description**

Validator distribution information

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
{
  "operator_address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
  "self_bond_rewards": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ],
  "val_commission": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ]
}
```

### `GET/distribution/validators/{validatorAddr}/outstanding_rewards` <a id="get-distribution-validators-validatoraddr-outstanding_rewards"></a>

**Description**

Fee distribution outstanding rewards of a single validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
[
  {
    "denom": "stake",
    "amount": "50"
  }
]
```

### `GET/distribution/validators/{validatorAddr}/rewards` <a id="get-distribution-validators-validatoraddr-rewards"></a>

**Description**

Commission and self-delegation rewards of a single validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example JSON Output**

```javascript
[
  {
    "denom": "stake",
    "amount": "50"
  }
]
```

### `POST/distribution/validators/{validatorAddr}/rewards` <a id="post-distribution-validators-validatoraddr-rewards"></a>

**Description**

Withdraw the validator's rewards

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| validatorAddr | string \* required | Bech32 OperatorAddress of validator |
| **Withdraw request body** | body | ​ |

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/distribution/community_pool` <a id="get-distribution-community_pool"></a>

**Description**

Community pool parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
[
  {
    "denom": "stake",
    "amount": "50"
  }
]
```

### `GET/distribution/parameters` <a id="get-distribution-parameters"></a>

**Description**

Fee distribution parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "base_proposer_reward": "string",
  "bonus_proposer_reward": "string",
  "community_tax": "string"
}
```

## **IBC** <a id="supply"></a>

**IBC module APIs**

### `GET/ibc/clients/{client-id}/consensus-state`

**Description**

Query client consensus-state

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "consensus_state": {
    "chain_id": "string",
    "height": 0,
    "root": {
      "type": "string",
      "value": {
        "hash": "string"
      }
    },
    "next_validator_set": {
      "validators": [
        {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      ],
      "proposer": {
        "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
        "pub_key": {
          "type": "string",
          "value": "string"
        },
        "voting_power": "1000",
        "proposer_priority": "1000"
      }
    }
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `GET/ibc/clients/{client-id}/client-state`

**Description**

Query client state

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "client_state": {
    "id": "string",
    "frozen": true
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `GET/ibc/clients/{client-id}/roots/{height}`

**Description**

Query client root

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **height** | number \* required | Root height |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "root": {
    "type": "string",
    "value": {
      "hash": "string"
    }
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `GET/ibc/header`

**Description**

Query header

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "type": "string",
  "value": {
    "SignedHeader": {
      "header": {
        "chain_id": "secret-1",
        "height": 1,
        "time": "2017-12-30T05:53:09.287+01:00",
        "num_txs": 0,
        "last_block_id": {
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "parts": {
            "total": 0,
            "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
          }
        },
        "total_txs": 35,
        "last_commit_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "data_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "next_validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "consensus_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "app_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "last_results_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "evidence_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
        "proposer_address": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27",
        "version": {
          "block": 10,
          "app": 0
        }
      },
      "commit": {
        "block_id": {
          "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "parts": {
            "total": 0,
            "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
          }
        },
        "precommits": [
          {
            "validator_address": "string",
            "validator_index": "0",
            "height": "0",
            "round": "0",
            "timestamp": "2017-12-30T05:53:09.287+01:00",
            "type": 2,
            "block_id": {
              "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
              "parts": {
                "total": 0,
                "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
              }
            },
            "signature": "7uTC74QlknqYWEwg7Vn6M8Om7FuZ0EO4bjvuj6rwH1mTUJrRuMMZvAAqT9VjNgP0RA/TDp6u/92AqrZfXJSpBQ=="
          }
        ]
      }
    },
    "validator_set": {
      "validators": [
        {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      ],
      "proposer": {
        "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
        "pub_key": {
          "type": "string",
          "value": "string"
        },
        "voting_power": "1000",
        "proposer_priority": "1000"
      }
    },
    "next_validator_set": {
      "validators": [
        {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      ],
      "proposer": {
        "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
        "pub_key": {
          "type": "string",
          "value": "string"
        },
        "voting_power": "1000",
        "proposer_priority": "1000"
      }
    }
  }
}
```

### `GET/ibc/node-state`

**Description**

Query node consensus-state

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "chain_id": "string",
  "height": 0,
  "root": {
    "type": "string",
    "value": {
      "hash": "string"
    }
  },
  "next_validator_set": {
    "validators": [
      {
        "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
        "pub_key": {
          "type": "string",
          "value": "string"
        },
        "voting_power": "1000",
        "proposer_priority": "1000"
      }
    ],
    "proposer": {
      "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
      "pub_key": {
        "type": "string",
        "value": "string"
      },
      "voting_power": "1000",
      "proposer_priority": "1000"
    }
  }
}
```

### `GET/ibc/path`

**Description**

Query IBC path

**Parameters**

No parameters

**Example JSON Output**

```javascript
string
```

### `POST/ibc/clients`

**Description**

Create client

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **Create client request body** | object \* required | Body |

**Request Example**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "client_id": "string",
  "consensus_state": {
    "type": "string",
    "value": {
      "chain_id": "string",
      "height": 0,
      "root": {
        "type": "string",
        "value": {
          "hash": "string"
        }
      },
      "next_validator_set": {
        "validators": [
          {
            "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
            "pub_key": {
              "type": "string",
              "value": "string"
            },
            "voting_power": "1000",
            "proposer_priority": "1000"
          }
        ],
        "proposer": {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      }
    }
  }
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/clients/{client-id}/update`

**Description**

Update client

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **Update client request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "header": {
    "type": "string",
    "value": {
      "SignedHeader": {
        "header": {
          "chain_id": "secret-1",
          "height": 1,
          "time": "2017-12-30T05:53:09.287+01:00",
          "num_txs": 0,
          "last_block_id": {
            "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
            "parts": {
              "total": 0,
              "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
            }
          },
          "total_txs": 35,
          "last_commit_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "data_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "next_validators_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "consensus_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "app_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "last_results_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "evidence_hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
          "proposer_address": "secret1depk54cuajgkzea6zpgkq36tnjwdzv4afc3d27",
          "version": {
            "block": 10,
            "app": 0
          }
        },
        "commit": {
          "block_id": {
            "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
            "parts": {
              "total": 0,
              "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
            }
          },
          "precommits": [
            {
              "validator_address": "string",
              "validator_index": "0",
              "height": "0",
              "round": "0",
              "timestamp": "2017-12-30T05:53:09.287+01:00",
              "type": 2,
              "block_id": {
                "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04",
                "parts": {
                  "total": 0,
                  "hash": "EE5F3404034C524501629B56E0DDC38FAD651F04"
                }
              },
              "signature": "7uTC74QlknqYWEwg7Vn6M8Om7FuZ0EO4bjvuj6rwH1mTUJrRuMMZvAAqT9VjNgP0RA/TDp6u/92AqrZfXJSpBQ=="
            }
          ]
        }
      },
      "validator_set": {
        "validators": [
          {
            "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
            "pub_key": {
              "type": "string",
              "value": "string"
            },
            "voting_power": "1000",
            "proposer_priority": "1000"
          }
        ],
        "proposer": {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      },
      "next_validator_set": {
        "validators": [
          {
            "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
            "pub_key": {
              "type": "string",
              "value": "string"
            },
            "voting_power": "1000",
            "proposer_priority": "1000"
          }
        ],
        "proposer": {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      }
    }
  }
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/clients/{client-id}/misbehavior`

**Description**

Submit misbehaviour

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **Submit misbehaviour request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "evidence": {
    "type": "string",
    "value": {
      "DuplicateVoteEvidence": "string",
      "chain_id": "string",
      "val_power": 0,
      "total_power": 0
    }
  }
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/ibc/connections`

**Description**

Query all connections

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **page** | integer | Page number |
| **limit** | integer | Maximum number of items per page |

**Example JSON Output**

```javascript
[
  {
    "id": "connectionidone",
    "state": "OPEN",
    "client_id": "clientidone",
    "counterparty": {
      "client_id": "string",
      "connection_id": "string",
      "prefix": {
        "key_prefix": "string"
      }
    },
    "versions": [
      "1.0.0"
    ]
  }
]
```

### `GET/ibc/cconnections/{connection-id}`

**Description**

Query connection

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **connection-id** | string \* required | Connection ID |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "connection": {
    "id": "connectionidone",
    "state": "OPEN",
    "client_id": "clientidone",
    "counterparty": {
      "client_id": "string",
      "connection_id": "string",
      "prefix": {
        "key_prefix": "string"
      }
    },
    "versions": [
      "1.0.0"
    ]
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `GET/ibc/clients/{client-id}/connections`

**Description**

Query connections of a client

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "connection_paths": [
    "string"
  ],
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `POST/ibc/connections/open-init`

**Description**

Connection open-init

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **Connection open-init request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "connection_id": "string",
  "client_id": "string",
  "counterparty_client_id": "string",
  "counterparty_connection_id": "string",
  "counterparty_prefix": {
    "type": "string",
    "value": {
      "key_prefix": "string"
    }
  }
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/connections/open-try`

**Description**

Connection open-try

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **Connection open-try request body** | object \* required | Body |

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "connection_id": "string",
  "client_id": "string",
  "counterparty_client_id": "string",
  "counterparty_connection_id": "string",
  "counterparty_prefix": {
    "type": "string",
    "value": {
      "key_prefix": "string"
    }
  },
  "counterparty_versions": [
    "string"
  ],
  "proof_init": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_consensus": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_height": 0,
  "consensus_height": 0
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/connections/{connection-id}/open-ack`

**Description**

Connection open-ack

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **connection-id** | string \* required | Connection ID |
| **Connection open-ack request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "proof_try": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_consensus": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_height": 0,
  "consensus_height": 0,
  "version": "string"
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/connections/{connection-id}/open-confirm`

**Description**

Query client consensus-state

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **client-id** | string \* required | Client ID |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "consensus_state": {
    "chain_id": "string",
    "height": 0,
    "root": {
      "type": "string",
      "value": {
        "hash": "string"
      }
    },
    "next_validator_set": {
      "validators": [
        {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      ],
      "proposer": {
        "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
        "pub_key": {
          "type": "string",
          "value": "string"
        },
        "voting_power": "1000",
        "proposer_priority": "1000"
      }
    }
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `GET/ibc/ports/{port-id}/channels/{channel-id}`

**Description**

Query channel

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |
| **prove** | boolean | Proof of result |

**Example JSON Output**

```javascript
{
  "channel": {
    "state": "string",
    "ordering": "string",
    "connection_hops": [
      "string"
    ],
    "version": "string"
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `POST/ibc/channels/open-init`

**Description**

Channel open-init

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **Channel open-init request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "port_id": "string",
  "channel_id": "string",
  "version": "string",
  "channel_order": "string",
  "connection_hops": [
    "string"
  ],
  "counterparty_port_id": "string",
  "counterparty_channel_id": "string"
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/channels/open-try`

**Description**

Channel open-try

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **Channel open-try request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "port_id": "string",
  "channel_id": "string",
  "version": "string",
  "channel_order": "string",
  "connection_hops": [
    "string"
  ],
  "counterparty_port_id": "string",
  "counterparty_channel_id": "string",
  "counterparty_version": "string",
  "proof_init": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_height": 0
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/ports/{port-id}/channels/{channel-id}/open-ack`

**Description**

Channel open-ack

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |
| **Channel open-ack request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "counterparty_version": "string",
  "proof_try": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_height": 0
}
```

**Example JSON Output**

```javascript
{
  "consensus_state": {
    "chain_id": "string",
    "height": 0,
    "root": {
      "type": "string",
      "value": {
        "hash": "string"
      }
    },
    "next_validator_set": {
      "validators": [
        {
          "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
          "pub_key": {
            "type": "string",
            "value": "string"
          },
          "voting_power": "1000",
          "proposer_priority": "1000"
        }
      ],
      "proposer": {
        "address": "secretvaloper16xyempempp92x9hyzz9wrgf94r6j9h5f2w4n2l",
        "pub_key": {
          "type": "string",
          "value": "string"
        },
        "voting_power": "1000",
        "proposer_priority": "1000"
      }
    }
  },
  "proof": {
    "proof": {
      "ops": [
        {
          "type": "string",
          "key": "string",
          "data": "string"
        }
      ]
    }
  },
  "proof_path": {
    "key_path": [
      {
        "name": "string",
        "enc": 0
      }
    ]
  },
  "proof_height": 0
}
```

### `POST/ibc/ports/{port-id}/channels/{channel-id}/open-confirm`

**Description**

Channel open-confirm

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |
| **Channel open-confirm request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "proof_ack": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_height": 0
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/ports/{port-id}/channels/{channel-id}/open-confirm`

**Description**

Channel close-init

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |
| **Channel close-init request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  }
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/ports/{port-id}/channels/{channel-id}/close-confirm`

**Description**

Channel close-confirm

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |
| **Channel close-confirm request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "proof_init": {
    "type": "string",
    "value": {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  },
  "proof_height": 0
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `GET/ibc/ports/{port-id}/channels/{channel-id}/next-sequence-recv`

**Description**

Query next sequence receive

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |

**Example JSON Output**

```javascript
OK
```

### `POST/ibc/ports/{port-id}/channels/{channel-id}/transfer`

**Description**

Transfer token

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **port-id** | string \* required | Port ID |
| **channel-id** | string \* required | Channel ID |
| **Transfer token request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "amount": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ],
  "receiver": "string",
  "source": true
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

### `POST/ibc/packets/receive`

**Description**

Receive packet

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **Receive packet request body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "secret1g9ahr6xhht5rmqven628nklxluzyv8z9jqjcmc",
    "memo": "Sent via Enigma",
    "chain_id": "secret-1",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "packet": {
    "type": "string",
    "value": {
      "sequence": 0,
      "timeout": 0,
      "source_port": "string",
      "source_channel": "string",
      "destination_port": "string",
      "destination_channel": "string",
      "data": "string"
    }
  },
  "proofs": [
    {
      "proof": {
        "ops": [
          {
            "type": "string",
            "key": "string",
            "data": "string"
          }
        ]
      }
    }
  ],
  "height": 0
}
```

**Example JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "stake",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  ]
}
```

## **Supply** <a id="supply"></a>

**Supply module APIs**

### `GET/supply/total` <a id="get-supply-total"></a>

**Description**

Total supply of coins in the chain

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "total": [
    {
      "denom": "stake",
      "amount": "50"
    }
  ]
}
```

### `GET/supply/total/{denomination}` <a id="get-supply-total-denomination"></a>

**Description**

Total supply of a single coin denomination

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denomination** | string \* required | Coin denomination |

**Example JSON Output**

```text
string
```

## **Mint** <a id="mint"></a>

**Minting module APIs**

### `GET/minting/parameters` <a id="get-minting-parameters"></a>

**Description**

Minting module parameters

**Parameters**

no parameters

**Example JSON Output**

```javascript
{
  "mint_denom": "string",
  "inflation_rate_change": "string",
  "inflation_max": "string",
  "inflation_min": "string",
  "goal_bonded": "string",
  "blocks_per_year": "string"
}
```

### `GET/minting/inflation` <a id="get-minting-inflation"></a>

**Description**

Current minting inflation value

**Parameters**

no parameters

**Example JSON Output**

```text
string
```

### `GET/minting/annual-provisions` <a id="get-minting-annual-provisions"></a>

**Description**

Current minting annual provisions value

**Parameters**

no parameters

**Example JSON Output**

```text
string
```

## **Secret Network REST**

### **`GET/node_info`**

**Description**

Information about the connected node

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "application_version": {
    "build_tags": "string",
    "client_name": "string",
    "commit": "string",
    "go": "string",
    "name": "string",
    "server_name": "string",
    "version": "string"
  },
  "node_info": {
    "id": "string",
    "moniker": "validator-name",
    "protocol_version": {
      "p2p": 7,
      "block": 10,
      "app": 0
    },
    "network": "secret-1",
    "channels": "string",
    "listen_addr": "192.168.56.1:26656",
    "version": "0.15.0",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  }
}
```

