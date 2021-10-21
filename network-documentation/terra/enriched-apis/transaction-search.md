---
description: Learn how to use the Transaction Search API on Terra
---

# Transaction Search

Test out our Transaction Search API today with [**DataHub**](https://datahub.figment.io/sign\_up?service=terra)!

{% swagger baseUrl="https://terra--search.datahub.figment.io/transactions_search" path=" " method="post" summary="transactions_search" %}
{% swagger-description %}
Transaction Search allows users to filter and query by account, transaction type, and date range. Users can also search by memo field and logs.
{% endswagger-description %}

{% swagger-parameter in="body" name="network" type="string" %}
Network identifier to search in. In this case, 

`terra`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="array" %}
The account identifier to look for. This searches for all account IDs which exist in transaction, including senders, recipients, validators, feeders, etc.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="after_height" type="integer" %}
Gets all transactions bigger than given height. Has to be bigger than BeforeHeight
{% endswagger-parameter %}

{% swagger-parameter in="body" name="after_time" type="string" %}
The time of transaction (if not given by chain API, the same as block)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="before_height" type="integer" %}
Gets all transactions lower than given height. Has to be lesser than AfterHeight
{% endswagger-parameter %}

{% swagger-parameter in="body" name="before_time" type="string" %}
The time of transaction (if not given by the chain API, the same as block)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="block_hash" type="string" %}
The hash of block to get transaction from
{% endswagger-parameter %}

{% swagger-parameter in="body" name="chain_ids" type="array" %}
ChainID to search in. In this case, 

`columbus-3`

 or 

`columbus-4`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="epoch" type="string" %}
Epoch of the transaction
{% endswagger-parameter %}

{% swagger-parameter in="body" name="hash" type="string" %}
The hash of the transaction
{% endswagger-parameter %}

{% swagger-parameter in="body" name="height" type="integer" %}
Height of the transactions to get
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" type="integer" %}
Limit how many transaction records to get in one request (default: 100, maximum: 1000)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memo" type="string" %}
Sets full text search for memo field
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offset" type="integer" %}
Offset the next X number of records
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiver" type="array" %}
Looks for transactions that include given account IDs
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender" type="array" %}
Looks for transactions that include given account IDs
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="array" %}
The list of types of transactions (see below for full list of parameters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="with_raw" type="boolean" %}
Include base64 raw request in search response
{% endswagger-parameter %}

{% swagger-parameter in="body" name="with_raw_log" type="boolean" %}
Include base64 raw log from search response. Defaults to 

`false`
{% endswagger-parameter %}

