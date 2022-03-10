---
description: >-
  HTTP API documentation for the Avalanche Indexer API service provided by
  DataHub
---

# Avalanche Indexer API

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/" method="get" summary="Service Index" %}
{% swagger-description %}
Returns the list of all available endpoints
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "endpoints": [
    {
      "path": "/",
      "description": "Index"
    },
    {
      "path": "/health",
      "description": "Get indexer health"
    },
    {
      "path": "/status",
      "description": "Get indexer status"
    },
    {
      "path": "/network_stats",
      "description": "Get network stats"
    },
    {
      "path": "/validators",
      "description": "Get current validator set"
    },
    {
      "path": "/validators/:id",
      "description": "Get validator details"
    },
    {
      "path": "/delegations",
      "description": "Get active delegations"
    },
    {
      "path": "/address/:id",
      "description": "Get address details"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/health" method="get" summary="Health Status" %}
{% swagger-description %}
Returns the current service healthThis endpoint is useful for automated service checks.
{% endswagger-description %}

{% swagger-response status="200" description="Service is healthy" %}
```javascript
{
  "healthy": true
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/status" method="get" summary="Service Status" %}
{% swagger-description %}
Returns the current service status along with node version and sync status
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "app_name": "avalanche-indexer",
  "app_version": "0.2.2",
  "git_commit": "8c2efdd63253973682423d8ef563b8a6a6d9d1e7",
  "go_version": "go1.15.8",
  "network_name": "mainnet",
  "node_version": "avalanche/1.3.0",
  "sync_status": "current",
  "sync_time": "2021-04-22T02:11:29.079984Z"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/network_stats" method="get" summary="Network Stats" %}
{% swagger-description %}
Returns network statistics for a given time period
{% endswagger-description %}

{% swagger-parameter in="query" name="bucket" type="string" %}
Time period. Daily - 

`d`

, Hourly - 

`h`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
Number of records to return
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "time": "2021-04-22T02:00:00Z",
    "bucket": "h",
    "height_change": 8,
    "peers": 844,
    "blockchains": 7,
    "active_validators": 927,
    "pending_validators": 0,
    "validator_uptime": 0,
    "active_delegations": 6896,
    "pending_delegations": 0,
    "min_validator_stake": 0,
    "min_delegator_stake": 0,
    "tx_fee": 0,
    "create_tx_fee": 0,
    "total_staked": "210234424485335687",
    "total_delegated": "88892179030090484"
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/assets" method="get" summary="Assets list" %}
{% swagger-description %}
Returns a list of all Avalanche assets
{% endswagger-description %}

{% swagger-parameter in="query" name="type" type="string" %}
Filter by asset type
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "id": "2U94JFY14wfAuDUEkyfLi8qY7NpVmWWHLDhYNCQc8gPqjVwmk2",
    "type": "nft",
    "name": "00dot00dot00",
    "symbol": "DOTZ",
    "denomination": 0
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/assets/{id}" method="get" summary="Asset details" %}
{% swagger-description %}
Returns asset details for a given ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Asset ID
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
  "type": "fixed_cap",
  "name": "Avalanche",
  "symbol": "AVAX",
  "denomination": 9,
  "transactions_count": 4808311
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/chains" method="get" summary="Chains list" %}
{% swagger-description %}
Returns list of all chains
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "id": "GF5KEgiGs2yhDFTL1KgfmszU61U3ipSMpQJZsra5nFysots68",
    "name": "Bthereum",
    "vm": "mgj786NP7uDwBCcq6YwThhaN8FLyybkCa4zBWTQbNgmK6k9A6",
    "subnet": "29ejv3iGb7xiAiCiTyxqm5cSR81CkitmWttxddRcr5wnrC3uhW",
    "network": 1
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/chain_sync_statuses" method="get" summary="Chain indexing statuses" %}
{% swagger-description %}
Returns current indexing status for primary chains
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "id": "11111111111111111111111111111111LpoYY",
    "index_id": 644773,
    "index_time": "2021-07-19T15:36:52.522053Z",
    "tip_id": 644773,
    "tip_time": "2021-07-19T15:36:52.522053Z"
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/validators" method="get" summary="Active Validators" %}
{% swagger-description %}
Returns a collection of active validators
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "node_id": "NodeID-Jp9FEmmXG3EoYpfatzkzvg5pyxvd6nUEN",
    "stake_amount": "2000000000000",
    "stake_percent": 0.0009513189882656466,
    "potential_reward": "120474792725",
    "reward_address": "P-avax1dlgpssepfscqsmatk05wrtt7dqyxnua4sp3zy2",
    "active": true,
    "active_start_time": "2021-02-14T04:19:10Z",
    "active_end_time": "2021-09-18T11:00:26Z",
    "active_progress_percent": 30.939804161041387,
    "uptime": 93.80999803543091,
    "delegations_count": 0,
    "delegations_percent": 0,
    "delegated_amount": "0",
    "delegated_amount_percent": 0,
    "delegation_fee": 2,
    "capacity": "8000000000000",
    "capacity_percent": 0,
    "first_height": 409696,
    "last_height": 409696,
    "created_at": "2021-02-14T04:21:03.691352Z",
    "updated_at": "2021-04-22T02:18:29.079797Z"
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/validators/{id}" method="get" summary="Validator Details" %}
{% swagger-description %}
Returns validator details and associated data
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Validator Node ID
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "delegations": [
    {
      "id": "0397094d96455816c1d93128393b3253262b68bb",
      "node_id": "NodeID-8gx2j2546NwHiqwjRqdy9uKfpDPSKoDVb",
      "stake_amount": "26461500000",
      "potential_reward": "946515102",
      "reward_address": "P-avax1626th8k05ep94mzw4smvely8hmrlgnqpfwpvk4",
      "active": true,
      "active_start_time": "2021-01-27T13:38:15Z",
      "active_end_time": "2021-06-08T12:40:52Z",
      "first_height": 285725,
      "last_height": 409697,
      "created_at": "2021-01-27T13:38:32.22744Z",
      "updated_at": "2021-04-22T02:20:29.079779Z"
    }
  ],
  "stats_24h": [
    {
      "time": "2021-04-22T02:00:00Z",
      "bucket": "h",
      "uptime_min": 99.97,
      "uptime_max": 99.97,
      "uptime_avg": 99.97,
      "stake_amount": 2000000000000,
      "stake_percent": 0.0009513189882656466,
      "delegations_count": 5,
      "delegations_percent": 0.07,
      "delegated_amount": 412603490406,
      "delegated_amount_percent": 0
    }
  ],
  "stats_30d": [
    {
      "time": "2021-04-22T00:00:00Z",
      "bucket": "d",
      "uptime_min": 99.97,
      "uptime_max": 99.97,
      "uptime_avg": 99.97,
      "stake_amount": 2000000000000,
      "stake_percent": 0.0009513197585872734,
      "delegations_count": 5,
      "delegations_percent": 0.07,
      "delegated_amount": 412603490406,
      "delegated_amount_percent": 0
    }
  ],
  "validator": {
    "node_id": "NodeID-8gx2j2546NwHiqwjRqdy9uKfpDPSKoDVb",
    "stake_amount": "2000000000000",
    "stake_percent": 0.0009513189882656466,
    "potential_reward": "102617375642",
    "reward_address": "P-avax1kkjr9znd0ya3h2h7zs4egtwr7l7sqctuw0p3gg",
    "active": true,
    "active_start_time": "2020-12-08T17:58:13Z",
    "active_end_time": "2021-06-08T16:55:52Z",
    "active_progress_percent": 73.83558626044213,
    "uptime": 99.97000098228455,
    "delegations_count": 5,
    "delegations_percent": 0.0725268349289237,
    "delegated_amount": "412603490406",
    "delegated_amount_percent": 0.0004641646639264132,
    "delegation_fee": 2,
    "capacity": "7587396509594",
    "capacity_percent": 5.157543630075,
    "first_height": 409697,
    "last_height": 409697,
    "created_at": "2020-12-08T17:58:47.047544Z",
    "updated_at": "2021-04-22T02:20:29.079779Z"
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/delegations" method="get" summary="Active Delegations" %}
{% swagger-description %}
Returns active delegations records
{% endswagger-description %}

{% swagger-parameter in="query" name="node_id" type="string" %}
Filter delegations by validator node ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="reward_address" type="string" %}
Filter delegations by a reward address
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "id": "5b2f32c5b779790d97047e07af993dc0c4fe23cd",
    "node_id": "NodeID-AWPFmXs1VyVmGod6eg14ZC67QZafBN8BZ",
    "stake_amount": "200000000000",
    "potential_reward": "1025559498",
    "reward_address": "P-avax1vr6ss2xj6r9qsgqsz47w77a8kncpl8tyexsx3j",
    "active": true,
    "active_start_time": "2021-04-22T01:42:08Z",
    "active_end_time": "2021-05-13T01:51:35Z",
    "first_height": 409675,
    "last_height": 409698,
    "created_at": "2021-04-22T01:42:29.079802Z",
    "updated_at": "2021-04-22T02:25:29.079839Z"
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/address/{address}" method="get" summary="Account Details" %}
{% swagger-description %}
Returns account balances
{% endswagger-description %}

{% swagger-parameter in="path" name="address" type="string" %}
Blockchain address (X/P/C)
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "balance": "2295690000",
  "unlocked": "2295690000",
  "lockedStakeable": "0",
  "lockedNotStakeable": "0"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/blocks" method="get" summary="Blocks search" %}
{% swagger-description %}
Returns block matching the search parameters
{% endswagger-description %}

{% swagger-parameter in="query" name="chain" type="string" %}
Chain ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="start_height" type="integer" %}
Start height
{% endswagger-parameter %}

{% swagger-parameter in="query" name="end_height" type="integer" %}
End height
{% endswagger-parameter %}

{% swagger-parameter in="query" name="type" type="string" %}
Block type
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
Results page
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "id": "BsnXKtvhyBUzXS87BbAfjAbFxfwTc4N8KGEiCkmA1kCV1fpct",
    "type": "commit",
    "parent": "2BUyTAMr4UZ5FjF6fbPsWRDqpXrUMRWCaJaTC3X2idZW6bdRXZ",
    "chain": "11111111111111111111111111111111LpoYY",
    "height": 640016,
    "timestamp": "2021-07-16T15:19:45.468737Z"
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/blocks/{hash}" method="get" summary="Block details" %}
{% swagger-description %}
Returns block details by block hash
{% endswagger-description %}

{% swagger-parameter in="path" name="hash" type="string" %}
Block hash
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": "2Bok2WUr92N5jYSs8mmGfChw9sFZ4h83Ttfs4ngjywiqfaJMBw",
  "type": "commit",
  "parent": "2WEk5pHvq6vKGvdEBSM8mCve1qpmt8cDmqbiZZxFDr6vK3Sbip",
  "chain": "11111111111111111111111111111111LpoYY",
  "height": 640025,
  "timestamp": "2021-07-16T15:25:54.091248Z"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Error" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transactions" method="get" summary="Transaction search" %}
{% swagger-description %}
Returns transactions matching the search parameters
{% endswagger-description %}

{% swagger-parameter in="query" name="chain" type="string" %}
Filter by chain ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="type" type="string" %}
Filter by transaction type. Separate multiple values by comma.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="start_time" type="string" %}
Search range start time.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="end_time" type="string" %}
Search range end time.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="start_height" type="string" %}
Search range start block height (if applicable).
{% endswagger-parameter %}

{% swagger-parameter in="query" name="block_hash" type="string" %}
Filter by block hash (if applicable).
{% endswagger-parameter %}

{% swagger-parameter in="query" name="memo" type="string" %}
Filter by memo text field.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="address" type="string" %}
Filter by account address. Separate multiple values by comma.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="asset" type="string" %}
Filter by asset ID.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
Results page.
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
    "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
    "type": "x_base",
    "timestamp": "2021-07-16T14:32:48.771734Z",
    "status": "accepted",
    "memo": "",
    "memo_text": "",
    "fee": 1000000,
    "inputs": [
      {
        "id": "nSCo2w1evTnkrcDxNb83jckhgeqhU3ZmSj9TmKXHG8snYU9x6",
        "tx_id": "mTgA8QRDc4fj9vgUz7WmrHuQyewVWFA8WSMq8gDmS8YyhMYB5",
        "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
        "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
        "type": "transfer",
        "index": 1,
        "locktime": 0,
        "threshold": 1,
        "amount": 246420423888,
        "group": 0,
        "addresses": [
          "avax1g62yztrg7nu6ml0gxvcn8c29ease7yqz9u5skq"
        ],
        "stake": false,
        "reward": false,
        "spent": true,
        "spent_in_tx": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq"
      }
    ],
    "input_amounts": {
      "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": 246420423888
    },
    "outputs": [
      {
        "id": "TxTjdRFsFX7FoTqGKytASi576Lv47qSt6xn7B2KA9Df7LkYYX",
        "tx_id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
        "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
        "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
        "type": "transfer",
        "index": 0,
        "locktime": 0,
        "threshold": 1,
        "amount": 31300000000,
        "group": 0,
        "addresses": [
          "avax1dsftd8yed98h2t6l2ymex0df7jq3naj5y54g7e"
        ],
        "stake": false,
        "reward": false,
        "spent": false,
        "spent_in_tx": null
      },
      {
        "id": "X9UXxDPRxt3aKFrNKX3cr2nzHktuJyHFxeBZtNbShUhdfFKqn",
        "tx_id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
        "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
        "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
        "type": "transfer",
        "index": 1,
        "locktime": 0,
        "threshold": 1,
        "amount": 215119423888,
        "group": 0,
        "addresses": [
          "avax1g0k7j58h5u3kwgjnw6zxc4su7cvk4zcelf35d8"
        ],
        "stake": false,
        "reward": false,
        "spent": false,
        "spent_in_tx": null
      }
    ],
    "output_amounts": {
      "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": 246419423888
    }
  }
]
```
{% endswagger-response %}

{% swagger-response status="400" description="Error" %}
```javascript
{
  "error": "invalid transaction type: foo",
  "status": 400
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transactions/{id}" method="get" summary="Transaction details" %}
{% swagger-description %}
Returns transaction details for a given ID/hash
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Transaction ID/hash
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
  "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
  "type": "x_base",
  "timestamp": "2021-07-16T14:32:48.771734Z",
  "status": "accepted",
  "memo": "",
  "memo_text": "",
  "fee": 1000000,
  "inputs": [
    {
      "id": "nSCo2w1evTnkrcDxNb83jckhgeqhU3ZmSj9TmKXHG8snYU9x6",
      "tx_id": "mTgA8QRDc4fj9vgUz7WmrHuQyewVWFA8WSMq8gDmS8YyhMYB5",
      "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
      "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "type": "transfer",
      "index": 1,
      "locktime": 0,
      "threshold": 1,
      "amount": 246420423888,
      "group": 0,
      "addresses": [
        "avax1g62yztrg7nu6ml0gxvcn8c29ease7yqz9u5skq"
      ],
      "stake": false,
      "reward": false,
      "spent": true,
      "spent_in_tx": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq"
    }
  ],
  "input_amounts": {
    "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": 246420423888
  },
  "outputs": [
    {
      "id": "TxTjdRFsFX7FoTqGKytASi576Lv47qSt6xn7B2KA9Df7LkYYX",
      "tx_id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
      "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
      "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "type": "transfer",
      "index": 0,
      "locktime": 0,
      "threshold": 1,
      "amount": 31300000000,
      "group": 0,
      "addresses": [
        "avax1dsftd8yed98h2t6l2ymex0df7jq3naj5y54g7e"
      ],
      "stake": false,
      "reward": false,
      "spent": false,
      "spent_in_tx": null
    },
    {
      "id": "X9UXxDPRxt3aKFrNKX3cr2nzHktuJyHFxeBZtNbShUhdfFKqn",
      "tx_id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
      "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
      "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "type": "transfer",
      "index": 1,
      "locktime": 0,
      "threshold": 1,
      "amount": 215119423888,
      "group": 0,
      "addresses": [
        "avax1g0k7j58h5u3kwgjnw6zxc4su7cvk4zcelf35d8"
      ],
      "stake": false,
      "reward": false,
      "spent": false,
      "spent_in_tx": null
    }
  ],
  "output_amounts": {
    "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": 246419423888
  }
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Error" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transaction_outputs/{id}" method="get" summary="Transaction output details" %}
{% swagger-description %}
Returns transaction output details for a given ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Transaction output ID
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": "TxTjdRFsFX7FoTqGKytASi576Lv47qSt6xn7B2KA9Df7LkYYX",
  "tx_id": "62RFqPfHP56tgxByVwp7JeM7uQkBouFyFpwNYxC2KZ2cw1Zxq",
  "chain": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
  "asset": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
  "type": "transfer",
  "index": 0,
  "locktime": 0,
  "threshold": 1,
  "amount": 31300000000,
  "group": 0,
  "addresses": [
    "avax1dsftd8yed98h2t6l2ymex0df7jq3naj5y54g7e"
  ],
  "stake": false,
  "reward": false,
  "spent": false,
  "spent_in_tx": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Error" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transaction_types" method="get" summary="Transaction type stats" %}
{% swagger-description %}
Returns available transaction types and their counts
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
[
  {
    "type": "c_evm",
    "total_count": 3373474
  }
]
```
{% endswagger-response %}
{% endswagger %}
