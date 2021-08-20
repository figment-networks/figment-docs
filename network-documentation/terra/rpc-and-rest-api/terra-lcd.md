---
description: Learn how to interact with the Terra LCD
---

# Terra LCD

## Source documentation

[**The Terra LCD's source documentation can be found here**](https://lcd.terra.dev/swagger-ui/#/).

A REST interface for state queries, transaction generation, and broadcasting.

## **Transactions**

**Search, encode, or broadcast transactions.**

### `GET/txs/{hash}`

**Description**

Get a transaction by hash

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **hash** | string \* required | Transaction hash |

**Example** \_\_**JSON Output**

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
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signature": {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
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

### `GET/txs`

**Description**

Search Transactions

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **message.action** | string | Transaction events such as 'message.action=send' which results in the following /txs?message.action=send' |
| **message.sender** | string | Transaction tags with sender: 'GET /txs message.action=send&message.sender=cosmos16xyempempp92x9hyzz9wrgf94r6j9h5f06pxxv' |
| **page** | integer | Page number |
| **limit** | integer | Maximum number of items per page |
| **tx.minheight** | integer | Transactions on blocks with height greater or equal this value |
| **tx.maxheight** | integer | Transactions on blocks with height less than or equal this value |

**Example** \_\_**JSON Output**

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
              "denom": "uluna",
              "amount": "50"
            }
          ]
        },
        "memo": "string",
        "signature": {
          "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
          "pub_key": {
            "type": "tendermint/PubKeySecp256k1",
            "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
          },
          "account_number": "0",
          "sequence": "0"
        }
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

### `POST/txs`

**Description**

Broadcast a signed transaction

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **txBroadcast** | object | The transaction must be signed _\*\*_ StdTx. The supported broadcast modes include `"block"`\(return after tx commit\), `"sync"`\(return afer CheckTx\) and `"async"`\(return right away\). |

**Example Request**

```javascript
{
  "tx": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signature": {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  },
  "mode": "block"
}
```

**Example** \_\_**JSON Output**

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

### `POST/txs/encode`

**Description**

Encode a transaction to the Amino wire format

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **tx** | object | The transaction to encode |

**Example Request**

```javascript
{
  "tx": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signature": {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  }
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "tx": "The base64-encoded Amino-serialized bytes for the tx"
}
```

### `POST/txs/estimate_fee`

**Description**

Estimate fees and gas of a transaction

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **estimate\_req** | body \* required | The transaction and gas parameters to compute fee |

**Example Request**

```javascript
{
  "tx": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signature": {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  },
  "gas_adjustment": "1.4",
  "gas_prices": [
    {
      "denom": "ukrw",
      "amount": "50.000"
    }
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "fees": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "gas": "10000"
}
```

## **Tendermint RPC**

**Tendermint APIs, such as query blocks, transactions, and validator set**

### `GET/node_info`

**Description**

The properties of the connected node

**Parameters**

no parameters

**Example** \_\_**JSON Output**

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
    "network": "gaia-2",
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

### `GET/syncing`

**Description**

