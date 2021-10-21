---
description: Learn how to interact with Figment's NEAR Indexer REST API
---

# Indexer API

## General

Below you can find a list of general service endpoints to check health, current indexer status, etc.

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/" method="get" summary="Service Index" %}
{% swagger-description %}
Returns the list of all available endpoints
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "endpoints": {
    "/accounts/:id": "Get account details",
    "/block": "Get current block details",
    "/block_stats": "Get block stats for a time bucket",
    "/block_times": "Get average block times",
    "/blocks": "Get latest blocks",
    "/blocks/:id": "Get block details by height or hash",
    "/delegations/:id": "Get account delegations",
    "/epochs": "Get list of epochs",
    "/epochs/:id": "Get epoch details",
    "/events": "Get list of events",
    "/events/:id": "Get event details",
    "/health": "Get service health",
    "/height": "Get current block height",
    "/status": "Get service and network status",
    "/transactions": "List all recent transactions",
    "/transactions/:id": "Get transaction details",
    "/validators": "List all validators",
    "/validators/:id": "Get validator details",
    "/validators/:id/epochs": "Get validator epochs performance",
    "/validators/:id/events": "Get validator events"
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/health" method="get" summary="Health Status" %}
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

{% swagger-response status="500" description="Service is unhealthy" %}
```javascript
{
  "healthy": false
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/status" method="get" summary="Service Status" %}
{% swagger-description %}
Returns the current service status along with node version and sync status
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "app_name": "near-indexer",
  "app_version": "0.3.6",
  "git_commit": "de980fab25af9f044f97a5680cf66909f6d5e023",
  "go_version": "go1.15.11",
  "last_block_height": 35401104,
  "last_block_time": "2021-04-22T00:39:01.893367Z",
  "network_name": "mainnet",
  "network_version": "1.18.2",
  "node_block_height": 35401108,
  "node_block_time": "2021-04-22T00:39:06Z",
  "sync_status": "current"
}
```
{% endswagger-response %}
{% endswagger %}

## Blocks

Below you can find block-related endpoints.

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/height" method="get" summary="Current Block Height" %}
{% swagger-description %}
Returns the latest block height and time
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "height": 35401371,
  "time": "2021-04-22T00:43:27.882413Z"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/blocks" method="get" summary="Fetch Blocks" %}
{% swagger-description %}
Returns a collection of blocks
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": 35401442,
  "time": "2021-04-22T00:44:39.21642Z",
  "producer": "moonlet.poolv1.near",
  "hash": "DYfWrRWjRUYo4RomVSVzEb8mNLKbXRtwtWxRvpniwUgp",
  "epoch": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
  "gas_price": "100000000",
  "gas_allowed": 0,
  "gas_used": 0,
  "total_supply": "1024662809690621148657935916978742",
  "chunks_count": 1,
  "transactions_count": 1,
  "approvals_count": 60,
  "created_at": "2021-04-22T00:44:42.942385Z"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/blocks/{id}" method="get" summary="Fetch Block" %}
{% swagger-description %}
Returns a single block
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="int" %}
Block height
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": 35401562,
  "time": "2021-04-22T00:46:41.463156Z",
  "producer": "figment.poolv1.near",
  "hash": "6k8oTAh3q7UPWLobZSHFVi3sKwEdv94ooF7wgaRuK2W8",
  "epoch": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
  "gas_price": "100000000",
  "gas_allowed": 0,
  "gas_used": 0,
  "total_supply": "1024662809647167208952262516978742",
  "chunks_count": 1,
  "transactions_count": 0,
  "approvals_count": 60,
  "created_at": "2021-04-22T00:46:45.331482Z"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Block not found" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/block_times" method="get" summary="Block Production Times" %}
{% swagger-description %}
Returns min/max/avg block production times for a number of recent blocks
{% endswagger-description %}

{% swagger-parameter in="query" name="limit" type="int" %}
Number of past blocks to scan
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "start_height": 35401691,
  "end_height": 35401790,
  "start_time": "2021-04-22T00:48:48.307734+00:00",
  "end_time": "2021-04-22T00:50:25.86459+00:00",
  "count": 100,
  "diff": 97.556856,
  "avg": 0.975569
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/block_stats" method="get" summary="Block Stats" %}
{% swagger-description %}
Returns various time-aggregated block statistics
{% endswagger-description %}

