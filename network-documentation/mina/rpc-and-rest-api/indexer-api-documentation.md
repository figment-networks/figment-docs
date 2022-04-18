---
description: HTTP API documentation for the Mina Indexer API service provided by DataHub
---

# Indexer API Documentation

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/health" method="get" summary="Health" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/status" method="get" summary="Status" %}
{% swagger-description %}
Returns the current service status along with node version and sync status
{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/height" method="get" summary="Height" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/block" method="get" summary="Block" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/blocks" method="get" summary="Blocks Search" %}
{% swagger-description %}
Returns a set of blocks that match input parameters.
{% endswagger-description %}

{% swagger-parameter in="query" name="min_height" type="integer" %}
Start height
{% endswagger-parameter %}

{% swagger-parameter in="query" name="max_height" type="integer" %}
End height
{% endswagger-parameter %}

{% swagger-parameter in="query" name="creator" type="string" %}
Block producer public key
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
Number of blocks to return
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sort" type="string" %}
Sort field
{% endswagger-parameter %}

{% swagger-parameter in="query" name="order" type="string" %}
Sort order
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "height": 1490,
  "hash": "3NLF7dmJQpDaheV2KuTcAHXVuLjGorht25jhJN7uJTAPJvv5dWDS",
  "parent_hash": "3NLFdGM1q4CiTTmPUKnYywtqqNL6wdfiTnsi1HBeCBTPTsyXwi47",
  "time": "2021-03-05T21:46:08Z",
  "canonical": true,
  "ledger_hash": "jxt6GQM3CvK1nBYxQpSLhGxsFc9VydTnVdNfUsardf1TEFwpK7K",
  "snarked_ledger_hash": "jxz1rCy4CkDFjHCgjRvZ95m6so35wimW6EaPyBww2ATRcBPoq82",
  "creator": "B62qnG5JpGGtWKSL9S4emeoEjXzUF7dcuZtBY3nwmAPz3M6pTn92kFh",
  "coinbase": "1440000000000",
  "total_currency": "178498400000001000",
  "epoch": 0,
  "slot": 5174,
  "transactions_count": 134,
  "transactions_fees": 0,
  "snarkers_count": 9,
  "snark_jobs_count": 128,
  "snark_jobs_fees": "2632400000"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/blocks/{id}" method="get" summary="Block Details" %}
{% swagger-description %}
Returns block details and all associated information, like validators, snarkers, transactions.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Block number or hash
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "block": {
    "height": 6813,
    "hash": "3NL9a89zjZyxBBrsLbGozHMVe7GVthnQxsuBdzAHSzZrvypHZHKN",
    "parent_hash": "3NKPjq2FKRukRRcc76cdRES3XuHdVVoSqV98gqtMQujM5y1J6soE",
    "time": "2021-02-18T05:57:00Z",
    "canonical": true,
    "ledger_hash": "jxVAmBm5YJMkzpZrNyEzDmBZRys9SSULFEZBtjETjC9r4HiNjEv",
    "snarked_ledger_hash": "jxdVnHxmDhhbMNrzEcoMnC862Ft3TRDy1PMZAP2cDraYXMcU5kE",
    "creator": "B62qmyjqEtUEZrsBpUaiz18DCkwh1ovCrJboiHbDhpvH8JEoaag5fUP",
    "coinbase": "400000000000",
    "total_currency": "168372598057001000",
    "epoch": 0,
    "slot": 6439,
    "transactions_count": 2,
    "transactions_fees": 0,
    "snarkers_count": 1,
    "snark_jobs_count": 1,
    "snark_jobs_fees": "10000"
  },
  "creator": {
    "public_key": "B62qmyjqEtUEZrsBpUaiz18DCkwh1ovCrJboiHbDhpvH8JEoaag5fUP",
    "delegate": null,
    "balance": "2524136468248478",
    "balance_unknown": "2524136468248478",
    "stake": null,
    "nonce": 0,
    "start_height": 6535,
    "start_time": "2021-02-14T12:42:00Z",
    "last_height": 6813,
    "last_time": "2021-02-18T05:57:00Z"
  },
  "snark_jobs": [
    {
      "id": 27990,
      "height": 6813,
      "time": "2021-02-18T05:57:00Z",
      "prover": "B62qmo7wZEAZPZoao5AKRVJox9B9fgpvYAsPvYevSH7tWdTS7ny93Uu",
      "fee": "10000",
      "works_count": 2
    }
  ],
  "transactions": [
    {
      "id": 165318,
      "hash": "CkpZ1NULZG56Dbw4iaSy6gacUQHH4jzVb9iwMmGtiyz2n3oqjgY3x-0",
      "type": "coinbase",
      "block_hash": "3NL9a89zjZyxBBrsLbGozHMVe7GVthnQxsuBdzAHSzZrvypHZHKN",
      "block_height": 6813,
      "time": "2021-02-18T05:57:00Z",
      "sender": null,
      "receiver": "B62qmyjqEtUEZrsBpUaiz18DCkwh1ovCrJboiHbDhpvH8JEoaag5fUP",
      "amount": "400000000000",
      "fee": null,
      "nonce": null,
      "memo": null,
      "status": "applied",
      "failure_reason": null,
      "sequence_number": 0,
      "secondary_sequence_number": 0
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Block does not exist" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/block_stats" method="get" summary="Block Stats" %}
{% swagger-description %}
Returns aggregated block statistics
{% endswagger-description %}

{% swagger-parameter in="query" name="interval" type="string" %}
Stats interval
{% endswagger-parameter %}

{% swagger-parameter in="query" name="period" type="integer" %}
Stats period
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "time": "2021-02-18T06:00:00+00:00",
  "block_time_avg": 0,
  "blocks_count": 1,
  "validators_count": 1,
  "snarkers_count": 106,
  "jobs_count": 1,
  "jobs_amount": "10000",
  "transactions_count": 1,
  "transactions_amount": "400000000000",
  "payments_count": 0,
  "payments_amount": "0",
  "fee_transfers_count": 0,
  "fee_transfers_amount": "0",
  "coinbase_count": 1,
  "coinbase_amount": "400000000000"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/block_times" method="get" summary="Block Times" %}
{% swagger-description %}
Returns the average block production time for N latest blocks.
{% endswagger-description %}

{% swagger-parameter in="query" name="limit" type="integer" %}
Number of block to include in calculation
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/validators" method="get" summary="Validators" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/snarkers" method="get" summary="Snarkers" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/validators/{id}" method="get" summary="Validator stats" %}
{% swagger-description %}
Returns aggregated validator statistics
{% endswagger-description %}

{% swagger-parameter in="query" name="interval" type="string" %}
Stats interval
{% endswagger-parameter %}

{% swagger-parameter in="query" name="period" type="integer" %}
Stats period
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "time": "2021-03-05T21:00:00Z",
  "bucket": "h",
  "blocks_produced_count": 2,
  "delegations_count": 1,
  "delegations_amount": "22500000000000000"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/delegations" method="get" summary="Active delegations" %}
{% swagger-description %}
Returns active delegations
{% endswagger-description %}

{% swagger-parameter in="query" name="public_key" type="string" %}
Account public key
{% endswagger-parameter %}

{% swagger-parameter in="query" name="delegate" type="string" %}
Delegate account public key
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "public_key": "B62qpawbpmboCYmenkXaCQuQDSKBR8PXkDw1MTjkZTUrRcVPLzd6Hnr",
  "delegate": "B62qjAW7anRhWx7P5ikiH1zRSEzoJsfFDyjBC7hKsXcGZb4RTmZJ2Yj",
  "balance": "20000000000000"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/transactions" method="get" summary="Transaction Search" %}
{% swagger-description %}
Returns transactions that match search input parameters.
{% endswagger-description %}

{% swagger-parameter in="query" name="height" type="integer" %}
Block height. Can't be used with 

`block_hash`

.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="block_hash" type="string" %}
Block hash.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="account" type="string" %}
Transaction sender or receiver.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sender" type="string" %}
Sender public key.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="receiver" type="string" %}
Receiver public key.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="type" type="string" %}
Transaction type. Supports multiple comma-separate values.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="memo" type="string" %}
Transaction memo.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="start_time" type="string" %}
Period start time. Format 