Syncing state of node

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "syncing": true
}
```

### `GET/blocks/latest`

**Description**

Get the latest block

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "block_meta": {
    "header": {
      "chain_id": "columbus-3",
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
      "proposer_address": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
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
      "chain_id": "columbus-3",
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
      "proposer_address": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
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

### `GET/blocks/{height}`

**Description**

Get a block at a certain height

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **height** | number \* required | Block height |

**Example** \_\_**JSON Output**

```javascript
{
  "block_meta": {
    "header": {
      "chain_id": "columbus-3",
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
      "proposer_address": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
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
      "chain_id": "columbus-3",
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
      "proposer_address": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
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

### `GET/validatorsets/latest`

**Description**

Get the latest validator set

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "block_height": "string",
  "validators": [
    {
      "address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
      "pub_key": "terravalconspub1zcjduepq7mft6gfls57a0a42d7uhx656cckhfvtrlmw744jv4q0mvlv0dypskehfk8",
      "voting_power": "1000",
      "proposer_priority": "1000"
    }
  ]
}
```

### `GET/validatorsets/{height}`

**Description**

Get a validator set a certain height

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **height** | number \* required | Block height |

**Example** \_\_**JSON Output**

```javascript
{
  "block_height": "string",
  "validators": [
    {
      "address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
      "pub_key": "terravalconspub1zcjduepq7mft6gfls57a0a42d7uhx656cckhfvtrlmw744jv4q0mvlv0dypskehfk8",
      "voting_power": "1000",
      "proposer_priority": "1000"
    }
  ]
}
```

## **Authentication**

**Authenticate accounts**

### `GET/auth/accounts/{address}`

**Description**

Get the account information on blockchain \_\_

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address |

**Example** \_\_**JSON Output**

```javascript
{
  "Account": {
    "type": "auth/Account",
    "value": {
      "account_number": "string",
      "address": "string",
      "coins": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ],
      "public_key": "string",
      "sequence": "string"
    }
  },
  "LazyGradedVestingAccount": {
    "type": "core/LazyGradedVestingAccount",
    "value": {
      "BaseVestingAccount": {
        "BaseAccount": {
          "account_number": "string",
          "address": "string",
          "coins": [
            {
              "denom": "uluna",
              "amount": "50"
            }
          ],
          "public_key": "string",
          "sequence": "string"
        },
        "original_vesting": [
          {
            "denom": "uluna",
            "amount": "50"
          }
        ],
        "delegated_free": [
          {
            "denom": "uluna",
            "amount": "50"
          }
        ],
        "delegated_vesting": [
          {
            "denom": "uluna",
            "amount": "50"
          }
        ],
        "end_time": "0"
      },
      "vesting_schedules": [
        {
          "denom": "usdr",
          "lazy_schedules": [
            {
              "start_time": "1556085600",
              "end_time": "1556085600",
              "ratio": "0.100000000000000000"
            }
          ]
        }
      ]
    }
  }
}
```

### `POST/auth/accounts/{address}/multisign`

**Description**

Generate multisig signatures for transactions generated offline

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address |
| **multisig\_req** | body \* required | Multisign request information; pubkey is an optional parameter in case multisig account is never used before |

**Example Request**

```javascript
{
  "tx": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signatures": null
  },
  "chain_id": "columbus-3",
  "signatures": [
    {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      }
    }
  ],
  "signature_only": true,
  "pubkey": {
    "threshold": 1,
    "pubkeys": [
      "terrapub1addwnpepq2l6pwj8h9fwxdjuge7lazu0sszpkck0nlhjag6q9drffrd93atywdt8ksu"
    ]
  }
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "MultiSignedTx": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signature": {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  },
  "MultiSig": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    }
  }
}
```

## **Bank**

**Create and broadcast transactions**

### `GET/bank/balances/{address}`

**Description**

Get the account balances

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "uluna",
    "amount": "50"
  }
]
```

### `POST/bank/accounts/{address}/transfers`

**Description**

Send coins from one account to another

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Account address in bech32 format |
| **account** | object \* required | The sender and transaction information |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "coins": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

## **Staking**

**Stake module APIs**

### `GET/staking/delegators/{delegatorAddr}/delegations`

**Description**

Get all delegations from a delegator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "delegator_address": "terra1pdx498r0hrc2fj36sjhs8vuhrz9hd2cw0tmam9",
    "validator_address": "terravaloper1pdx498r0hrc2fj36sjhs8vuhrz9hd2cw0yhqtk",
    "shares": "1000000",
    "balance": "1000000"
  }
]
```

### `POST/staking/delegators/{delegatorAddr}/delegations`

**Description**

Submit delegation

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegation** | object | The password of the account to remove from the KMS _\*\*_ |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "delegator_address": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "validator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
  "amount": {
    "denom": "uluna",
    "amount": "50"
  }
}
```

**Example** \_\_**JSON Output**

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

### `GET/staking/delegators/{delegatorAddr}/delegations/{validatorAddr}`

**Description**

Query the current delegation between a delegator and a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
{
  "delegator_address": "terra1pdx498r0hrc2fj36sjhs8vuhrz9hd2cw0tmam9",
  "validator_address": "terravaloper1pdx498r0hrc2fj36sjhs8vuhrz9hd2cw0yhqtk",
  "shares": "1000000",
  "balance": "1000000"
}
```

### `GET/staking/delegators/{delegatorAddr}/unbonding_delegations`

**Description**

Get all unbonding delegations from a delegator.

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_address": "string",
    "entries": [
      {
        "initial_balance": "string",
        "balance": "string",
        "creation_height": "string",
        "completion_time": "string"
      }
    ]
  }
]
```

### `POST/staking/delegators/{delegatorAddr}/unbonding_delegations`

**Description**

Submit an unbonding delegation

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |
| **delegation** | object | Body |

**Example Request**

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

**Example** \_\_**JSON Output**

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

### `GET/staking/delegators/{delegatorAddr}/unbonding_delegations/{validatorAddr}`

**Description**

