---
description: Learn how to use the Transaction Search API on Polkadot
---

# Transaction Search

Test out our Transaction Search API today with [**DataHub**](https://datahub.figment.io/sign\_up?service=polkadot)!

{% swagger baseUrl="https://polkadot--search.datahub.figment.io/transactions_search" path=" " method="post" summary="transactions_search" %}
{% swagger-description %}
Transaction Search allows users to filter and query by account, event type, and date range.
{% endswagger-description %}

{% swagger-parameter in="body" name="network" type="string" %}
Network identifier to search in. In this case, 

`polkadot`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="array" %}
The account identifier to look for. This searches for all account IDs which exist inside transaction events.
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

`mainnet`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="epoch" type="string" %}
Era the transaction occurred,
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
The list of types of transaction events (see below for full list of parameters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="with_raw" type="boolean" %}
Include base64 raw rtransaction data in search response. Defaults to 

`false`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="with_raw_log" type="boolean" %}
Include base64 raw events from search response. Defaults to 

`false`
{% endswagger-parameter %}

{% swagger-response status="200" description="Success response" %}
```javascript
{
    "id": "string",
    "hash": "string",
    "block_hash": "string",
    "chain_id": "string",
    "time": "2020-10-15T20:38:09.017Z",
    "height": 0,
    "epoch": "string",
    "transaction_fee": [
        {
            "text": "string",
            "currency": "string",
            "numeric": {},
            "exp": 0
        }
    ],
    "events": [
      {
        "id": "string",
        "kind": "string",
        "type": [
            "string"
        ],
        "module": "string",
        "sub": [
          {
            "id": "string",
            "type": [
                "string"
            ],
            "module": "string",

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
            "node": {
              "additionalProp1": [
                {
                  "id": "string"
                }
              ],
              "additionalProp2": [
                {
                  "id": "string"
                }
              ],
              "additionalProp3": [
                {
                  "id": "string"
                }
              ]
            },
            "nonce": "string",
            "recipient": [
              {
                "account": {
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
            ]
          }
        ]
      }
    ],
    "raw": [
      0
    ],
    "raw_log": [
      0
    ],
    "updated_at": "2020-10-15T20:38:09.017Z",
    "version": "string",
    "has_errors": false,
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

List of currently supported sub event types in polkadot-worker are (listed by modules):

| **Module**             | Type                                                                                                                                                                                                |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **balances**           | `balanceset`, `deposit`, `dustlost`, `endowed`, `reserverepatriated`, `reserved`, `transfer`, `unreserved`                                                                                          |
| **council**            | `approved`, `closed`, `disapproved`, `executed`, `proposed`, `voted`                                                                                                                                |
| **democracy**          | `cancelled`, `delegated`, `preimagenoted`, `preimagereaped`, `proposed`, `started`, `undelegated`                                                                                                   |
| **identity**           | `identitycleared`, `identitykilled`, `identityset`, `judgementgiven`, `judgementrequested`, `judgementunrequested`, `registraradded`, `subidentityadded`, `subidentiyremoved`, `subidentityrevoked` |
| **indices**            | `indexassigned`, `indexfreed`, `indexfrozen`                                                                                                                                                        |
| **multisig**           | `multisigapproval`, `multisigcancelled`, `multisigexecuted`, `newmultisig`                                                                                                                          |
| **proxy**              | `bonded`, `reward`, `slash`                                                                                                                                                                         |
| **staking**            | `bonded`, `reward`, `slash`                                                                                                                                                                         |
| **system**             | `extrinsicfailed`, `extrinsicsuccess`, `killedaccount`, `newaccount`                                                                                                                                |
| **technicalcommittee** | `approved`, `closed`, `disapproved`, `executed`, `memberexecuted`, `proposed`, `voted`                                                                                                              |
| **tips**               | `newtip`, `tipclosed`, `tipclosing`, `tipretracted`, `tipslashed`                                                                                                                                   |
| **treasury**           | `proposed`, `rejected`                                                                                                                                                                              |
| **utility**            | `batchcompleted`, `batchinterrupted`                                                                                                                                                                |
| **vesting**            | `vestingupdated`, `vestingcompleted`                                                                                                                                                                |

List of currently supported extrinsic event types in polkadot-worker are (listed by modules):

| **Module**                     | Type                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **authorship**                 | `setuncles`                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **babe**                       | `planconfigchange`, `reportequivocation`, `reportequivocationunsigned`                                                                                                                                                                                                                                                                                                                                                                              |
| **balances**                   | `forcetransfer`, `setbalance`, `transfer`, `transferall`, `transferkeepalive`                                                                                                                                                                                                                                                                                                                                                                       |
| **bounties**                   | `acceptcurator`, `approvebounty`, `awardbounty`, `claimbounty`, `closebounty`, `extendbountyexpiry`, `proposecurator`, `unassigncurator`                                                                                                                                                                                                                                                                                                            |
| **claims**                     | `attest`, `claim`, `claimattest`, `mintclaim`, `moveclaim`                                                                                                                                                                                                                                                                                                                                                                                          |
| **council**                    | `close`, `disapproveproposal`, `execute`, `propose`, `setmembers`, `vote`                                                                                                                                                                                                                                                                                                                                                                           |
| **democracy**                  | `blacklist`, `cancelproposal`, `cancelqueued`, `cancelreferendum`, `clearpublicproposals`, `delegate`, `emergencycancel`, `enactproposal`, `externalproposal`, `externalpropose`, `externalproposedefault`, `fasttrack`, `noteimminentpreimage`, `noteimminentpreimageoperational`, `notepreimage`, `notepreimageoperational`, `propose`, `reappreimage`, `removeothervote`, `removevote`, `second`, `undelegate`, `unlock`, `vetoexternal`, `vote` |
| **electionprovidermultiphase** | `setemergencyelectionresult`, `setminimumuntrustedsource`, `submitunsigned`                                                                                                                                                                                                                                                                                                                                                                         |
| **grandpa**                    | `notestalled`, `reportequivocation`, `reportequivocationunsigned`                                                                                                                                                                                                                                                                                                                                                                                   |
| **identity**                   | `addregistrar`, `addsub`, `cancelrequest`, `clearidentity`, `killidentity`, `providejudgement`, `quitsub`, `removesub`, `renamesub`, `requestjudgement`, `setaccountid`, `setfee`, `setfields`, `setidentity`, `setsubs`                                                                                                                                                                                                                            |
| **indices**                    | `claim`, `forcetransfer`, `free`, `freeze`, `transfer`                                                                                                                                                                                                                                                                                                                                                                                              |
| **imonline**                   | `heartbeat`                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **multisig**                   | `approveasmulti`, `asmulti`, `asmultithreshold1`, `cancelasmulti`                                                                                                                                                                                                                                                                                                                                                                                   |
| **phragmenelection**           | `cleandefunctvoters`, `removemember`, `removevoter`, `renouncecandidacy`, `submitcandidacy`                                                                                                                                                                                                                                                                                                                                                         |
| **proxy**                      | `addproxy`, `announce`, `anonymous`, `killanonymous`, `proxy`, `proxyannounced`, `rejectannouncement`, `removeannouncement`, `removeproxies`, `removeproxy`                                                                                                                                                                                                                                                                                         |
| **scheduler**                  | `cancel`, `cancelnamed`, `schedule`, `scheduleafter`, `schedulenamed`, `schedulenamedafter`                                                                                                                                                                                                                                                                                                                                                         |
| **session**                    | `purgekeys`, `setkeys`                                                                                                                                                                                                                                                                                                                                                                                                                              |
| **staking**                    | `bond`, `bondextra`, `canceldeferredslash`, `chill`, `chillother`, `forcenewera`, `forceneweraalways`, `forcenoeras`, `forceunstake`, `increasevalidatorcount`, `kick`, `nominate`, `payoutstakers`, `reapstash`, `scalevalidatorcount`, `setcontroller`, `sethistorydepth`, `setinvulnerables`, `setvalidatorcount`, `unbond`, `updatestakinglimits`, `validate`, `withdrawunbonded`                                                               |
| **system**                     | `fillblock`, `killprefix`, `killstorage`, `remark`, `remarkwithevent`, `setchangestrieconfig`, `setcode`, `setcodewithoutchecks`, `setheappages`, `setstorage`                                                                                                                                                                                                                                                                                      |
| **technicalcommittee**         | `close`, `disapproveproposal`, `execute`, `propose`, `setmembers`, `vote`                                                                                                                                                                                                                                                                                                                                                                           |
| **technicalmembership**        | `addmember`, `changekey`, `clearprime`, `removemember`, `resetmembers`, `setprime`, `swapmember`                                                                                                                                                                                                                                                                                                                                                    |
| **timestamp**                  | `set`                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **tips**                       | `closetip`, `reportawesome`, `retracttip`, `slashtip`, `tip`, `tipnew`                                                                                                                                                                                                                                                                                                                                                                              |
| **treasury**                   | `approveproposal`, `proposespend`, `rejectproposal`                                                                                                                                                                                                                                                                                                                                                                                                 |
| **utility**                    | `asderivative`, `batch`, `batchall`                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **vesting**                    | `forcevestedtransfer`, `vest`, `vestother`, `vestedtransfer`                                                                                                                                                                                                                                                                                                                                                                                        |

## Example Request

```javascript
{
    "network": "polkadot",
    "type": ["transfer"],
    "limit": 1
}
```

## Example Response

```javascript
[
    {
        "id": "60a781c7-8864-4b0a-b631-797aaa89c78a",
        "hash": "0x2928c23403c68c36eb03e4f0afefc93ff657387b4e1846922a38231def412390",
        "block_hash": "0xf7fbcffe75bcf826501e3c9686e4ae0d751d01d5663994c16f5c0ef9a3499fcf",
        "height": 4432200,
        "epoch": "303",
        "chain_id": "mainnet",
        "time": "2021-03-31T19:22:00Z",
        "transaction_fee": [
            {
                "text": "0.0155000016DOT",
                "currency": "DOT",
                "numeric": 155000016,
                "exp": 10
            }
        ],
        "version": "0.0.1",
        "events": [
            {
                "id": "4432200-1",
                "kind": "Extrinsic",
                "type": [
                    "transfer"
                ],
                "module": "balances",
                "sub": [
                    {
                        "id": "4432200-1",
                        "type": [
                            "killedaccount"
                        ],
                        "module": "system",
                        "node": {
                            "versions": [
                                {
                                    "id": "13rhEambpf84PevKhSTg7dgjh8pVBp9jTDS5udV92yz7rwqR"
                                }
                            ]
                        },
                        "nonce": "0",
                        "completion": "2021-03-31T19:22:00Z",
                        "additional": {
                            "attributes": [
                                "{\"name\": \"AccountId\", \"value\": \"13rhEambpf84PevKhSTg7dgjh8pVBp9jTDS5udV92yz7rwqR\"}"
                            ]
                        }
                    },
                    {
                        "id": "4432200-2",
                        "type": [
                            "transfer"
                        ],
                        "module": "balances",
                        "sender": [
                            {
                                "account": {
                                    "id": "13rhEambpf84PevKhSTg7dgjh8pVBp9jTDS5udV92yz7rwqR"
                                },
                                "amounts": [
                                    {
                                        "text": "11.8483936984DOT",
                                        "currency": "DOT",
                                        "numeric": 118483936984,
                                        "exp": 10
                                    }
                                ]
                            }
                        ],
                        "recipient": [
                            {
                                "account": {
                                    "id": "15P3xxCWPUJHsTN7WEiUtAkskTzN4VgNvrJeFTCt4pzKNWZZ"
                                },
                                "amounts": [
                                    {
                                        "text": "11.8483936984DOT",
                                        "currency": "DOT",
                                        "numeric": 118483936984,
                                        "exp": 10
                                    }
                                ]
                            }
                        ],
                        "node": {
                            "recipient": [
                                {
                                    "id": "15P3xxCWPUJHsTN7WEiUtAkskTzN4VgNvrJeFTCt4pzKNWZZ"
                                }
                            ],
                            "sender": [
                                {
                                    "id": "13rhEambpf84PevKhSTg7dgjh8pVBp9jTDS5udV92yz7rwqR"
                                }
                            ],
                            "versions": [
                                {
                                    "id": "13rhEambpf84PevKhSTg7dgjh8pVBp9jTDS5udV92yz7rwqR"
                                },
                                {
                                    "id": "15P3xxCWPUJHsTN7WEiUtAkskTzN4VgNvrJeFTCt4pzKNWZZ"
                                }
                            ]
                        },
                        "nonce": "0",
                        "completion": "2021-03-31T19:22:00Z",
                        "amount": {
                            "0": {
                                "text": "11.8483936984DOT",
                                "currency": "DOT",
                                "numeric": 118483936984,
                                "exp": 10
                            }
                        },
                        "transfers": {
                            "15P3xxCWPUJHsTN7WEiUtAkskTzN4VgNvrJeFTCt4pzKNWZZ": [
                                {
                                    "account": {
                                        "id": "15P3xxCWPUJHsTN7WEiUtAkskTzN4VgNvrJeFTCt4pzKNWZZ"
                                    },
                                    "amounts": [
                                        {
                                            "text": "11.8483936984DOT",
                                            "currency": "DOT",
                                            "numeric": 118483936984,
                                            "exp": 10
                                        }
                                    ]
                                }
                            ]
                        },
                        "additional": {
                            "attributes": [
                                "{\"name\": \"AccountId\", \"value\": \"13rhEambpf84PevKhSTg7dgjh8pVBp9jTDS5udV92yz7rwqR\"}",
                                "{\"name\": \"AccountId\", \"value\": \"15P3xxCWPUJHsTN7WEiUtAkskTzN4VgNvrJeFTCt4pzKNWZZ\"}",
                                "{\"name\": \"Balance\", \"value\": 118483936984}"
                            ]
                        }
                    },
                    {
                        "id": "4432200-3",
                        "type": [
                            "deposit"
                        ],
                        "module": "balances",
                        "recipient": [
                            {
                                "account": {
                                    "id": "16ZzMovSVVLU5oP2o5PwNG2ybbdT2diiKPAsz6J37myEGsDw"
                                },
                                "amounts": [
                                    {
                                        "text": "0.0155000016DOT",
                                        "currency": "DOT",
                                        "numeric": 155000016,
                                        "exp": 10
                                    }
                                ]
                            }
                        ],
                        "node": {
                            "recipient": [
                                {
                                    "id": "16ZzMovSVVLU5oP2o5PwNG2ybbdT2diiKPAsz6J37myEGsDw"
                                }
                            ],
                            "versions": [
                                {
                                    "id": "16ZzMovSVVLU5oP2o5PwNG2ybbdT2diiKPAsz6J37myEGsDw"
                                }
                            ]
                        },
                        "nonce": "0",
                        "completion": "2021-03-31T19:22:00Z",
                        "amount": {
                            "0": {
                                "text": "0.0155000016DOT",
                                "currency": "DOT",
                                "numeric": 155000016,
                                "exp": 10
                            }
                        },
                        "transfers": {
                            "16ZzMovSVVLU5oP2o5PwNG2ybbdT2diiKPAsz6J37myEGsDw": [
                                {
                                    "account": {
                                        "id": "16ZzMovSVVLU5oP2o5PwNG2ybbdT2diiKPAsz6J37myEGsDw"
                                    },
                                    "amounts": [
                                        {
                                            "text": "0.0155000016DOT",
                                            "currency": "DOT",
                                            "numeric": 155000016,
                                            "exp": 10
                                        }
                                    ]
                                }
                            ]
                        },
                        "additional": {
                            "attributes": [
                                "{\"name\": \"AccountId\", \"value\": \"16ZzMovSVVLU5oP2o5PwNG2ybbdT2diiKPAsz6J37myEGsDw\"}",
                                "{\"name\": \"Balance\", \"value\": 155000016}"
                            ]
                        }
                    },
                    {
                        "id": "4432200-4",
                        "type": [
                            "extrinsicsuccess"
                        ],
                        "module": "system",
                        "nonce": "0",
                        "completion": "2021-03-31T19:22:00Z",
                        "additional": {
                            "attributes": [
                                "{\"name\": \"DispatchInfo\", \"value\": {\"weight\":202714000,\"class\":\"Normal\",\"paysFee\":\"Yes\"}}"
                            ]
                        }
                    }
                ]
            }
        ],
        "has_errors": false
    }
]
```

If you need help with this API or simply want to share with other builders, you can [**join our community today**](https://discord.gg/fszyM7K)!