{% swagger-parameter in="query" name="bucket" type="string" %}
Time bucket. Default is 

`h`

 \- hourly
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="int" %}
Number of entries to return. Default is 

`24`
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "time": "2021-04-22T00:00:00+00:00",
  "bucket": "h",
  "blocks_count": 3292,
  "block_time_avg": 1.01,
  "validators_count": 60,
  "transactions_count": 1217
}
```
{% endswagger-response %}
{% endswagger %}

## Validators

Below you can find a set of endpoints to get active validators, validator details, events and epoch performance.

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/validators" method="get" summary="Current Validators" %}
{% swagger-description %}
Returns a collection of active validators
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "account_id": "binancestaking.poolv1.near",
  "start_height": 31852250,
  "start_time": "2021-03-11T09:28:35.846878Z",
  "last_height": 35402265,
  "last_time": "2021-04-22T00:58:17.094339Z",
  "expected_blocks": 89856,
  "produced_blocks": 89848,
  "active": true,
  "slashed": false,
  "stake": "8444497444615070302919326207972",
  "efficiency": 99.99095061728396,
  "reward_fee": 10
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/validators/{name}" method="get" summary="Validator Details" %}
{% swagger-description %}
Returns validator details
{% endswagger-description %}

{% swagger-parameter in="path" name="name" type="string" %}
Validator name
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "account": {
    "name": "figment.poolv1.near",
    "start_height": 15133832,
    "start_time": "2020-09-08T16:05:14.275077Z",
    "last_height": 35402368,
    "last_time": "2021-04-22T00:59:59.233854Z",
    "balance": null,
    "staking_balance": "4928670356302427455959185032855"
  },
  "blocks": [
    {
      "id": 35402368,
      "time": "2021-04-22T00:59:59.233854Z",
      "producer": "abl_pool.poolv1.near",
      "hash": "FGU2LRUaomSaL55LgdJKBPgiDkocDvXp55pub2B5FQG6",
      "epoch": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
      "gas_price": "100000000",
      "gas_allowed": 0,
      "gas_used": 0,
      "total_supply": "1024662809256761082456380316978742",
      "chunks_count": 1,
      "transactions_count": 0,
      "approvals_count": 60,
      "created_at": "2021-04-22T01:00:02.95959Z"
    }
  ],
  "epochs": [
    {
      "epoch": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
      "last_height": 35402368,
      "last_time": "2021-04-22T00:59:59.233854Z",
      "expected_blocks": 432,
      "produced_blocks": 432,
      "efficiency": 100,
      "staking_balance": "4928670356302427455959185032855",
      "reward_fee": 10
    }
  ],
  "events": [
    {
      "id": 667,
      "scope": "staking",
      "action": "joined_active_set",
      "block_height": 33796253,
      "block_time": "2021-04-03T11:06:44.044152Z",
      "epoch": "8Lmh225rm6JL5dkibKnhfqXo24dqV45gq1VY3j9bEXEg",
      "item_id": "figment.poolv1.near",
      "item_type": "validator",
      "metadata": {
        "stake": "5012170183531623510393965623638"
      },
      "created_at": "2021-04-09T20:07:59.240599Z"
    }
  ],
  "validator": {
    "account_id": "figment.poolv1.near",
    "start_height": 15133832,
    "start_time": "2020-09-08T16:05:14.275077Z",
    "last_height": 35402368,
    "last_time": "2021-04-22T00:59:59.233854Z",
    "expected_blocks": 410394,
    "produced_blocks": 409112,
    "active": true,
    "slashed": false,
    "stake": "4928670356302427455959185032855",
    "efficiency": 99.73643819742489,
    "reward_fee": 10
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

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/validators/{name}/epochs" method="get" summary="Validator Epoch Performance" %}
{% swagger-description %}
Returns validator's performance records
{% endswagger-description %}

{% swagger-parameter in="query" name="page" type="int" %}
Results page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="int" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "page": 1,
  "pages": 5,
  "limit": 100,
  "count": 466,
  "records": [
    {
      "epoch": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
      "last_height": 35402527,
      "last_time": "2021-04-22T01:02:43.011692Z",
      "expected_blocks": 432,
      "produced_blocks": 432,
      "efficiency": 100,
      "staking_balance": "4928670356302427455959185032855",
      "reward_fee": 10
    }
  ]
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

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/validators/{name}/events" method="get" summary="Validator Events" %}
{% swagger-description %}
Returns validator's events
{% endswagger-description %}

{% swagger-parameter in="query" name="page" type="int" %}
Results page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="int" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "page": 1,
  "pages": 1,
  "limit": 100,
  "count": 8,
  "records": [
    {
      "id": 667,
      "scope": "staking",
      "action": "joined_active_set",
      "block_height": 33796253,
      "block_time": "2021-04-03T11:06:44.044152Z",
      "epoch": "8Lmh225rm6JL5dkibKnhfqXo24dqV45gq1VY3j9bEXEg",
      "item_id": "figment.poolv1.near",
      "item_type": "validator",
      "metadata": {
        "stake": "5012170183531623510393965623638"
      },
      "created_at": "2021-04-09T20:07:59.240599Z"
    }
  ]
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

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/delegations/{name}" method="get" summary="Validator Delegations" %}
{% swagger-description %}
Returns validator's active delegations
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "account": "zulunh.near",
  "unstaked_balance": "205356875549964590938748204",
  "staked_balance": "205356875549964590938748204",
  "can_withdraw": true
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

## Epochs

Below is the list of epoch-related endpoints.

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/epochs" method="get" summary="List Epochs" %}
{% swagger-description %}
Returns a paginated collection of epochs
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
  "start_height": 35394654,
  "start_time": "2021-04-21T22:50:38.876386Z",
  "end_height": 35403632,
  "end_time": "2021-04-22T01:22:07.620618Z",
  "blocks_count": 8976,
  "validators_count": 60,
  "average_efficiency": 99.9624
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/epochs/{id}" method="get" summary="Epoch Details" %}
{% swagger-description %}
Returns epoch details
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": "9b4WLoXXYgga9mGRLGsWKuWEk4FsFwbXETao7bDUdLE6",
  "start_height": 35394654,
  "start_time": "2021-04-21T22:50:38.876386Z",
  "end_height": 35403678,
  "end_time": "2021-04-22T01:22:59.256034Z",
  "blocks_count": 9021,
  "validators_count": 60,
  "average_efficiency": 99.9624
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

## Events

Below is the list of event-related endpoints.

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/events" method="get" summary="List Events" %}
{% swagger-description %}
Returns a paginated collection of network events
{% endswagger-description %}

{% swagger-parameter in="query" name="epoch" type="string" %}
Filter events by epoch
{% endswagger-parameter %}

{% swagger-parameter in="query" name="height" type="integer" %}
Filter events by block height
{% endswagger-parameter %}

{% swagger-parameter in="query" name="action" type="string" %}
Filter events by action
{% endswagger-parameter %}

{% swagger-parameter in="query" name="item_id" type="string" %}
Filter by entity. Required when 

`item_type`

 is set.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="item_type" type="string" %}
Filter by entity type. Required when 

`item_id`

 is set.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
Results page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "page": 1,
  "pages": 7,
  "limit": 100,
  "count": 670,
  "records": [
    {
      "id": 699,
      "scope": "staking",
      "action": "joined_active_set",
      "block_height": 35092254,
      "block_time": "2021-04-18T10:24:21.54726Z",
      "epoch": "Atp4ojbE8BDAgMUeGDkFtzAQqT717aXo8WtWAyEiucTz",
      "item_id": "legends.poolv1.near",
      "item_type": "validator",
      "metadata": {
        "stake": "4053494604887807455238768084035"
      },
      "created_at": "2021-04-19T16:40:18.339886Z"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/events/{id}" method="get" summary="Event Details" %}
{% swagger-description %}
Returns an individual event details
{% endswagger-description %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": 699,
  "scope": "staking",
  "action": "joined_active_set",
  "block_height": 35092254,
  "block_time": "2021-04-18T10:24:21.54726Z",
  "epoch": "Atp4ojbE8BDAgMUeGDkFtzAQqT717aXo8WtWAyEiucTz",
  "item_id": "legends.poolv1.near",
  "item_type": "validator",
  "metadata": {
    "stake": "4053494604887807455238768084035"
  },
  "created_at": "2021-04-19T16:40:18.339886Z"
}
```
{% endswagger-response %}
{% endswagger %}