{% swagger-response status="200" description="Success response" %}
```javascript
{
  "block_hash": "string",
  "chain_id": "string",
  "created_at": "2020-10-15T20:38:09.017Z",
  "epoch": "string",
  "events": [
    {
      "id": "string",
      "kind": "string",
      "sub": [
        {
          "action": "string",
          "additional": {
            "additionalProp1": [
              "string"
            ],
            "additionalProp2": [
              "string"
            ],
            "additionalProp3": [
              "string"
            ]
          },
          "amount": {
            "additionalProp1": {
              "currency": "string",
              "exp": 0,
              "numeric": {},
              "text": "string"
            },
            "additionalProp2": {
              "currency": "string",
              "exp": 0,
              "numeric": {},
              "text": "string"
            },
            "additionalProp3": {
              "currency": "string",
              "exp": 0,
              "numeric": {},
              "text": "string"
            }
          },
          "completion": "2020-10-15T20:38:09.017Z",
          "error": {
            "message": "string"
          },
          "module": "string",
          "node": {
            "additionalProp1": [
              {
                "detail": {
                  "contact": "string",
                  "description": "string",
                  "name": "string",
                  "website": "string"
                },
                "id": "string"
              }
            ],
            "additionalProp2": [
              {
                "detail": {
                  "contact": "string",
                  "description": "string",
                  "name": "string",
                  "website": "string"
                },
                "id": "string"
              }
            ],
            "additionalProp3": [
              {
                "detail": {
                  "contact": "string",
                  "description": "string",
                  "name": "string",
                  "website": "string"
                },
                "id": "string"
              }
            ]
          },
          "nonce": "string",
          "recipient": [
            {
              "account": {
                "detail": {
                  "contact": "string",
                  "description": "string",
                  "name": "string",
                  "website": "string"
                },
                "id": "string"
              },
              "amounts": [
                {
                  "currency": "string",
                  "exp": 0,
                  "numeric": {},
                  "text": "string"
                }
              ]
            }
          ],
          "sender": [
            {
              "account": {
                "detail": {
                  "contact": "string",
                  "description": "string",
                  "name": "string",
                  "website": "string"
                },
                "id": "string"
              },
              "amounts": [
                {
                  "currency": "string",
                  "exp": 0,
                  "numeric": {},
                  "text": "string"
                }
              ]
            }
          ],
          "type": [
            "string"
          ]
        }
      ]
    }
  ],
  "gas_used": 0,
  "gas_wanted": 0,
  "hash": "string",
  "height": 0,
  "id": [
    0
  ],
  "memo": "string",
  "raw": [
    0
  ],
  "raw_log": [
    0
  ],
  "time": "2020-10-15T20:38:09.017Z",
  "transaction_fee": [
    {
      "currency": "string",
      "exp": 0,
      "numeric": {},
      "text": "string"
    }
  ],
  "updated_at": "2020-10-15T20:38:09.017Z",
  "version": "string",
  "has_errors": false
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Bad parameters sent" %}
```javascript
{
  "error": "Bad parameters sent"
}
```
{% endswagger-response %}

{% swagger-response status="406" description="Not acceptable content type" %}
```javascript
{
  "error": "Not acceptable content type"
}
```
{% endswagger-response %}

{% swagger-response status="500" description="Internal/Other server error while processing request" %}
```javascript
{
  "error": "Something bad happened"
}
```
{% endswagger-response %}
{% endswagger %}

## **Transaction Types**

List of currently supporter transaction types in cosmos-worker are (listed by modules):

| **Module**       | Type                                                                                                        |
| ---------------- | ----------------------------------------------------------------------------------------------------------- |
| **bank**         | `multisend` , `send`                                                                                        |
| **crisis**       | `verify_invariant`                                                                                          |
| **distribution** | `withdraw_validator_commission`, `set_withdraw_address`, `withdraw_delegator_reward`, `fund_community_pool` |
| **evidence**     | `submit_evidence`                                                                                           |
| **gov**          | `deposit`, `vote`, `submit_proposal`                                                                        |
| **slashing**     | `unjail`                                                                                                    |
| **staking**      | `begin_unbonding`, `edit_validator`, `create_validator` , `delegate`, `begin_redelegate`                    |
| **internal**     | `error`                                                                                                     |

## Example Request

```javascript
{
    "network": "terra",
    "limit": 1
}
```

## Example Response

```javascript
[
    {
        "id": "135e76d6-c26f-4472-a6a0-49f8b4d87421",
        "hash": "E6F6916FD7F50BC9BCB7CDBB33DDB22176103E8BBA02441A5CA74517A41DD003",
        "block_hash": "369FDA008FDABB37A34078502EAEB1250DD497854896C947A25677D64469D081",
        "height": 797187,
        "chain_id": "columbus-4",
        "time": "2020-12-01T20:14:25.852279Z",
        "transaction_fee": [
            {
                "text": "206943",
                "currency": "ukrw",
                "numeric": 206943
            }
        ],
        "gas_wanted": 116227,
        "gas_used": 81146,
        "version": "0.0.1",
        "has_errors": false,
        "events": [
            {
                "id": "0",
                "kind": "aggregateexchangeratevote",
                "sub": [
                    {
                        "type": [
                            "aggregateexchangerateprevote"
                        ],
                        "module": "oracle",
                        "node": {
                            "feeder": [
                                {
                                    "id": "terra1qt7kqljer7fxzudqdyhx87l7wreeef53s9uxqw"
                                }
                            ],
                            "validator": [
                                {
                                    "id": "terravaloper1qt7kqljer7fxzudqdyhx87l7wreeef53s2smsa"
                                }
                            ]
                        },
                        "additional": {
                            "exchangeRates": [
                                "428.395216522890552458ukrw",
                                "1102.267345679666643166umnt",
                                "0.270833380822064165usdr",
                                "0.387227045713562639uusd"
                            ],
                            "salt": [
                                "a5b1"
                            ]
                        }
                    }
                ]
            },
            {
                "id": "1",
                "kind": "aggregateexchangerateprevote",
                "sub": [
                    {
                        "type": [
                            "aggregateexchangerateprevote"
                        ],
                        "module": "oracle",
                        "node": {
                            "feeder": [
                                {
                                    "id": "terra1qt7kqljer7fxzudqdyhx87l7wreeef53s9uxqw"
                                }
                            ],
                            "validator": [
                                {
                                    "id": "terravaloper1qt7kqljer7fxzudqdyhx87l7wreeef53s2smsa"
                                }
                            ]
                        },
                        "additional": {
                            "hash": [
                                "7a4d9fd06c87e9e26688dc77f2f42d64172e2e6f"
                            ]
                        }
                    }
                ]
            }
        ]
    }
]
```

If you need help with this API or simply want to share with other builders, you can [**join our community today**](https://discord.gg/fszyM7K)!
