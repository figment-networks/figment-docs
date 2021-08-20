---
description: HTTP API documentation for the Mina Indexer API service provided by DataHub
---

# Indexer API Documentation

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/health" %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/status" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}
Returns the current service status along with node version and sync status
{% endapi-method-description %}

{% api-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/height" %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/block" %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/blocks" %}
{% api-method-summary %}
Blocks Search
{% endapi-method-summary %}

{% api-method-description %}
Returns a set of blocks that match input parameters.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="min\_height" type="integer" required=false %}
Start height
{% endapi-method-parameter %}

{% api-method-parameter name="max\_height" type="integer" required=false %}
End height
{% endapi-method-parameter %}

{% api-method-parameter name="creator" type="string" required=false %}
Block producer public key
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
Number of blocks to return
{% endapi-method-parameter %}

{% api-method-parameter name="sort" type="string" required=false %}
Sort field
{% endapi-method-parameter %}

{% api-method-parameter name="order" type="string" required=false %}
Sort order
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/blocks/{id}" %}
{% api-method-summary %}
Block Details
{% endapi-method-summary %}

{% api-method-description %}
Returns block details and all associated information, like validators, snarkers, transactions.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Block number or hash
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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Block does not exist
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

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/block\_stats" %}
{% api-method-summary %}
Block Stats
{% endapi-method-summary %}

{% api-method-description %}
Returns aggregated block statistics
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="interval" type="string" required=false %}
Stats interval
{% endapi-method-parameter %}

{% api-method-parameter name="period" type="integer" required=false %}
Stats period
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/block\_times" %}
{% api-method-summary %}
Block Times
{% endapi-method-summary %}

{% api-method-description %}
Returns the average block production time for N latest blocks.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="limit" type="integer" required=false %}
Number of block to include in calculation
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/validators" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/snarkers" %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/validators/{id}" %}
{% api-method-summary %}
Validator stats
{% endapi-method-summary %}

{% api-method-description %}
Returns aggregated validator statistics
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="interval" type="string" required=false %}
Stats interval
{% endapi-method-parameter %}

{% api-method-parameter name="period" type="integer" required=false %}
Stats period
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

```javascript
{
  "time": "2021-03-05T21:00:00Z",
  "bucket": "h",
  "blocks_produced_count": 2,
  "delegations_count": 1,
  "delegations_amount": "22500000000000000"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/delegations" %}
{% api-method-summary %}
Active delegations
{% endapi-method-summary %}

{% api-method-description %}
Returns active delegations
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="public\_key" type="string" required=false %}
Account public key
{% endapi-method-parameter %}

{% api-method-parameter name="delegate" type="string" required=false %}
Delegate account public key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

```javascript
{
  "public_key": "B62qpawbpmboCYmenkXaCQuQDSKBR8PXkDw1MTjkZTUrRcVPLzd6Hnr",
  "delegate": "B62qjAW7anRhWx7P5ikiH1zRSEzoJsfFDyjBC7hKsXcGZb4RTmZJ2Yj",
  "balance": "20000000000000"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/transactions" %}
{% api-method-summary %}
Transaction Search
{% endapi-method-summary %}

{% api-method-description %}
Returns transactions that match search input parameters.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="height" type="integer" required=false %}
Block height. Can't be used with `block_hash`.
{% endapi-method-parameter %}

{% api-method-parameter name="block\_hash" type="string" required=false %}
Block hash.
{% endapi-method-parameter %}

{% api-method-parameter name="account" type="string" required=false %}
Transaction sender or receiver.
{% endapi-method-parameter %}

{% api-method-parameter name="sender" type="string" required=false %}
Sender public key.
{% endapi-method-parameter %}

{% api-method-parameter name="receiver" type="string" required=false %}
Receiver public key.
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
Transaction type. Supports multiple comma-separate values.
{% endapi-method-parameter %}

{% api-method-parameter name="memo" type="string" required=false %}
Transaction memo.
{% endapi-method-parameter %}

{% api-method-parameter name="start\_time" type="string" required=false %}
Period start time. Format `YYYY-MM-DD`.
{% endapi-method-parameter %}

{% api-method-parameter name="end\_time" type="string" required=false %}
Period end time. Format: `YYYY-MM-DD`
{% endapi-method-parameter %}

{% api-method-parameter name="after\_id" type="integer" required=false %}
Start transaction ID. Can't be used with `before_id`.
{% endapi-method-parameter %}

{% api-method-parameter name="before\_id" type="integer" required=false %}
End transaction ID. Can't be used with `after_id`.
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
Number of transactions to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Input error
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Invalid input",
  "status": 400
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Server error
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Something went wrong",
  "status": 500
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/transactions/{hash}" %}
{% api-method-summary %}
Transaction Details
{% endapi-method-summary %}

{% api-method-description %}
Returns transaction details
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="hash" type="string" required=true %}
Transaction hash
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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Not Found
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

{% api-method method="get" host="https://mina--devnet--indexer.datahub.figment.io/apikey/YOURAPIKEY" path="/accounts/{id}" %}
{% api-method-summary %}
Account Details
{% endapi-method-summary %}

{% api-method-description %}
Returns information about account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Account public key
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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Account not found
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

