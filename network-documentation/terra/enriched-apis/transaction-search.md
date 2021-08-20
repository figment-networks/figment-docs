---
description: Learn how to use the Transaction Search API on Terra
---

# Transaction Search

Test out our Transaction Search API today with [**DataHub**](https://datahub.figment.io/sign_up?service=terra)!

{% api-method method="post" host="https://terra--search.datahub.figment.io/transactions\_search" path=" " %}
{% api-method-summary %}
transactions\_search
{% endapi-method-summary %}

{% api-method-description %}
Transaction Search allows users to filter and query by account, transaction type, and date range. Users can also search by memo field and logs.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="network" type="string" required=true %}
Network identifier to search in. In this case, `terra`
{% endapi-method-parameter %}

{% api-method-parameter name="account" type="array" required=false %}
The account identifier to look for. This searches for all account IDs which exist in transaction, including senders, recipients, validators, feeders, etc.
{% endapi-method-parameter %}

{% api-method-parameter name="after\_height" type="integer" required=false %}
Gets all transactions bigger than given height. Has to be bigger than BeforeHeight
{% endapi-method-parameter %}

{% api-method-parameter name="after\_time" type="string" required=false %}
The time of transaction \(if not given by chain API, the same as block\)
{% endapi-method-parameter %}

{% api-method-parameter name="before\_height" type="integer" required=false %}
Gets all transactions lower than given height. Has to be lesser than AfterHeight
{% endapi-method-parameter %}

{% api-method-parameter name="before\_time" type="string" required=false %}
The time of transaction \(if not given by the chain API, the same as block\)
{% endapi-method-parameter %}

{% api-method-parameter name="block\_hash" type="string" required=false %}
The hash of block to get transaction from
{% endapi-method-parameter %}

{% api-method-parameter name="chain\_ids" type="array" required=false %}
ChainID to search in. In this case, `columbus-3` or `columbus-4`
{% endapi-method-parameter %}

{% api-method-parameter name="epoch" type="string" required=false %}
Epoch of the transaction
{% endapi-method-parameter %}

{% api-method-parameter name="hash" type="string" required=false %}
The hash of the transaction
{% endapi-method-parameter %}

{% api-method-parameter name="height" type="integer" required=false %}
Height of the transactions to get
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
Limit how many transaction records to get in one request \(default: 100, maximum: 1000\)
{% endapi-method-parameter %}

{% api-method-parameter name="memo" type="string" required=false %}
Sets full text search for memo field
{% endapi-method-parameter %}

{% api-method-parameter name="offset" type="integer" required=false %}
Offset the next X number of records
{% endapi-method-parameter %}

{% api-method-parameter name="receiver" type="array" required=false %}
Looks for transactions that include given account IDs
{% endapi-method-parameter %}

{% api-method-parameter name="sender" type="array" required=false %}
Looks for transactions that include given account IDs
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="array" required=false %}
The list of types of transactions \(see below for full list of parameters\)
{% endapi-method-parameter %}

{% api-method-parameter name="with\_raw" type="boolean" required=false %}
Include base64 raw request in search response
{% endapi-method-parameter %}

{% api-method-parameter name="with\_raw\_log" type="boolean" required=false %}
Include base64 raw log from search response. Defaults to `false`
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success response
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Bad parameters sent
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Bad parameters sent"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=406 %}
{% api-method-response-example-description %}
Not acceptable content type
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Not acceptable content type"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Internal/Other server error while processing request
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Something bad happened"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## **Transaction Types**

List of currently supporter transaction types in cosmos-worker are \(listed by modules\):

| **Module** | Type |
| :--- | :--- |
| **bank** | `multisend` , `send` |
| **crisis** | `verify_invariant` |
| **distribution** | `withdraw_validator_commission`, `set_withdraw_address`, `withdraw_delegator_reward`, `fund_community_pool` |
| **evidence** | `submit_evidence` |
| **gov** | `deposit`, `vote`, `submit_proposal` |
| **slashing** | `unjail` |
| **staking** | `begin_unbonding`, `edit_validator`, `create_validator` , `delegate`, `begin_redelegate` |
| **internal** | `error` |

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