Query all unbonding delegations between a delegator and a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
{
  "delegator_address": "string",
  "validator_address": "string",
  "entries": [
    {
      "initial_balance": "string",
      "balance": "string",
      "creation_height": "string",
      "completion_time": "string"
    }
  ]
}
```

### `GET/staking/redelegations`

**Description**

Get all redelegations \(filter by query params\)

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech 32 AccAddress of Delegator |
| **validator\_from** | string | Bech32 ValAddress of SrcValidator |
| **validator\_to** | string | Bech32 ValAddress of DstValidator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_src_address": "string",
    "validator_dst_address": "string",
    "entries": [
      {
        "creation_height": 0,
        "completion_time": 0,
        "initial_balance": "string",
        "balance": "string",
        "shares_dst": "string"
      }
    ]
  }
]
```

### `GET/staking/delegators/{delegatorAddr}/validators`

**Description**

Query all validators that a delegator is bonded to

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "operator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
    "consensus_pubkey": "terravalconspub1zcjduepq7mft6gfls57a0a42d7uhx656cckhfvtrlmw744jv4q0mvlv0dypskehfk8",
    "jailed": true,
    "status": 0,
    "tokens": "string",
    "delegator_shares": "string",
    "description": {
      "moniker": "string",
      "identity": "string",
      "website": "string",
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

### `GET/staking/delegators/{delegatorAddr}/validators/{validatorAddr}`

**Description**

Query a validator that a delegator is bonded to

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 ValAddress of Delegator |

**Example** \_\_**JSON Output**

```javascript
{
  "operator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
  "consensus_pubkey": "terravalconspub1zcjduepq7mft6gfls57a0a42d7uhx656cckhfvtrlmw744jv4q0mvlv0dypskehfk8",
  "jailed": true,
  "status": 0,
  "tokens": "string",
  "delegator_shares": "string",
  "description": {
    "moniker": "string",
    "identity": "string",
    "website": "string",
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

### `GET/staking/delegators/{delegatorAddr}/txs`

**Description**

Get all staking transactions \(i.e. msgs\) from a delegator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example** \_\_**JSON Output**

```javascript
[
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
                "denom": "uluna",
                "amount": "50"
              }
            ]
          },
          "memo": "string",
          "signature": {
            "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
            "pub_key": {
              "type": "tendermint/PubKeySecp256k1",
              "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
            },
            "account_number": "0",
            "sequence": "0"
          }
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
]
```

### `GET/staking/validators`

**Description**

Get all validator candidates. By default it returns only the bonded validators

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **status** | string | The validator bond status. Must be either 'bonded', 'unbonded', or 'unbonding' |
| **page** | integer | The page number |
| **limit** | integer | The maximum number of items per page |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "operator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
    "consensus_pubkey": "terravalconspub1zcjduepq7mft6gfls57a0a42d7uhx656cckhfvtrlmw744jv4q0mvlv0dypskehfk8",
    "jailed": true,
    "status": 0,
    "tokens": "string",
    "delegator_shares": "string",
    "description": {
      "moniker": "string",
      "identity": "string",
      "website": "string",
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

### `GET/staking/validators/{validatorAddr}`

**Description**

Query the information from a single validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
{
  "operator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
  "consensus_pubkey": "terravalconspub1zcjduepq7mft6gfls57a0a42d7uhx656cckhfvtrlmw744jv4q0mvlv0dypskehfk8",
  "jailed": true,
  "status": 0,
  "tokens": "string",
  "delegator_shares": "string",
  "description": {
    "moniker": "string",
    "identity": "string",
    "website": "string",
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

### `GET/staking/validators/{validatorAddr}/delegations`

**Description**

Get all delegations from a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "delegator_address": "terra1pdx498r0hrc2fj36sjhs8vuhrz9hd2cw0tmam9",
    "validator_address": "terravaloper1pdx498r0hrc2fj36sjhs8vuhrz9hd2cw0yhqtk",
    "shares": "1000000",
    "balance": "1000000"
  }
]
```

### `GET/staking/validators/{validatorAddr}/unbonding_delegations`

**Description**

Get all unbonding delegations from a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "delegator_address": "string",
    "validator_address": "string",
    "entries": [
      {
        "initial_balance": "string",
        "balance": "string",
        "creation_height": "string",
        "completion_time": "string"
      }
    ]
  }
]
```

### `GET/staking/pool`

**Description**

Get the current state of the staking pool

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "bonded_tokens": "string",
  "not_bonded_tokens": "string"
}
```

### `GET/staking/parameters`

**Description**

Get the current staking parameter values

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "unbonding_time": "string",
  "max_validators": 0,
  "max_entries": 0,
  "bond_denom": "string"
}
```

## **Governance**

**Governance module APIs**

### `POST/gov/proposals`

**Description**

Submit a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | object \* required | Valid value of `"proposal_type"` can be `"text"`, `"parameter_change"`, `"software_upgrade"` |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "title": "string",
  "description": "string",
  "proposal_type": "text",
  "proposer": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "initial_deposit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/gov/proposals`

