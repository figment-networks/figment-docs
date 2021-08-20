---
description: Learn how to interact with Figment's Miner Reputation System API
---

# Miner Reputation System API

## Overview

The Miner Reputation System API provides users with all of the necessary information for assessing the reputation of storage miners on the Filecoin network.

By tracking storage capacity, sector faults and deal slashes of every storage miner, the API calculates a reputation score, which can be used by network participants to compare and choose a reliable miner.

Additionally, the API allows users to look up account details \(such as balance\) or retrieve a list of transactions for a given account. It also keeps a history of miner-related events, such as storage capacity changes, sector faults, and deal slashes.

Check out the API documentation below and sign up to [**DataHub**](https://datahub.figment.io/sign_up?service=filecoin) to test it out.

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/miners" %}
{% api-method-summary %}
Get miners
{% endapi-method-summary %}

{% api-method-description %}
Lists all storage miners for a given epoch. If no epoch is given, the data is returned for the most recent epoch.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
The page number
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
The record count limit
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "page": 1,
  "limit": 100,
  "total_count": 3,
  "total_pages": 1,
  "records": [
    {
      "address": "f01002",
      "sector_size": 34359738368,
      "raw_byte_power": 26388279066624,
      "quality_adj_power": 263882790666240,
      "relative_power": 0.33333334,
      "deals_count": 768,
      "slashed_deals_count": 0,
      "faults_count": 0,
      "score": 543
    },
    {
      "address": "f01000",
      "sector_size": 34359738368,
      "raw_byte_power": 26388279066624,
      "quality_adj_power": 263882790666240,
      "relative_power": 0.33333334,
      "deals_count": 768,
      "slashed_deals_count": 0,
      "faults_count": 0,
      "score": 543
    },
    {
      "address": "f01001",
      "sector_size": 34359738368,
      "raw_byte_power": 26388279066624,
      "quality_adj_power": 263882790666240,
      "relative_power": 0.33333334,
      "deals_count": 768,
      "slashed_deals_count": 0,
      "faults_count": 0,
      "score": 543
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/miners/:address" %}
{% api-method-summary %}
Get miner
{% endapi-method-summary %}

{% api-method-description %}
Returns storage miner details for a given epoch. If no epoch is given, the data is returned for the most recent epoch.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=true %}
The ID address of a storage miner
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "address": "f01000",
  "sector_size": 34359738368,
  "raw_byte_power": 26388279066624,
  "quality_adj_power": 263882790666240,
  "relative_power": 0.33333334,
  "deals_count": 768,
  "slashed_deals_count": 0,
  "faults_count": 0,
  "score": 543
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "Not Found"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/miners/:address/events" %}
{% api-method-summary %}
Get miner events
{% endapi-method-summary %}

{% api-method-description %}
Lists network events related to a storage miner for a given epoch and kind. If no epoch is given, the data is returned for all epochs. If no kind is given, the data is returned for all event kinds.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=true %}
The ID address of a storage miner
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}