`YYYY-MM-DD`

.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="end_time" type="string" %}
Period end time. Format: 

`YYYY-MM-DD`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="after_id" type="integer" %}
Start transaction ID. Can't be used with 

`before_id`

.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="before_id" type="integer" %}
End transaction ID. Can't be used with 

`after_id`

.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
Number of transactions to return
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": 58413,
  "hash": "CkpZfUe2CmkeXizqiup7hgM2zk2VAPkeY833976QfsSC95yiPVCA8",
  "type": "payment",
  "block_hash": "3NLF7dmJQpDaheV2KuTcAHXVuLjGorht25jhJN7uJTAPJvv5dWDS",
  "block_height": 1490,
  "time": "2021-03-05T21:46:08Z",
  "sender": "B62qjAW7anRhWx7P5ikiH1zRSEzoJsfFDyjBC7hKsXcGZb4RTmZJ2Yj",
  "receiver": "B62qokfNxSDJzYyyDQvqhCMAvURuSxoLxcjSNG92unBdNYt3nSXamsG",
  "amount": "1500000",
  "fee": "87923725",
  "nonce": 4063,
  "memo": "BeepBoop",
  "status": "failed",
  "failure_reason": "Amount_insufficient_to_create_account",
  "sequence_number": 121,
  "secondary_sequence_number": null
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Input error" %}
```javascript
{
  "error": "Invalid input",
  "status": 400
}
```
{% endswagger-response %}