**Description**

Query proposals

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| voter | string | Voter address |
| **depositor** | string | Depositor address |
| **status** | string | Proposal status, valid values can be `"deposit_period"`, `"voting_period"`, `"passed"`, `"rejected"` |

**Example** \_\_**JSON Output**

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
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "voting_start_time": "string"
  }
]
```

### `POST/gov/proposals/param_change`

**Description**

Generate a parameter change proposal transaction

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | object \* required | The parameter change proposal body that contains all parameter changes |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "title": "string",
  "description": "string",
  "proposer": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "deposit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "changes": [
    {
      "subspace": "staking",
      "key": "MaxValidators",
      "subkey": "",
      "value": {}
    }
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `POST/gov/proposals/community_pool_spend`

**Description**

Grant community pool coins to contributor

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | body \* required | The community pool spend proposal body that contains receipient and reward info |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "title": "string",
  "description": "string",
  "proposer": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "deposit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "recipient": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "amount": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `POST/gov/proposals/tax_rate_update`

**Description**

Tax rate update proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | body \* required | The tax rate update body that contains new tax rate info |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "title": "string",
  "description": "string",
  "proposer": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "deposit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "tax_rate": "0.12"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `POST/gov/proposals/reward_weight_update`

**Description**

Reward weight update proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **post\_proposal\_body** | body \* required | The reward weight update body that contains new reward weight info |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "title": "string",
  "description": "string",
  "proposer": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "deposit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "reward_weight": "0.12"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/gov/proposals/{proposalId}`

**Description**

Query a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example** \_\_**JSON Output**

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
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "voting_start_time": "string"
}
```

### `GET/gov/proposals/{proposalId}/proposer`

**Description**

Query proposer

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example** \_\_**JSON Output**

```javascript
{
  "proposal_id": "string",
  "proposer": "string"
}
```

### `GET/gov/proposals/{proposalId}/deposits`

**Description**

Query deposits

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "proposal_id": "string",
    "depositor": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv"
  }
]
```

### `POST/gov/proposals/{proposalId}/deposits`

**Description**

Deposit tokens to a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| **post\_deposit\_body** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "depositor": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "amount": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

**Example** \_\_**JSON Output**

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

### `GET/gov/proposals/{proposalId}/deposits/{depositor}`

**Description**

Query deposit

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| **depositor** | string \* required | Bech32 depositor address |

**Example** \_\_**JSON Output**

```javascript
{
  "amount": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "proposal_id": "string",
  "depositor": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv"
}
```

### `GET/gov/proposals/{proposalId}/votes`

**Description**

Query voters

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "voter": "string",
    "proposal_id": "string",
    "option": "string"
  }
]
```

### `POST/gov/proposals/{proposalId}/votes`

**Description**

Vote a proposal

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| **post\_vote\_body** | object \* required | Valid value of `"option"` field can be `"yes"`, `"no"`, `"no_with_veto"` and `"abstain"` |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "voter": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
  "option": "yes"
}
```

**Example** \_\_**JSON Output**

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

### `GET/gov/proposals/{proposalId}/votes/{voter}`

**Description**

Query vote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |
| **voter** | string \* required | Bech32 voter address |

**Example** \_\_**JSON Output**

```javascript
{
  "voter": "string",
  "proposal_id": "string",
  "option": "string"
}
```

### `GET/gov/proposals/{proposalId}/tally`

**Description**

Get a proposal's tally result at the current time

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **proposalId** | string \* required | Proposal ID |

**Example** \_\_**JSON Output**

```javascript
{
  "yes": "0.0000000000",
  "abstain": "0.0000000000",
  "no": "0.0000000000",
  "no_with_veto": "0.0000000000"
}
```

### `GET/gov/parameters/deposit`

**Description**

Query governance deposit parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "min_deposit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "max_deposit_period": "86400000000000"
}
```

### `GET/gov/parameters/tallying`

**Description**

Query governance tally parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "quorum": "0.4000000000",
  "threshold": "0.5000000000",
  "veto": "0.3340000000"
}
```

### `GET/gov/parameters/voting`

**Description**

Query governance voting parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "voting_period": "86400000000000"
}
```

## **Slashing**

**Slashing module APIs**

### `GET/slashing/validators/{validatorPubKey}/signing_info`

**Description**

Get sign info of given validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **page** | integer \* required | Page number |
| **limit** | integer \* required | Maximum number of items per page |

**Example** \_\_**JSON Output**

```javascript
{
  "address": "terravalcons1qsdpq864szmfk8nh82qcg7lyle6k95w07acdqn",
  "start_height": "string",
  "index_offset": "string",
  "jailed_until": "string",
  "tombstoned": true,
  "missed_blocks_counter": "string"
}
```

### `GET/slashing/signing_infos`

**Description**

Get sign info of all given validators

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **page** | integer \* required | Page number |
| **limit** | integer \* required | Maximum number of items per page |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "address": "terravalcons1qsdpq864szmfk8nh82qcg7lyle6k95w07acdqn",
    "start_height": "string",
    "index_offset": "string",
    "jailed_until": "string",
    "tombstoned": true,
    "missed_blocks_counter": "string"
  }
]
```