{% api-method-parameter name="kind" type="string" required=false %}
The event kind
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
The page number
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
The record count limit
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "page": 1,
  "limit": 2,
  "total_count": 768,
  "total_pages": 384,
  "records": [
    {
      "height": 0,
      "miner_address": "f01000",
      "kind": "new_deal",
      "data": {
        "client_address": "f0100",
        "deal_id": "396",
        "is_verified": true,
        "piece_size": "34359738368",
        "storage_price": "0"
      }
    },
    {
      "height": 0,
      "miner_address": "f01000",
      "kind": "new_deal",
      "data": {
        "client_address": "f0100",
        "deal_id": "351",
        "is_verified": true,
        "piece_size": "34359738368",
        "storage_price": "0"
      }
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/top\_miners" %}
{% api-method-summary %}
Get top miners
{% endapi-method-summary %}

{% api-method-description %}
Lists top 100 storage miners for a given epoch based on their reputation score. If no epoch is given, the data is returned for the most recent epoch.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "address": "f01002",
    "sector_size": 34359738368,
    "raw_byte_power": 26388279066624,
    "quality_adj_power": 263882790666240,
    "relative_power": 0.33333334,
    "deals_count": 768,
    "slashed_deals_count": 0,
    "faults_count": 0,
    "score": 300
  },
  {
    "address": "f01000",
    "sector_size": 34359738368,
    "raw_byte_power": 26388279066624,
    "quality_adj_power": 263882790666240,
    "relative_power": 0.33333334,
    "deals_count": 768,
    "slashed_deals_count": 0,
    "faults_count": 0,
    "score": 200
  },
  {
    "address": "f01001",
    "sector_size": 34359738368,
    "raw_byte_power": 26388279066624,
    "quality_adj_power": 263882790666240,
    "relative_power": 0.33333334,
    "deals_count": 768,
    "slashed_deals_count": 0,
    "faults_count": 0,
    "score": 100
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/transactions" %}
{% api-method-summary %}
Get transactions
{% endapi-method-summary %}

{% api-method-description %}
Lists all transactions for a given epoch. If no epoch is given, the data is returned for all epochs.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
The page number
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
The record count limit
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "page": 1,
  "limit": 100,
  "total_count": 5,
  "total_pages": 1,
  "records": [
    {
      "cid": "bafy2bzaceb5sbhzn6i7bltslktujctr2rcd5f2nby6ernapn6ml74xmv3fnga",
      "height": 1,
      "from": "f3vfs6f7tagrcpnwv65wq3leznbajqyg77bmijrpvoyjv3zjyi3urq25vigfbs3ob6ug5xdihajumtgsxnz2pa",
      "to": "f01000",
      "value": "0",
      "method": "ChangePeerID"
    },
    {
      "cid": "bafy2bzaceaoo4msi45t3pbhfov3guu5l34ektpjhuftyddy2rvhf2o5ajijle",
      "height": 1,
      "from": "f3xf54js52xz74sw55pebpfr3q5uiogntgwmk5iq7jpvh4a66kb6loswq6filtmuk2b72wk7mhfpmms4swha6q",
      "to": "f01001",
      "value": "0",
      "method": "ChangePeerID"
    },
    {
      "cid": "bafy2bzaceb2cujbpoijbkyov7yb2lmzesacq24d7mtled7yybwkmrla5db354",
      "height": 1,
      "from": "f3xf54js52xz74sw55pebpfr3q5uiogntgwmk5iq7jpvh4a66kb6loswq6filtmuk2b72wk7mhfpmms4swha6q",
      "to": "f01001",
      "value": "0",
      "method": "ChangePeerID"
    },
    {
      "cid": "bafy2bzacebmapwdgjsod5ytgbcrsqumt77pynzt44l43homumj6l5h7yrhu7u",
      "height": 1,
      "from": "f3qfjszg5oe6ouqexl5uzrev7ht4b5q6fyead25hvt76rbppsaabjn6fwzqeuqtkk5f6hrsoray76oind2yaea",
      "to": "f01002",
      "value": "0",
      "method": "ChangePeerID"
    },
    {
      "cid": "bafy2bzacebghgexoolgk3rn4h4v3qteodnjkycc4i2ksce6hx7ekfcrc57a36",
      "height": 1,
      "from": "f3qfjszg5oe6ouqexl5uzrev7ht4b5q6fyead25hvt76rbppsaabjn6fwzqeuqtkk5f6hrsoray76oind2yaea",
      "to": "f01002",
      "value": "0",
      "method": "ChangePeerID"
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/accounts/:address" %}
{% api-method-summary %}
Get account
{% endapi-method-summary %}

{% api-method-description %}
Returns account details for a given address. The address could be either an ID address or an account key address.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=true %}
The address of an account \(ID or public key\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": "f0100",
  "public_key": "f3vfs6f7tagrcpnwv65wq3leznbajqyg77bmijrpvoyjv3zjyi3urq25vigfbs3ob6ug5xdihajumtgsxnz2pa",
  "balance": "0.482788569758516947",
  "nonce": 43,
  "transactions_sent": 1,
  "transactions_received": 0
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "actor not found"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/accounts/:address/transactions" %}
{% api-method-summary %}
Get account transactions
{% endapi-method-summary %}

{% api-method-description %}
Lists sent and received transactions for a given account. The address of the account could be either an ID address or an account key address. If no epoch is given, the data is returned for all epochs.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=true %}
The address of an account \(ID or public key\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
The page number
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
The record count limit
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "page": 1,
  "limit": 100,
  "total_count": 1,
  "total_pages": 1,
  "records": [
    {
      "cid": "bafy2bzaceb5sbhzn6i7bltslktujctr2rcd5f2nby6ernapn6ml74xmv3fnga",
      "height": 1,
      "from": "f3vfs6f7tagrcpnwv65wq3leznbajqyg77bmijrpvoyjv3zjyi3urq25vigfbs3ob6ug5xdihajumtgsxnz2pa",
      "to": "f01000",
      "value": "0",
      "method": "ChangePeerID"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid address: unknown address network"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/events" %}
{% api-method-summary %}
Get events
{% endapi-method-summary %}

{% api-method-description %}
Lists all network events for a given epoch and kind. If no epoch is given, the data is returned for all epochs. If no kind is given, the data is returned for all event kinds.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
The epoch number
{% endapi-method-parameter %}

{% api-method-parameter name="kind" type="string" required=false %}
The event kind
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=false %}
The page number
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
The record count limit
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "page": 1,
  "limit": 3,
  "total_count": 2304,
  "total_pages": 768,
  "records": [
    {
      "height": 0,
      "miner_address": "f01001",
      "kind": "new_deal",
      "data": {
        "client_address": "f0101",
        "deal_id": "1470",
        "is_verified": true,
        "piece_size": "34359738368",
        "storage_price": "0"
      }
    },
    {
      "height": 0,
      "miner_address": "f01000",
      "kind": "new_deal",
      "data": {
        "client_address": "f0100",
        "deal_id": "351",
        "is_verified": true,
        "piece_size": "34359738368",
        "storage_price": "0"
      }
    },
    {
      "height": 0,
      "miner_address": "f01001",
      "kind": "new_deal",
      "data": {
        "client_address": "f0101",
        "deal_id": "1074",
        "is_verified": true,
        "piece_size": "34359738368",
        "storage_price": "0"
      }
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/health" %}

{% api-method method="get" host="https://filecoin--mainnet--miner-rep-api.datahub.figment.io" path="/status" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}
Returns the status of the synchronization process.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "current_epoch": 340610,
  "last_synced_epoch": 340600
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "driver: bad connection"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Event Kinds

| Kind | Description |
| :--- | :--- |
| `storage_capacity_change` | A change of miner's storage capacity |
| `slashed_deal` | A slash of a miner's deal |
| `sector_fault` | An increase in miner's faults |
| `sector_recovery` | A decrease in miner's faults |

