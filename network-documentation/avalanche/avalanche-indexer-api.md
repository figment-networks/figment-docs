---
description: >-
  HTTP API documentation for the Avalanche Indexer API service provided by
  DataHub
---

# Avalanche Indexer API

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/" %}
{% api-method-summary %}
Service Index
{% endapi-method-summary %}

{% api-method-description %}
Returns the list of all available endpoints
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/health" %}
{% api-method-summary %}
Health Status
{% endapi-method-summary %}

{% api-method-description %}
Returns the current service healthThis endpoint is useful for automated service checks.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Service is healthy
{% endapi-method-response-example-description %}

```javascript
{
  "healthy": true
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/status" %}
{% api-method-summary %}
Service Status
{% endapi-method-summary %}

{% api-method-description %}
Returns the current service status along with node version and sync status
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/network\_stats" %}
{% api-method-summary %}
Network Stats
{% endapi-method-summary %}

{% api-method-description %}
Returns network statistics for a given time period
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="bucket" type="string" required=false %}
Time period. Daily - `d`, Hourly - `h`
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
Number of records to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/assets" %}
{% api-method-summary %}
Assets list
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of all Avalanche assets
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="type" type="string" required=false %}
Filter by asset type
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/assets/{id}" %}
{% api-method-summary %}
Asset details
{% endapi-method-summary %}

{% api-method-description %}
Returns asset details for a given ID
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Asset ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/chains" %}
{% api-method-summary %}
Chains list
{% endapi-method-summary %}

{% api-method-description %}
Returns list of all chains
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/chain\_sync\_statuses" %}
{% api-method-summary %}
Chain indexing statuses
{% endapi-method-summary %}

{% api-method-description %}
Returns current indexing status for primary chains
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/validators" %}
{% api-method-summary %}
Active Validators
{% endapi-method-summary %}

{% api-method-description %}
Returns a collection of active validators
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/validators/{id}" %}
{% api-method-summary %}
Validator Details
{% endapi-method-summary %}

{% api-method-description %}
Returns validator details and associated data
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Validator Node ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/delegations" %}
{% api-method-summary %}
Active Delegations
{% endapi-method-summary %}

{% api-method-description %}
Returns active delegations records
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="node\_id" type="string" required=false %}
Filter delegations by validator node ID
{% endapi-method-parameter %}

{% api-method-parameter name="reward\_address" type="string" required=false %}
Filter delegations by a reward address
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/accounts/{address}" %}
{% api-method-summary %}
Account Details
{% endapi-method-summary %}

{% api-method-description %}
Returns account balances
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=true %}
Blockchain address \(X/P/C\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

```javascript
{
  "balance": "2295690000",
  "unlocked": "2295690000",
  "lockedStakeable": "0",
  "lockedNotStakeable": "0"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/blocks" %}
{% api-method-summary %}
Blocks search
{% endapi-method-summary %}

{% api-method-description %}
Returns block matching the search parameters
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="chain" type="string" required=true %}
Chain ID
{% endapi-method-parameter %}

{% api-method-parameter name="start\_height" type="integer" required=false %}
Start height
{% endapi-method-parameter %}

{% api-method-parameter name="end\_height" type="integer" required=false %}
End height
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
Block type
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
Results page
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/blocks/{hash}" %}
{% api-method-summary %}
Block details
{% endapi-method-summary %}

{% api-method-description %}
Returns block details by block hash
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="hash" type="string" required=true %}
Block hash
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Error
{% endapi-method-response-example-description %}

```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transactions" %}
{% api-method-summary %}
Transaction search
{% endapi-method-summary %}

{% api-method-description %}
Returns transactions matching the search parameters
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="chain" type="string" required=false %}
Filter by chain ID
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
Filter by transaction type. Separate multiple values by comma.
{% endapi-method-parameter %}

{% api-method-parameter name="start\_time" type="string" required=false %}
Search range start time.
{% endapi-method-parameter %}

{% api-method-parameter name="end\_time" type="string" required=false %}
Search range end time.
{% endapi-method-parameter %}

{% api-method-parameter name="start\_height" type="string" required=false %}
Search range start block height \(if applicable\).
{% endapi-method-parameter %}

{% api-method-parameter name="block\_hash" type="string" required=false %}
Filter by block hash \(if applicable\).
{% endapi-method-parameter %}

{% api-method-parameter name="memo" type="string" required=false %}
Filter by memo text field.
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=false %}
Filter by account address. Separate multiple values by comma.
{% endapi-method-parameter %}

{% api-method-parameter name="asset" type="string" required=false %}
Filter by asset ID.
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
Results page.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Error
{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid transaction type: foo",
  "status": 400
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transactions/{id}" %}
{% api-method-summary %}
Transaction details
{% endapi-method-summary %}

{% api-method-description %}
Returns transaction details for a given ID/hash
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Transaction ID/hash
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Error
{% endapi-method-response-example-description %}

```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transaction\_outputs/{id}" %}
{% api-method-summary %}
Transaction output details
{% endapi-method-summary %}

{% api-method-description %}
Returns transaction output details for a given ID
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Transaction output ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Error
{% endapi-method-response-example-description %}

```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://avalanche--mainnet--indexer.datahub.figment.io/apikey/APIKEY" path="/transaction\_types" %}
{% api-method-summary %}
Transaction type stats
{% endapi-method-summary %}

{% api-method-description %}
Returns available transaction types and their counts
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

```javascript
[
  {
    "type": "c_evm",
    "total_count": 3373474
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