### `POST/slashing/validators/{validatorAddr}/unjail`

**Description**

Unjail a jailed validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 validator address |
| **UnjailBody** | object \* required | Body |

**Example Request**

```javascript
{
  "base_req": {
    "msg": [
      "string"
    ],
    "fee": {
      "gas": "string",
      "amount": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    },
    "memo": "string",
    "signature": {
      "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
      },
      "account_number": "0",
      "sequence": "0"
    }
  }
}
```

**Example** \_\_**JSON Output**

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

### `GET/slashing/parameters`

**Description**

Get the current slashing parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "max_evidence_age": "string",
  "signed_blocks_window": "string",
  "min_signed_per_window": "string",
  "downtime_jail_duration": "string",
  "slash_fraction_double_sign": "string",
  "slash_fraction_downtime": "string"
}
```

## **Distribution**

**Fee distribution module APIs**

### `GET/distribution/delegators/{delegatorAddr}/rewards`

**Description**

Get the total rewards balance from all delegations _\*\*_

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |

**Example** \_\_**JSON Output**

```javascript
{
  "rewards": [
    {
      "validator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
      "reward": [
        {
          "denom": "uluna",
          "amount": "50"
        }
      ]
    }
  ],
  "total": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

### `POST/distribution/delegators/{delegatorAddr}/rewards`

**Description**

Withdraw all the delegator's delegation rewards

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **Withdraw request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  }
}
```

**Example** \_\_**JSON Output**

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

### `GET/distribution/delegators/{delegatorAddr}/rewards/{validatorAddr}`

**Description**

Query a delegation reward

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "uluna",
    "amount": "50"
  }
][
  {
    "denom": "uluna",
    "amount": "50"
  }
]
```

### `POST/distribution/delegators/{delegatorAddr}/rewards/{validatorAddr}`

**Description**

Withdraw a delegation reward

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |
| **Withdraw request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  }
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  }
}
```

### `GET/distribution/delegators/{delegatorAddr}/withdraw_address`

**Description**

Get the rewards withdrawal address

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv
```

### `POST/distribution/delegators/{delegatorAddr}/withdraw_address`

**Description**

Replace the rewards withdrawal address

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **delegatorAddr** | string \* required | Bech32 AccAddress of Delegator |
| **Withdraw request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "withdraw_address": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv"
}
```

**Example** \_\_**JSON Output**

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

### `GET/distribution/validators/{validatorAddr}`

**Description**

Validator distribution information

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
{
  "operator_address": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
  "self_bond_rewards": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "val_commission": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

### `GET/distribution/validators/{validatorAddr}/outstanding_rewards`

**Description**

Fee distribution outstanding rewards of a single validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "uluna",
    "amount": "50"
  }
]
```

### `GET/distribution/validators/{validatorAddr}/rewards`

**Description**

Commission and self-delegation rewards of a single validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddres of validator |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "uluna",
    "amount": "50"
  }
]
```

### `POST/distribution/validators/{validatorAddr}/rewards`

**Description**

Withdraw the validator's rewards

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validatorAddr** | string \* required | Bech32 OperatorAddress of validator |
| **Withdraw request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  }
}
```

**Example** \_\_**JSON Output**

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

### `GET/distribution/community_pool`

**Description**

Community pool parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "uluna",
    "amount": "50"
  }
]
```

### `GET/distribution/params`

**Description**

Fee distribution parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "base_proposer_reward": "string",
  "bonus_proposer_reward": "string",
  "community_tax": "string"
}
```

## **Supply**

**Supply module APIs**

### `GET/supply/total`

**Description**

Total supply of coins in the chain

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "total": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

### `GET/supply/total/{denomination}`

**Description**

Total supply of a single coin denomination

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denomination** | string \* required | Coin denomination |

**Example** \_\_**JSON Output**

```javascript
string
```

## **Market**

**Market modules APIs**

### `POST/market/swap`

**Description**