{% swagger-response status="500" description="Server error" %}
```javascript
{
  "error": "Something went wrong",
  "status": 500
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/transactions/{hash}" method="get" summary="Transaction Details" %}
{% swagger-description %}
Returns transaction details
{% endswagger-description %}

{% swagger-parameter in="path" name="hash" type="string" %}
Transaction hash
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "id": 58413,
  "hash": "CkpZfUe2CmkeXizqiup7hgM2zk2VAPkeY833976QfsSC95yiPVCA8",
  "type": "payment",
  "block_hash": "3NLF7dmJQpDaheV2KuTcAHXVuLjGorht25jhJN7uJTAPJvv5dWDS",
  "block_height": 1490,
  "time": "2021-03-05T21:46:08Z",
  "sender": "B62qjAW7anRhWx7P5ikiH1zRSEzoJsfFDyjBC7hKsXcGZb4RTmZJ2Yj",
  "receiver": "B62qokfNxSDJzYyyDQvqhCMAvURuSxoLxcjSNG92unBdNYt3nSXamsG",
  "amount": "1500000",
  "fee": "87923725",
  "nonce": 4063,
  "memo": "BeepBoop",
  "status": "failed",
  "failure_reason": "Amount_insufficient_to_create_account",
  "sequence_number": 121,
  "secondary_sequence_number": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Not Found" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/accounts/{id}" method="get" summary="Account Details" %}
{% swagger-description %}
Returns information about account
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Account public key
{% endswagger-parameter %}

{% swagger-response status="200" description="Success" %}
```javascript
{
  "public_key": "B62qmL7bWrMRuYr8hCT9p7L7jUho7oajSTohtFYSr8XYM3QoWyf8VL6",
  "delegate": null,
  "balance": "1941653020586758",
  "balance_unknown": "1941653020586758",
  "stake": "1941653020586758",
  "nonce": 0,
  "start_height": 5860,
  "start_time": "2021-02-09T11:51:00-06:00",
  "last_height": 7251,
  "last_time": "2021-02-21T12:06:00-06:00"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Account not found" %}
```javascript
{
  "error": "record not found",
  "status": 404
}
```
{% endswagger-response %}
{% endswagger %}
