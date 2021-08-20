---
description: Learn how to query the Mina GraphQL API using DataHub
---

# Query Mina GraphQL API

You don't need any tooling or clients to communicate with Mina GraphQL API. Simply head over to DataHub service page and grab your API token, then open up GraphQL UI:

[https://mina-mainnet--graphql.datahub.figment.io/apikey/REPLACE\_YOUR\_API\_KEY/graphql](https://mina-mainnet--graphql.datahub.figment.io/apikey/REPLACE_YOUR_API_KEY/graphql)

Make sure to replace the API key in the link!

### Network status

We can check out the node/network status by running the following query:

```graphql
query status {
  daemonStatus {
    syncStatus
    stateHash
    numAccounts
    chainId
    commitId
    catchupStatus
    blockchainLength
  }
}
```

You'll get an output like:

```graphql
{
  "data": {
    "daemonStatus": {
      "syncStatus": "SYNCED",
      "stateHash": "3NKQhPYhJgxvzjrnGYfcYx4azdashoU4HKa5kSRoqVEh8i36o9mm",
      "numAccounts": 1954,
      "chainId": "5f704cc0c82e0ed70e873f0893d7e06f148524e3f0bdae2afb02e7819a0c24d1",
      "commitId": "a8893ab6dd8a68171e7b99a5dc6b76940411350b",
      "catchupStatus": [
        "to_build_breadcrumb",
        "to_initial_validate",
        "finished",
        "to_verify",
        "to_download",
        "wait_for_parent"
      ],
      "blockchainLength": 4778
    }
  }
}
```

### Latest Blocks

Pull information about latest 10 blocks:

```graphql
query blocks {
  bestChain(maxLength: 10) {
    stateHash
    protocolState {
      consensusState {
        blockHeight
      }
    }
  }
}
```

Example output:

```graphql
{
  "data": {
    "bestChain": [
      {
        "stateHash": "3NKVcbeedJ6tHUb9GAD7hucwK8vfupnTfa9KNpZPWAdjy18aV8AS",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4770"
          }
        }
      },
      {
        "stateHash": "3NLjoNzTnTWSB1G4E2Twf9tVhqPicn3K3UsQ8NJmUmFKvpVsU7fe",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4771"
          }
        }
      },
      {
        "stateHash": "3NLRbB6KPZrQmvhe4GHobWscid7CEH5B5xv33rn4gJNkjasprPRm",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4772"
          }
        }
      },
      {
        "stateHash": "3NK9drYacgJJKZLuyBkd5wFuBNmqAmTWRs6sNfuB8KfMsJqQAQtW",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4773"
          }
        }
      },
      {
        "stateHash": "3NKSRCsANY2hi9d1mNm15CSGfP6gFwWezzQ4eKrrChaKc3qMv4hf",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4774"
          }
        }
      },
      {
        "stateHash": "3NLVTRP2YpyiFZ1rE7vuD84myiEBwQHxDLrppW48VWGdz9maH9mb",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4775"
          }
        }
      },
      {
        "stateHash": "3NK8z2vszqRFdnVCoefnZN1b8RQfmyAR5aAN8pqBM7Y7gqQSGbUb",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4776"
          }
        }
      },
      {
        "stateHash": "3NL5bpevCpb9UihrXDV1x3urMnWVyUrsEYqoJJtRZogXd5oUQrZU",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4777"
          }
        }
      },
      {
        "stateHash": "3NKQhPYhJgxvzjrnGYfcYx4azdashoU4HKa5kSRoqVEh8i36o9mm",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4778"
          }
        }
      },
      {
        "stateHash": "3NKfgwKwq3qWFFMNcr6BcAzv1BkZip3m6ADtr9htfjD6WftD3TrS",
        "protocolState": {
          "consensusState": {
            "blockHeight": "4779"
          }
        }
      }
    ]
  }
}
```

### Current Block

We can obtain the latest canonical block and it's information with:

```graphql
query block {
  bestChain(maxLength: 1) {
    creator
    stateHash
    stateHashField
    protocolState {
      blockchainState {
        date
        snarkedLedgerHash
      }
      previousStateHash
      consensusState {
        blockHeight
        blockchainLength
        epoch
        slot
        totalCurrency
      }
    }
    transactions {
      userCommands {
        amount
        fee
        from
        hash
      }
      coinbase
    }
  }
}
```

Example output:

```graphql
{
  "data": {
    "bestChain": [
      {
        "creator": "B62qjCuPisQjLW7YkB22BR9KieSmUZTyApftqxsAuB3U21r3vj1YnaG",
        "stateHash": "3NKfgwKwq3qWFFMNcr6BcAzv1BkZip3m6ADtr9htfjD6WftD3TrS",
        "stateHashField": "21538604359563529269247680765381984336006730725137316435164719777253393337427",
        "protocolState": {
          "blockchainState": {
            "date": "1617151320000",
            "snarkedLedgerHash": "jx1obrfdK5zczX6bKZ8YkezJRq1PENhCA6SYbTRCdvpgsaJbSEN"
          },
          "previousStateHash": "3NKQhPYhJgxvzjrnGYfcYx4azdashoU4HKa5kSRoqVEh8i36o9mm",
          "consensusState": {
            "blockHeight": "4779",
            "blockchainLength": "4779",
            "epoch": "0",
            "slot": "6734",
            "totalCurrency": "808566652840039233"
          }
        },
        "transactions": {
          "userCommands": [
            {
              "amount": "1000",
              "fee": "10000000",
              "from": "B62qix9vooX5NqJYo8nT6xWqCeQu5AJoS1ng6FRnUpVAra6PAZZ1CU4",
              "hash": "CkpYREaq17zXtxxnLJBdnfVQ2BqjMTp3aE7CgxLk2yGwWi1WkjM7w"
            },
            {
              "amount": "1000",
              "fee": "10000000",
              "from": "B62qix9vooX5NqJYo8nT6xWqCeQu5AJoS1ng6FRnUpVAra6PAZZ1CU4",
              "hash": "CkpZKJXFdeTk6UN8EaML5CAo9KPkYWcgvtn8CGHkiYix94vqn8t8D"
            },
            {
              "amount": "1000",
              "fee": "10000000",
              "from": "B62qix9vooX5NqJYo8nT6xWqCeQu5AJoS1ng6FRnUpVAra6PAZZ1CU4",
              "hash": "CkpaLPq63CJsjtPxqfdAZFR8E9DadJ2e57GjoEpt6aq3CSLot9MP7"
            },
            {
              "amount": "1000",
              "fee": "10000000",
              "from": "B62qre3erTHfzQckNuibViWQGyyKwZseztqrjPZBv6SQF384Rg6ESAy",
              "hash": "Ckpa8USvMbVNANow4NGeoSfeFKfGhb1TjJNYTAFCh9dYLyKwFJoRg"
            },
            {
              "amount": "1000",
              "fee": "10000000",
              "from": "B62qre3erTHfzQckNuibViWQGyyKwZseztqrjPZBv6SQF384Rg6ESAy",
              "hash": "CkpZGkGQcYC4X2a7VGT2oRZGph3KSoajxnUkRz6hiHJ8MHDfY23Am"
            },
            {
              "amount": "1000",
              "fee": "10000000",
              "from": "B62qre3erTHfzQckNuibViWQGyyKwZseztqrjPZBv6SQF384Rg6ESAy",
              "hash": "CkpYRm7RcwgR5ivEFLWaa1vJnzdUuh9VRmrTiG83wSsLS6EarjJ8z"
            }
          ],
          "coinbase": "720000000000"
        }
      }
    ]
  }
}
```

## Snark Pool

See a list of pending snark jobs with:

```graphql
query snarkPool {
  snarkPool {
    fee
    prover
    workIds
  }
}
```

Example output:

```graphql
{
  "data": {
    "snarkPool": [
      {
        "fee": "0",
        "prover": "B62qpLeuZDL7PxNsCqsJwWFPAmnixi5ay8Kz9NcNGBQU8jK19VpJQaY",
        "workIds": [
          343409785,
          151173040
        ]
      }
    ]
  }
}
```

### Account Details

We can get account balance with:

```graphql
query accDetails {
  account(publicKey: "B62qix9vooX5NqJYo8nT6xWqCeQu5AJoS1ng6FRnUpVAra6PAZZ1CU4") {
    delegate
    balance {
      blockHeight
      liquid
      locked
      stateHash
      total
      unknown
    }
    delegators {
      publicKey
    }
    publicKey
    stakingActive
    votingFor
    isDisabled
  }
}
```

Example output:

```graphql
{
  "data": {
    "account": {
      "delegate": "B62qix9vooX5NqJYo8nT6xWqCeQu5AJoS1ng6FRnUpVAra6PAZZ1CU4",
      "balance": {
        "blockHeight": "4779",
        "liquid": "787133086000",
        "locked": "0",
        "stateHash": "3NKfgwKwq3qWFFMNcr6BcAzv1BkZip3m6ADtr9htfjD6WftD3TrS",
        "total": "787133086000",
        "unknown": "787133086000"
      },
      "delegators": [],
      "publicKey": "B62qix9vooX5NqJYo8nT6xWqCeQu5AJoS1ng6FRnUpVAra6PAZZ1CU4",
      "stakingActive": false,
      "votingFor": "3NK2tkzqqK5spR2sZ7tujjqPksL45M3UUrcA4WhCkeiPtnugyE2x",
      "isDisabled": false
    }
  }
}
```