Swap coin with another coin _\*\*_

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **Swap coin request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "offer_coin": {
    "denom": "uluna",
    "amount": "50"
  },
  "ask_denom": "uluna",
  "receiver": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/market/swap`

**Description**

Query swap result amount

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **offer\_coin** | string \* required | Coin expression you want to swap |
| **ask\_denom** | string \* required | Then coin denomination you want to ask |

**Example** \_\_**JSON Output**

```javascript
{
  "denom": "uluna",
  "amount": "50"
}
```

### `GET/market/terra_pool_delta`

**Description**

Get Terra pool delta, the USDR amount used for swap operation from the TerraPool

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
10000000.00
```

### `GET/market/parameters`

**Description**

Get market parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "daily_luna_delta_limit": "0.005",
  "min_swap_spread": "0.02",
  "max_swap_spread": "0.1"
}
```

## **Oracle**

**Get price and voting modules APIs**

### `POST/oracle/denoms/{denom}/votes`

**Description**

Generate oracle exchange rate vote message containing exchange rate and salt for a prevote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to vote |
| **Vote request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "exchange_rate": "1000.0",
  "salt": "abcd",
  "validator": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/oracle/denoms/{denom}/votes`

**Description**

Get the currently unelected outstanding exchange rate oracle vote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to get |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "exchange_rate": "0.01241",
    "denom": "ukrw",
    "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l"
  }
]
```

### `GET/oracle/denoms/{denom}/votes/{validator}`

**Description**

Get the currently unelected outstanding exchange rate oracle vote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to get |
| **validator** | string \* required |  |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "exchange_rate": "0.01241",
    "denom": "ukrw",
    "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l"
  }
]
```

### `GET/oracle/voters/{validator}/votes`

**Description**

Get the currently outstanding exchange rate oracle votes of a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required |  |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "exchange_rate": "0.01241",
    "denom": "ukrw",
    "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l"
  }
]
```

### `POST/oracle/denoms/{denom}/prevotes`

**Description**

Generate oracle exchange rate prevote message containing hash of a vote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to prevote |
| **Vote request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "exchange_rate": "1000.0",
  "salt": "abcd",
  "hash": "061bf1e27dfff121f40c826e593c8a28ec299a02",
  "validator": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/oracle/denoms/{denom}/prevotes`

**Description**

Get the currently outstanding exchange rate oracle prevote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to get |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "hash": "061bf1e27dfff121f40c826e593c8a28ec299a02",
    "denom": "uusd",
    "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
    "submit_block": "1"
  }
]
```

### `GET/oracle/denoms/{denom}/prevotes/{validator}`

**Description**

Get the currently outstanding exchange rate oracle prevote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to get |
| **validator** | string \* required |  |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "hash": "061bf1e27dfff121f40c826e593c8a28ec299a02",
    "denom": "uusd",
    "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
    "submit_block": "1"
  }
]
```

### `GET/oracle/voters/{validator}/prevotes`

**Description**

Get the currently outstanding exchange rate oracle prevotes of a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required |  |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "hash": "061bf1e27dfff121f40c826e593c8a28ec299a02",
    "denom": "uusd",
    "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
    "submit_block": "1"
  }
]
```

### `GET/oracle/denoms/{denom}/exchange_rate`

**Description**

Get the current effective exchange rate in LUNA for the asset

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | The coin denomination to get |

**Example** \_\_**JSON Output**

```javascript
1872.000000000000000000
```

### `GET/oracle/denoms/exchange_rates`

**Description**

Get all activated exchange rates

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "ukrw",
    "amount": "50.000"
  }
]
```

### `GET/oracle/denoms/actives`

**Description**

Get all activated denoms

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
[
  "ukrw",
  "usdr"
]
```

### `POST/oracle/voters/{validator}/feeder`

**Description**

Generate oracle feeder right delegation message

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Feeder right delegator |
| **Feeder right delegation request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "feeder": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/oracle/voters/{validator}/feeder`

**Description**

Get delegated oracle feeder of a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Feeder right delegator |

**Example** \_\_**JSON Output**

```javascript
terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv
```

### `GET/oracle/voters/{validator}/miss`

**Description**

Get the number of vote periods missed in this oracle slash window

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Oracle operator |

**Example** \_\_**JSON Output**

```javascript
100
```

### **`POST/oracle/voters/`**`{validator}/aggregate_prevote`

**Description**

Generate oracle aggregate exchange rate prevote message containing a hash

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Oracle operator |
| **Aggregate prevote request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "exchange_rates": "1000.0ukrw,1.2uusd,0.99usdr",
  "salt": "abcd",
  "hash": "061bf1e27dfff121f40c826e593c8a28ec299a02"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/oracle/voters/{validator}/aggregate_prevote`

**Description**

Get the currently outstanding aggregate exchange rate oracle prevote of a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Oracle operator |

**Example** \_\_**JSON Output**

```javascript
{
  "hash": "061bf1e27dfff121f40c826e593c8a28ec299a02",
  "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l",
  "submit_block": "1"
}
```

### **`POST/oracle/voters/`**`{validator}/aggregate_vote`

**Description**

Generate oracle aggregate exchange rate vote message containing exchange rates to prove the aggregate prevote

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Oracle operator |
| **Aggregate vote request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "exchange_rates": "1000.0ukrw,1.2uusd,0.99usdr",
  "salt": "abcd"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/oracle/voters/{validator}/aggregate_vote`