## Transaction Search

Below is the list of transactions related endpoints.

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/transactions" method="get" summary="Search Transactions" %}
{% swagger-description %}
Returns a paginated collection of transactions matching input filters.
{% endswagger-description %}

{% swagger-parameter in="query" name="block_hash" type="string" %}
Filter transactions by block hash.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="block_height" type="integer" %}
Filter transactions by block height.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sender" type="string" %}
Filter transactions by sender account name.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="receiver" type="string" %}
Filter transactions by receiver account name.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="start_date" type="string" %}
Time range start date. Supports 

`YYYY-MM-DD`

 or RFC3339 format.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="end_date" type="string" %}
Time range end date. Supports 

`YYYY-MM-DD`

 or RFC3339 format.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="integer" %}
Results page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "page": 1,
  "pages": 17107,
  "limit": 100,
  "count": 1710634,
  "records": [
    {
      "id": 1710688,
      "created_at": "2021-04-22T01:24:17.583057Z",
      "updated_at": "2021-04-22T01:24:17.583057Z",
      "time": "2021-04-22T01:24:10.024782Z",
      "height": 35403745,
      "hash": "7aFHtiGFuKkeiHx6hCyjftWjaXoKThf2HEsfarnvWz1Z",
      "block_hash": "H7mPyKcQ5LqTndt4jyN7zeayCzQv8BAETbk7SQqRt2BL",
      "sender": "thuongdphan.near",
      "receiver": "ref-finance.near",
      "gas_burnt": "2428117762192",
      "actions": [
        {
          "data": {
            "gas": 50000000000000,
            "deposit": "1",
            "method_name": "withdraw"
          },
          "type": "FunctionCall"
        }
      ],
      "actions_count": 1,
      "success": true
    },
    {
      "id": 1710687,
      "created_at": "2021-04-22T01:24:17.583057Z",
      "updated_at": "2021-04-22T01:24:17.583057Z",
      "time": "2021-04-22T01:24:07.143511Z",
      "height": 35403742,
      "hash": "4CgsaXJNGN8Ckb3PcfXhUf9ZZGsT5BTbXJFMmTFDdMo8",
      "block_hash": "39SP5VU7Ymk4n3DJU5bJZfxuAMN3zTj3Tiy9GB2WABna",
      "sender": "poppingbean6.near",
      "receiver": "ref-finance.near",
      "gas_burnt": "2428115526258",
      "actions": [
        {
          "data": {
            "gas": 50000000000000,
            "deposit": "1",
            "method_name": "withdraw"
          },
          "type": "FunctionCall"
        }
      ],
      "actions_count": 1,
      "success": true
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="500" description="Invalid time filter" %}
```javascript
{
  "error": "start time is invalid",
  "status": 500

```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://near--indexer.datahub.figment.io/apikey/APIKEY" path="/transactions/{hash}" method="get" summary="Transaction Details" %}
{% swagger-description %}
Returns transaction details for a given transaction hash
{% endswagger-description %}

{% swagger-parameter in="path" name="hash" type="string" %}
Transaction hash
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": 1710928,
  "created_at": "2021-04-22T01:32:30.813232Z",
  "updated_at": "2021-04-22T01:32:30.813232Z",
  "time": "2021-04-22T01:32:24.299016Z",
  "height": 35404213,
  "hash": "3Hd4PWFJ2P94ynMAExW2QBYrmo2Jp16Z1LD2UpGKTU1x",
  "block_hash": "E4PjGYCGWScdVLYaJwzG85QUD77Wj4jj2Z8pXUeTwJyM",
  "sender": "congloi036.near",
  "receiver": "wrap.near",
  "gas_burnt": "7067930199552",
  "actions": [
    {
      "data": {
        "gas": 30000000000000,
        "deposit": "1250000000000000000000",
        "method_name": "storage_deposit"
      },
      "type": "FunctionCall"
    },
    {
      "data": {
        "gas": 30000000000000,
        "deposit": "61000000000000000000000000",
        "method_name": "near_deposit"
      },
      "type": "FunctionCall"
    },
    {
      "data": {
        "gas": 100000000000000,
        "deposit": "1",
        "method_name": "ft_transfer_call"
      },
      "type": "FunctionCall"
    }
  ],
  "actions_count": 3,
  "success": true
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Transaction not found" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}