**Description**

Get the currently outstanding aggregate exchange rate oracle vote of a validator

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **validator** | string \* required | Oracle operator |

**Example** \_\_**JSON Output**

```javascript
{
  "exchange_rates": [
    {
      "denom": "ukrw",
      "amount": "50.000"
    }
  ],
  "voter": "terravaloper1wg2mlrxdmnnkkykgqg4znky86nyrtc45q7a85l"
}
```

### `GET/oracle/parameters`

**Description**

Get oracle parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "vote_period": "900",
  "vote_threshold": "0.67",
  "drop_threshold": "10",
  "oracle_reward_band": "0.02"
}
```

## **Treasury**

**Treasury modules APIs**

### `GET/treasury/tax_rate`

**Description**

Get current tax rate

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
0.05
```

### `GET/treasury/tax_cap/{denom}`

**Description**

Get tax cap of the denom

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **denom** | string \* required | Denomination |

**Example** \_\_**JSON Output**

```javascript
100000
```

### `GET/treasury/reward_weight`

**Description**

Get current reward weight

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
0.05
```

### `GET/treasury/tax_proceeds`

**Description**

Get current tax proceeds

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
[
  {
    "denom": "uluna",
    "amount": "50"
  }
]
```

### `GET/treasury/seigniorage_proceeds`

**Description**

Retrieve the size of the seigniorage pool

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
0
```

### `GET/treasury/parameters`

**Description**

Get treasury module parameters

**Parameters**

no parameters

**Example** \_\_**JSON Output**

```javascript
{
  "tax_policy": {
    "rate_min": "0.0005",
    "rate_max": "0.01",
    "cap": {
      "denom": "uluna",
      "amount": "50"
    },
    "change_max": "0.00025"
  },
  "reward_policy": {
    "rate_min": "0.0005",
    "rate_max": "0.01",
    "cap": {
      "denom": "uluna",
      "amount": "50"
    },
    "change_max": "0.00025"
  },
  "seigniorage_burden_target": "0.67",
  "mining_increment": "1.07",
  "window_short": "4",
  "window_long": "52",
  "window_probation": "12",
  "oracle_share": "0.1",
  "budget_share": "0.9"
}
```

## Wasm

**Wasm modules APIs**

### **`POST/wasm/codes`**

**Description**

Generate wasm store code message

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **Store code request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "wasm_bytes": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `POST/wasm/codes/{codeID}`

**Description**

Instantiate wasm contract message

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **codeID** | number \* required | code ID you want to instantiate |
| Instantiate contract request body | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "init_coins": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "init_msg": "{}"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/wasm/codes/{codeID}`

**Description**

Get code info of the code ID

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **codeID** | number \* required | code ID you want to instantiate |

**Example** \_\_**JSON Output**

```javascript
{
  "code_hash": "string",
  "creator": "string"
}
```

### `POST/wasm/contracts/{contractAddress}`

**Description**

Execute wasm contract message

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **contractAddress** | string \* required | contract address you want to execute |
| **Execute contract request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "coins": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ],
  "exec_msg": "{}"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/wasm/contracts/{contractAddress}`

**Description**

Get contract info of the contract Address

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **contractAddress** | string \* required | contract address you want to execute |

**Example** \_\_**JSON Output**

```javascript
{
  "code_id": "string",
  "address": "string",
  "creator": "string",
  "init_msg": "string"
}
```

### `POST/wasm/contracts/{contractAddress}/migrate`

**Description**

Migrate wasm contract to new code base

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **contractAddress** | string \* required | contract address you want to migrate |
| **Migrate contract request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "new_code_id": 10,
  "migrate_msg": "{}"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `POST/wasm/contracts/{contractAddress}/owner`

**Description**

Update wasm contract owner to new address

**Parameters**

| **Parameters** | Type | Description |
| :--- | :--- | :--- |
| **contractAddress** | string \* required | contract address you want to update |
| **Update contract request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "new_owner": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv"
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/wasm/contracts/{contractAddress}/store`

**Description**

Retrieve the size of the seigniorage pool

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **contractAddress** | string \* required | contract address you want to lookup |
| **query\_msg** | string \* required | Get stored information with query msg |

**Example** \_\_**JSON Output**

```javascript
string
```

### `GET/wasm/contracts/{contractAddress}/store/raw`

**Description**

Get stored information with store key

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **contractAddress** | string \* required | contract address you want to lookup |
| **key** | string \* required | Raw key you want to query |
| **Subkey** | string | Raw subkey attached to the key |

**Example** \_\_**JSON Output**

```javascript
string
```

### `GET/wasm/parameters`

**Description**

Get wasm module parameters

**Parameters**

No parameters

**Example** \_\_**JSON Output**

```javascript
{
  "max_contract_size": "1000000",
  "max_contract_gas": "1000000",
  "max_contract_msg_size": "1000000",
  "gas_multiplier": "100"
}
```

## Authorization

Authorization modules APIs

### `GET/msgauth/granters/{granterAddress}/grantees/{granteeAddress}/grants`

**Description**

Get stored information with store key

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **granterAddress** | string \* required | Granter address you want to lookup |
| **granteeAddress** | string \* required | Grantee address you want to lookup |

**Example** \_\_**JSON Output**

```javascript
[
  {
    "GenericGrantInfo": {
      "authorization": {
        "type": "msgauth/GenericAuthorization",
        "value": {
          "msg_type": "send"
        }
      },
      "expiration": "2021-06-24T09:33:20.012999Z"
    },
    "SendGrantInfo": {
      "authorization": {
        "type": "msgauth/SendAuthorization",
        "value": {
          "spend_limit": [
            {
              "denom": "uluna",
              "amount": "50"
            }
          ]
        }
      },
      "expiration": "2021-06-24T09:33:20.012999Z"
    }
  }
]
```

### `POST/msgauth/granters/{granterAddress}/grantees/{granteeAddress}/grants/{msgType}`

**Description**

Grant message execute permission to grantee address

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **granterAddress** | string \* required | Granter address you want to lookup |
| **granteeAddress** | string \* required | Grantee address you want to lookup |
| **msgType** | string \* required | Message type you want to execute |
| **Grant request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "period": "3600000000000",
  "limit": [
    {
      "denom": "uluna",
      "amount": "50"
    }
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### `GET/msgauth/granters/{granterAddress}/grantees/{granteeAddress}/grants/{msgType}`

**Description**

Get grant about a specific msg type between the granter and the grantee

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **granterAddress** | string \* required | Granter address you want to lookup |
| **granteeAddress** | string \* required | Grantee address you want to lookup |
| **msgType** | string \* required | Message type you want to lookup |

**Example** \_\_**JSON Output**

```javascript
{
  "GenericGrantInfo": {
    "authorization": {
      "type": "msgauth/GenericAuthorization",
      "value": {
        "msg_type": "send"
      }
    },
    "expiration": "2021-06-24T09:33:20.012999Z"
  },
  "SendGrantInfo": {
    "authorization": {
      "type": "msgauth/SendAuthorization",
      "value": {
        "spend_limit": [
          {
            "denom": "uluna",
            "amount": "50"
          }
        ]
      }
    },
    "expiration": "2021-06-24T09:33:20.012999Z"
  }
}
```

### `POST/msgauth/granters/{granterAddress}/grantees/{granteeAddress}/grants/{msgType}/revoke`

**Description**

Revoke grant from grantee address

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **granterAddress** | string \* required | Granter address you want to lookup |
| **granteeAddress** | string \* required | Grantee address you want to lookup |
| **msgType** | string \* required |  |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  }
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

### **`POST/msgauth/execute`**

**Description**

Execute messages from grantee address

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **Revoke request body** | object | Body |

**Example Request**

```javascript
{
  "base_req": {
    "from": "terra1wg2mlrxdmnnkkykgqg4znky86nyrtc45q336yv",
    "memo": "Sent via Terra Station 🚀",
    "chain_id": "columbus-3",
    "account_number": "0",
    "sequence": "1",
    "gas": "200000",
    "gas_adjustment": "1.2",
    "fees": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ],
    "simulate": false
  },
  "msgs": [
    "string"
  ]
}
```

**Example** \_\_**JSON Output**

```javascript
{
  "msg": [
    "string"
  ],
  "fee": {
    "gas": "string",
    "amount": [
      {
        "denom": "uluna",
        "amount": "50"
      }
    ]
  },
  "memo": "string",
  "signature": {
    "signature": "MEUCIQD02fsDPra8MtbRsyB1w7bqTM55Wu138zQbFcWx4+CFyAIge5WNPfKIuvzBZ69MyqHsqD8S1IwiEp+iUb6VSdtlpgY=",
    "pub_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "Avz04VhtKJh8ACCVzlI8aTosGy0ikFXKIVHQ3jKMrosH"
    },
    "account_number": "0",
    "sequence": "0"
  }
}
```

