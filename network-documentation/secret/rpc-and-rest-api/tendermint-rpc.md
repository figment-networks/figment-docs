---
description: Learn how to interact with the Tendermint RPC
---

# Tendermint RPC

## Source documentation

[**The Tendermint RPC's source documentation can be found here**](https://docs.tendermint.com/master/rpc/#/).

Tendermint supports the following RPC protocols:

* URI over HTTP
* JSONRPC over HTTP
* JSONRPC over websockets

## Configuration

RPC can be configured by tuning parameters under `[rpc]` table in the `$TMHOME/config/config.toml` file or by using the `--rpc.X` command-line flags.

Default rpc listen address is `tcp://0.0.0.0:26657`. To set another address, set the `laddr` config parameter to desired value. CORS \(Cross-Origin Resource Sharing\) can be enabled by setting `cors_allowed_origins`, `cors_allowed_methods`, `cors_allowed_headers` config parameters.

### Arguments

Arguments which expect strings or byte arrays may be passed as quoted strings, like `"abc"` or as `0x`-prefixed strings, like `0x616263`.

### URI/HTTP

A REST-like interface.

```javascript
curl localhost:26657/block?height=5
```

### JSONRPC/HTTP

JSONRPC requests can be POST'd to the root RPC endpoint via HTTP.

```javascript
curl --header "Content-Type: application/json" --request POST --data '{"method": "block", "params": ["5"], "id": 1}' localhost:26657
```

### JSONRPC/websockets

JSONRPC requests can be also made via websocket. The websocket endpoint is at `/websocket`, e.g. `localhost:26657/websocket`. Asynchronous RPC functions like event `subscribe` and `unsubscribe` are only available via websockets.

Example using [https://github.com/hashrocket/ws](https://github.com/hashrocket/ws):

```javascript
ws ws://localhost:26657/websocket
> { "jsonrpc": "2.0", "method": "subscribe", "params": ["tm.event='NewBlock'"], "id": 1 }
```

## **Websocket**

**Subscribe/unsubscribe are reserved for websocket events.**

### `GET​/subscribe`

**Description**

Subscribe for events via Websocket

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>query</b>
      </td>
      <td style="text-align:left">string * required</td>
      <td style="text-align:left">
        <p>Query is a string, which has a form: &quot;condition AND condition ...&quot;
          (no OR at the moment). condition has a form: &quot;key operation operand&quot;.
          key is a string with a restricted set of possible symbols ( \t\n\r()&quot;&apos;=&gt;&lt;
          are not allowed). operation can be &quot;=&quot;, &quot;&lt;&quot;, &quot;&lt;=&quot;,
          &quot;&gt;&quot;, &quot;&gt;=&quot;, &quot;CONTAINS&quot;. operand can
          be a string (escaped with single quotes), number, date or time.</p>
        <p>tm.event = &apos;Tx&apos; AND tx.height = 5</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {}
}
```

### `GET​/unsubscribe`

**Description**

Unsubscribe from event on Websocket

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>query</b>
      </td>
      <td style="text-align:left">string * required</td>
      <td style="text-align:left">
        <p>Query is a string, which has a form: &quot;condition AND condition ...&quot;
          (no OR at the moment). condition has a form: &quot;key operation operand&quot;.
          key is a string with a restricted set of possible symbols ( \t\n\r()&quot;&apos;=&gt;&lt;
          are not allowed). operation can be &quot;=&quot;, &quot;&lt;&quot;, &quot;&lt;=&quot;,
          &quot;&gt;&quot;, &quot;&gt;=&quot;, &quot;CONTAINS&quot;. operand can
          be a string (escaped with single quotes), number, date or time.</p>
        <p>tm.event = &apos;Tx&apos; AND tx.height = 5</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {}
}
```

### `GET​/unsubscribe_all`

**Description**

Unsubscribe from all events via Websocket

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {}
}
```

## **Info**

**Information about the node APIs**

### `GET​/health`

**Description**

Node heartbeat

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {}
}
```

### `GET​/status`

**Description**

Node Status

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "node_info": {
      "protocol_version": {
        "p2p": "7",
        "block": "10",
        "app": "0"
      },
      "id": "5576458aef205977e18fd50b274e9b5d9014525a",
      "listen_addr": "tcp:0.0.0.0:26656",
      "network": "cosmoshub-2",
      "version": "0.32.1",
      "channels": "4020212223303800",
      "moniker": "moniker-node",
      "other": {
        "tx_index": "on",
        "rpc_address": "tcp:0.0.0.0:26657"
      }
    },
    "sync_info": {
      "latest_block_hash": "790BA84C3545FCCC49A5C629CEE6EA58A6E875C3862175BDC11EE7AF54703501",
      "latest_app_hash": "C9AEBB441B787D9F1D846DE51F3826F4FD386108B59B08239653ABF59455C3F8",
      "latest_block_height": "1262196",
      "latest_block_time": "2019-08-01T11:52:22.818762194Z",
      "earliest_block_hash": "790BA84C3545FCCC49A5C629CEE6EA58A6E875C3862175BDC11EE7AF54703501",
      "earliest_app_hash": "C9AEBB441B787D9F1D846DE51F3826F4FD386108B59B08239653ABF59455C3F8",
      "earliest_block_height": "1262196",
      "earliest_block_time": "2019-08-01T11:52:22.818762194Z",
      "catching_up": false
    },
    "validator_info": {
      "address": "5D6A51A8E9899C44079C6AF90618BA0369070E6E",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "A6DoBUypNtUAyEHWtQ9bFjfNg8Bo9CrnkUGl6k6OHN4="
      },
      "voting_power": "0"
    }
  }
}
```

### `GET​/net_info`

**Description**

Network information

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "listening": true,
    "listeners": [
      "Listener(@)"
    ],
    "n_peers": "1",
    "peers": [
      {
        "node_info": {
          "protocol_version": {
            "p2p": "7",
            "block": "10",
            "app": "0"
          },
          "id": "5576458aef205977e18fd50b274e9b5d9014525a",
          "listen_addr": "tcp:0.0.0.0:26656",
          "network": "cosmoshub-2",
          "version": "0.32.1",
          "channels": "4020212223303800",
          "moniker": "moniker-node",
          "other": {
            "tx_index": "on",
            "rpc_address": "tcp:0.0.0.0:26657"
          }
        },
        "is_outbound": true,
        "connection_status": {
          "Duration": "168901057956119",
          "SendMonitor": {
            "Active": true,
            "Start": "2019-07-31T14:31:28.66Z",
            "Duration": "168901060000000",
            "Idle": "168901040000000",
            "Bytes": "5",
            "Samples": "1",
            "InstRate": "0",
            "CurRate": "0",
            "AvgRate": "0",
            "PeakRate": "0",
            "BytesRem": "0",
            "TimeRem": "0",
            "Progress": 0
          },
          "RecvMonitor": {
            "Active": true,
            "Start": "2019-07-31T14:31:28.66Z",
            "Duration": "168901060000000",
            "Idle": "168901040000000",
            "Bytes": "5",
            "Samples": "1",
            "InstRate": "0",
            "CurRate": "0",
            "AvgRate": "0",
            "PeakRate": "0",
            "BytesRem": "0",
            "TimeRem": "0",
            "Progress": 0
          },
          "Channels": [
            {
              "ID": 48,
              "SendQueueCapacity": "1",
              "SendQueueSize": "0",
              "Priority": "5",
              "RecentlySent": "0"
            }
          ]
        },
        "remote_ip": "95.179.155.35"
      }
    ]
  }
}
```

### `GET​/blockchain`

**Description**

Get block headers \(max:20\) for minHeight &lt;= height &lt;= maxHeight

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **minHeight** | integer | Minimum block height to return |
| maxHeight | integer | Maximum block height to return |

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "last_height": "1276718",
    "block_metas": [
      {
        "block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "block_size": 1000000,
        "header": {
          "version": {
            "block": "10",
            "app": "0"
          },
          "chain_id": "cosmoshub-2",
          "height": "12",
          "time": "2019-04-22T17:01:51.701356223Z",
          "last_block_id": {
            "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
            "parts": {
              "total": 1,
              "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
            }
          },
          "last_commit_hash": "21B9BC845AD2CB2C4193CDD17BFC506F1EBE5A7402E84AD96E64171287A34812",
          "data_hash": "970886F99E77ED0D60DA8FCE0447C2676E59F2F77302B0C4AA10E1D02F18EF73",
          "validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
          "next_validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
          "consensus_hash": "0F2908883A105C793B74495EB7D6DF2EEA479ED7FC9349206A65CB0F9987A0B8",
          "app_hash": "223BF64D4A01074DC523A80E76B9BBC786C791FB0A1893AC5B14866356FCFD6C",
          "last_results_hash": "",
          "evidence_hash": "",
          "proposer_address": "D540AB022088612AC74B287D076DBFBC4A377A2E"
        },
        "num_txs": "54"
      }
    ]
  }
}
```

### `GET​/block`

**Description**

Get block at a specified height

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>height</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Height to return. If no height is provided, it will fetch the latest block.</p>
        <p>Default value = 0</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "block_id": {
      "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
      "parts": {
        "total": 1,
        "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
      }
    },
    "block": {
      "header": {
        "version": {
          "block": "10",
          "app": "0"
        },
        "chain_id": "cosmoshub-2",
        "height": "12",
        "time": "2019-04-22T17:01:51.701356223Z",
        "last_block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "last_commit_hash": "21B9BC845AD2CB2C4193CDD17BFC506F1EBE5A7402E84AD96E64171287A34812",
        "data_hash": "970886F99E77ED0D60DA8FCE0447C2676E59F2F77302B0C4AA10E1D02F18EF73",
        "validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
        "next_validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
        "consensus_hash": "0F2908883A105C793B74495EB7D6DF2EEA479ED7FC9349206A65CB0F9987A0B8",
        "app_hash": "223BF64D4A01074DC523A80E76B9BBC786C791FB0A1893AC5B14866356FCFD6C",
        "last_results_hash": "",
        "evidence_hash": "",
        "proposer_address": "D540AB022088612AC74B287D076DBFBC4A377A2E"
      },
      "data": [
        "yQHwYl3uCkKoo2GaChRnd+THLQ2RM87nEZrE19910Z28ABIUWW/t8AtIMwcyU0sT32RcMDI9GF0aEAoFdWF0b20SBzEwMDAwMDASEwoNCgV1YXRvbRIEMzEwMRCd8gEaagom61rphyEDoJPxlcjRoNDtZ9xMdvs+lRzFaHe2dl2P5R2yVCWrsHISQKkqX5H1zXAIJuC57yw0Yb03Fwy75VRip0ZBtLiYsUqkOsPUoQZAhDNP+6LY+RUwz/nVzedkF0S29NZ32QXdGv0="
      ],
      "evidence": [
        {
          "type": "string",
          "height": 0,
          "time": 0,
          "total_voting_power": 0,
          "validator": {
            "pub_key": {
              "type": "tendermint/PubKeyEd25519",
              "value": "A6DoBUypNtUAyEHWtQ9bFjfNg8Bo9CrnkUGl6k6OHN4="
            },
            "voting_power": 0,
            "address": "string"
          }
        }
      ],
      "last_commit": {
        "height": 0,
        "round": 0,
        "block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "signatures": [
          {
            "type": 2,
            "height": "1262085",
            "round": 0,
            "block_id": {
              "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
              "parts": {
                "total": 1,
                "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
              }
            },
            "timestamp": "2019-08-01T11:39:38.867269833Z",
            "validator_address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "validator_index": 0,
            "signature": "DBchvucTzAUEJnGYpNvMdqLhBAHG4Px8BsOBB3J3mAFCLGeuG7uJqy+nVngKzZdPhPi8RhmE/xcw/M9DOJjEDg=="
          }
        ]
      }
    }
  }
}
```

### `GET​/block_by_hash`

**Description**

Get block by hash

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **hash** | string \* required | Block hash |

**Example JSON Output**

```javascript
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "block_id": {
      "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
      "parts": {
        "total": 1,
        "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
      }
    },
    "block": {
      "header": {
        "version": {
          "block": "10",
          "app": "0"
        },
        "chain_id": "cosmoshub-2",
        "height": "12",
        "time": "2019-04-22T17:01:51.701356223Z",
        "last_block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "last_commit_hash": "21B9BC845AD2CB2C4193CDD17BFC506F1EBE5A7402E84AD96E64171287A34812",
        "data_hash": "970886F99E77ED0D60DA8FCE0447C2676E59F2F77302B0C4AA10E1D02F18EF73",
        "validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
        "next_validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
        "consensus_hash": "0F2908883A105C793B74495EB7D6DF2EEA479ED7FC9349206A65CB0F9987A0B8",
        "app_hash": "223BF64D4A01074DC523A80E76B9BBC786C791FB0A1893AC5B14866356FCFD6C",
        "last_results_hash": "",
        "evidence_hash": "",
        "proposer_address": "D540AB022088612AC74B287D076DBFBC4A377A2E"
      },
      "data": [
        "yQHwYl3uCkKoo2GaChRnd+THLQ2RM87nEZrE19910Z28ABIUWW/t8AtIMwcyU0sT32RcMDI9GF0aEAoFdWF0b20SBzEwMDAwMDASEwoNCgV1YXRvbRIEMzEwMRCd8gEaagom61rphyEDoJPxlcjRoNDtZ9xMdvs+lRzFaHe2dl2P5R2yVCWrsHISQKkqX5H1zXAIJuC57yw0Yb03Fwy75VRip0ZBtLiYsUqkOsPUoQZAhDNP+6LY+RUwz/nVzedkF0S29NZ32QXdGv0="
      ],
      "evidence": [
        {
          "type": "string",
          "height": 0,
          "time": 0,
          "total_voting_power": 0,
          "validator": {
            "pub_key": {
              "type": "tendermint/PubKeyEd25519",
              "value": "A6DoBUypNtUAyEHWtQ9bFjfNg8Bo9CrnkUGl6k6OHN4="
            },
            "voting_power": 0,
            "address": "string"
          }
        }
      ],
      "last_commit": {
        "height": 0,
        "round": 0,
        "block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "signatures": [
          {
            "type": 2,
            "height": "1262085",
            "round": 0,
            "block_id": {
              "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
              "parts": {
                "total": 1,
                "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
              }
            },
            "timestamp": "2019-08-01T11:39:38.867269833Z",
            "validator_address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "validator_index": 0,
            "signature": "DBchvucTzAUEJnGYpNvMdqLhBAHG4Px8BsOBB3J3mAFCLGeuG7uJqy+nVngKzZdPhPi8RhmE/xcw/M9DOJjEDg=="
          }
        ]
      }
    }
  }
}
```

### `GET​/block_results`

**Description**

Get block results at a specified height

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>height</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Height to return. If no height is provided, it will fetch information
          regarding the latest block.</p>
        <p>Default value : 0</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "height": "12",
    "txs_results": [
      {
        "code": "0",
        "data": "",
        "log": "not enough gas",
        "info": "",
        "gas_wanted": "100",
        "gas_used": "100",
        "events": [
          {
            "type": "app",
            "attributes": [
              {
                "key": "YWN0aW9u",
                "value": "c2VuZA==",
                "index": false
              }
            ]
          }
        ],
        "codespace": "ibc"
      }
    ],
    "begin_block_events": [
      {
        "type": "app",
        "attributes": [
          {
            "key": "YWN0aW9u",
            "value": "c2VuZA==",
            "index": false
          }
        ]
      }
    ],
    "end_block": [
      {
        "type": "app",
        "attributes": [
          {
            "key": "YWN0aW9u",
            "value": "c2VuZA==",
            "index": false
          }
        ]
      }
    ],
    "validator_updates": [
      {
        "pub_key": {
          "type": "tendermint/PubKeyEd25519",
          "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
        },
        "power": "300"
      }
    ],
    "consensus_params_updates": {
      "block": {
        "max_bytes": "22020096",
        "max_gas": "1000",
        "time_iota_ms": "1000"
      },
      "evidence": {
        "max_age": "100000"
      },
      "validator": {
        "pub_key_types": [
          "ed25519"
        ]
      }
    }
  }
}
```

### `GET​/commit`

### **Get commit results at a specified height**

**Description**

Get commit results at a specified height

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>height</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Height to return. If no height is provided, it will fetch validator set
          which corresponds to the latest block.</p>
        <p>Default value : 0</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "signed_header": {
      "header": {
        "version": {
          "block": "10",
          "app": "0"
        },
        "chain_id": "cosmoshub-2",
        "height": "12",
        "time": "2019-04-22T17:01:51.701356223Z",
        "last_block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "last_commit_hash": "21B9BC845AD2CB2C4193CDD17BFC506F1EBE5A7402E84AD96E64171287A34812",
        "data_hash": "970886F99E77ED0D60DA8FCE0447C2676E59F2F77302B0C4AA10E1D02F18EF73",
        "validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
        "next_validators_hash": "D658BFD100CA8025CFD3BECFE86194322731D387286FBD26E059115FD5F2BCA0",
        "consensus_hash": "0F2908883A105C793B74495EB7D6DF2EEA479ED7FC9349206A65CB0F9987A0B8",
        "app_hash": "223BF64D4A01074DC523A80E76B9BBC786C791FB0A1893AC5B14866356FCFD6C",
        "last_results_hash": "",
        "evidence_hash": "",
        "proposer_address": "D540AB022088612AC74B287D076DBFBC4A377A2E"
      },
      "commit": {
        "height": "1311801",
        "round": 0,
        "block_id": {
          "hash": "112BC173FD838FB68EB43476816CD7B4C6661B6884A9E357B417EE957E1CF8F7",
          "parts": {
            "total": 1,
            "hash": "38D4B26B5B725C4F13571EFE022C030390E4C33C8CF6F88EDD142EA769642DBD"
          }
        },
        "signatures": [
          {
            "block_id_flag": 2,
            "validator_address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "timestamp": "2019-04-22T17:01:58.376629719Z",
            "signature": "14jaTQXYRt8kbLKEhdHq7AXycrFImiLuZx50uOjs2+Zv+2i7RTG/jnObD07Jo2ubZ8xd7bNBJMqkgtkd0oQHAw=="
          }
        ]
      }
    },
    "canonical": true
  }
}
```

### `GET​/validators`

**Description**

Get a validator set at a specified height

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>height</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Height to return. If no height is provided, it will fetch validator set
          which corresponds to the latest block</p>
        <p>Default value : 0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>page</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Page number (1-based)</p>
        <p>Default value: 1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>per_page</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Number of entries per page (max: 100)</p>
        <p>Default value : 30</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "block_height": "55",
    "validators": [
      {
        "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
        "pub_key": {
          "type": "tendermint/PubKeyEd25519",
          "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
        },
        "voting_power": "239727",
        "proposer_priority": "-11896414"
      }
    ],
    "count": "1",
    "total": "25"
  }
}
```

### `GET​/genesis`

**Description**

Get Genesis

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "genesis": {
      "genesis_time": "2019-04-22T17:00:00Z",
      "chain_id": "cosmoshub-2",
      "initial_height": "2",
      "consensus_params": {
        "block": {
          "max_bytes": "22020096",
          "max_gas": "1000",
          "time_iota_ms": "1000"
        },
        "evidence": {
          "max_age": "100000"
        },
        "validator": {
          "pub_key_types": [
            "ed25519"
          ]
        }
      },
      "validators": [
        {
          "address": "B00A6323737F321EB0B8D59C6FD497A14B60938A",
          "pub_key": {
            "type": "tendermint/PubKeyEd25519",
            "value": "cOQZvh/h9ZioSeUMZB/1Vy1Xo5x2sjrVjlE/qHnYifM="
          },
          "power": "9328525",
          "name": "Certus One"
        }
      ],
      "app_hash": "",
      "app_state": {}
    }
  }
}
```

### `GET​/dump_consensus_state`

**Description**

Get consensus state

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "round_state": {
      "height": "1311801",
      "round": 0,
      "step": 3,
      "start_time": "2019-08-05T11:28:49.064658805Z",
      "commit_time": "2019-08-05T11:28:44.064658805Z",
      "validators": {
        "validators": [
          {
            "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "pub_key": {
              "type": "tendermint/PubKeyEd25519",
              "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
            },
            "voting_power": "239727",
            "proposer_priority": "-11896414"
          }
        ],
        "proposer": {
          "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
          "pub_key": {
            "type": "tendermint/PubKeyEd25519",
            "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
          },
          "voting_power": "239727",
          "proposer_priority": "-11896414"
        }
      },
      "locked_round": -1,
      "valid_round": "-1",
      "votes": [
        {
          "round": "0",
          "prevotes": [
            "nil-Vote",
            "Vote{19:46A3F8B8393B 1311801/00/1(Prevote) 000000000000 64CE682305CB @ 2019-08-05T11:28:47.374703444Z}"
          ],
          "prevotes_bit_array": "BA{100:___________________x________________________________________________________________________________} 209706/170220253 = 0.00",
          "precommits": [
            "nil-Vote"
          ],
          "precommits_bit_array": "BA{100:____________________________________________________________________________________________________} 0/170220253 = 0.00"
        }
      ],
      "commit_round": -1,
      "last_commit": {
        "votes": [
          "Vote{0:000001E443FD 1311800/00/2(Precommit) 3071ADB27D1A 77EE1B6B6847 @ 2019-08-05T11:28:43.810128139Z}"
        ],
        "votes_bit_array": "BA{100:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx} 170220253/170220253 = 1.00",
        "peer_maj_23s": {}
      },
      "last_validators": {
        "validators": [
          {
            "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "pub_key": {
              "type": "tendermint/PubKeyEd25519",
              "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
            },
            "voting_power": "239727",
            "proposer_priority": "-11896414"
          }
        ],
        "proposer": {
          "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
          "pub_key": {
            "type": "tendermint/PubKeyEd25519",
            "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
          },
          "voting_power": "239727",
          "proposer_priority": "-11896414"
        }
      },
      "triggered_timeout_precommit": false
    },
    "peers": [
      {
        "node_address": "357f6a6c1d27414579a8185060aa8adf9815c43c@68.183.41.207:26656",
        "peer_state": {
          "round_state": {
            "height": "1311801",
            "round": "0",
            "step": 3,
            "start_time": "2019-08-05T11:28:49.21730864Z",
            "proposal": false,
            "proposal_block_parts_header": {
              "total": 0,
              "hash": ""
            },
            "proposal_pol_round": -1,
            "proposal_pol": "____________________________________________________________________________________________________",
            "prevotes": "___________________x________________________________________________________________________________",
            "precommits": "____________________________________________________________________________________________________",
            "last_commit_round": 0,
            "last_commit": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "catchup_commit_round": -1,
            "catchup_commit": "____________________________________________________________________________________________________"
          },
          "stats": {
            "votes": "1159558",
            "block_parts": "4786"
          }
        }
      }
    ]
  }
}
```

### `GET​/consensus_state`

**Description**

Get consensus state

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "round_state": {
      "height": "1311801",
      "round": 0,
      "step": 3,
      "start_time": "2019-08-05T11:28:49.064658805Z",
      "commit_time": "2019-08-05T11:28:44.064658805Z",
      "validators": {
        "validators": [
          {
            "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "pub_key": {
              "type": "tendermint/PubKeyEd25519",
              "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
            },
            "voting_power": "239727",
            "proposer_priority": "-11896414"
          }
        ],
        "proposer": {
          "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
          "pub_key": {
            "type": "tendermint/PubKeyEd25519",
            "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
          },
          "voting_power": "239727",
          "proposer_priority": "-11896414"
        }
      },
      "locked_round": -1,
      "valid_round": "-1",
      "votes": [
        {
          "round": "0",
          "prevotes": [
            "nil-Vote",
            "Vote{19:46A3F8B8393B 1311801/00/1(Prevote) 000000000000 64CE682305CB @ 2019-08-05T11:28:47.374703444Z}"
          ],
          "prevotes_bit_array": "BA{100:___________________x________________________________________________________________________________} 209706/170220253 = 0.00",
          "precommits": [
            "nil-Vote"
          ],
          "precommits_bit_array": "BA{100:____________________________________________________________________________________________________} 0/170220253 = 0.00"
        }
      ],
      "commit_round": -1,
      "last_commit": {
        "votes": [
          "Vote{0:000001E443FD 1311800/00/2(Precommit) 3071ADB27D1A 77EE1B6B6847 @ 2019-08-05T11:28:43.810128139Z}"
        ],
        "votes_bit_array": "BA{100:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx} 170220253/170220253 = 1.00",
        "peer_maj_23s": {}
      },
      "last_validators": {
        "validators": [
          {
            "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
            "pub_key": {
              "type": "tendermint/PubKeyEd25519",
              "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
            },
            "voting_power": "239727",
            "proposer_priority": "-11896414"
          }
        ],
        "proposer": {
          "address": "000001E443FD237E4B616E2FA69DF4EE3D49A94F",
          "pub_key": {
            "type": "tendermint/PubKeyEd25519",
            "value": "9tK9IT+FPdf2qm+5c2qaxi10sWP+3erWTKgftn2PaQM="
          },
          "voting_power": "239727",
          "proposer_priority": "-11896414"
        }
      },
      "triggered_timeout_precommit": false
    },
    "peers": [
      {
        "node_address": "357f6a6c1d27414579a8185060aa8adf9815c43c@68.183.41.207:26656",
        "peer_state": {
          "round_state": {
            "height": "1311801",
            "round": "0",
            "step": 3,
            "start_time": "2019-08-05T11:28:49.21730864Z",
            "proposal": false,
            "proposal_block_parts_header": {
              "total": 0,
              "hash": ""
            },
            "proposal_pol_round": -1,
            "proposal_pol": "____________________________________________________________________________________________________",
            "prevotes": "___________________x________________________________________________________________________________",
            "precommits": "____________________________________________________________________________________________________",
            "last_commit_round": 0,
            "last_commit": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "catchup_commit_round": -1,
            "catchup_commit": "____________________________________________________________________________________________________"
          },
          "stats": {
            "votes": "1159558",
            "block_parts": "4786"
          }
        }
      }
    ]
  }
}
```

### `GET​/consensus_params`

**Description**

Get consensus parameters

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>height</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Height to return. If no height is provided, it will fetch commit information
          regarding the latest block.</p>
        <p>Default value : 0</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "block_height": "1",
    "consensus_params": {
      "block": {
        "max_bytes": "22020096",
        "max_gas": "1000",
        "time_iota_ms": "1000"
      },
      "evidence": {
        "max_age": "100000"
      },
      "validator": {
        "pub_key_types": [
          "ed25519"
        ]
      }
    }
  }
}
```

### `GET​/unconfirmed_txs`

**Description**

Get the list of unconfirmed transactions

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>limit</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Maximum number of unconfirmed transactions to reutrn (max 100)</p>
        <p>Default value : 30</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "n_txs": "82",
    "total": "82",
    "total_bytes": "19974",
    "txs": [
      "gAPwYl3uCjCMTXENChSMnIkb5ZpYHBKIZqecFEV2tuZr7xIUA75/FmYq9WymsOBJ0XSJ8yV8zmQKMIxNcQ0KFIyciRvlmlgcEohmp5wURXa25mvvEhQbrvwbvlNiT+Yjr86G+YQNx7kRVgowjE1xDQoUjJyJG+WaWBwSiGannBRFdrbma+8SFK2m+1oxgILuQLO55n8mWfnbIzyPCjCMTXENChSMnIkb5ZpYHBKIZqecFEV2tuZr7xIUQNGfkmhTNMis4j+dyMDIWXdIPiYKMIxNcQ0KFIyciRvlmlgcEohmp5wURXa25mvvEhS8sL0D0wwgGCItQwVowak5YB38KRIUCg4KBXVhdG9tEgUxMDA1NBDoxRgaagom61rphyECn8x7emhhKdRCB2io7aS/6Cpuq5NbVqbODmqOT3jWw6kSQKUresk+d+Gw0BhjiggTsu8+1voW+VlDCQ1GRYnMaFOHXhyFv7BCLhFWxLxHSAYT8a5XqoMayosZf9mANKdXArA="
    ]
  }
}
```

### `GET​/num_unconfirmed_txs`

**Description**

Get data about unconfirmed transactions

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "n_txs": "31",
    "total": "82",
    "total_bytes": "19974"
  }
}
```

### `GET​/tx_search`

**Description**

Search for transactions

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>query</b>
      </td>
      <td style="text-align:left">string * required</td>
      <td style="text-align:left">Query</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>prove</b>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>Include proofs of the transactions inclusion in the block</p>
        <p>Default value : false</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>page</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Page number (1-based)</p>
        <p>Default value : 1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>per_page</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Number of entries per page (max: 100)</p>
        <p>Default value : 30</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>order_by</b>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>Order in which transactions are sorted (&quot;asc&quot; or &quot;desc&quot;),
          by height &amp; index. If empty, default sorting will be still aplied</p>
        <p>Default value: asc</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "txs": [
      {
        "hash": "D70952032620CC4E2737EB8AC379806359D8E0B17B0488F627997A0B043ABDED",
        "height": "1000",
        "index": 0,
        "tx_result": {
          "log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
          "gas_wanted": "200000",
          "gas_used": "28596",
          "tags": {
            "key": "YWN0aW9u",
            "value": "c2VuZA==",
            "index": false
          }
        },
        "tx": "5wHwYl3uCkaoo2GaChQmSIu8hxpJxLcCuIi8fiHN4TMwrRIU/Af1cEG7Rcs/6LjTl7YjRSymJfYaFAoFdWF0b20SCzE0OTk5OTk1MDAwEhMKDQoFdWF0b20SBDUwMDAQwJoMGmoKJuta6YchAwswBShaB1wkZBctLIhYqBC3JrAI28XGzxP+rVEticGEEkAc+khTkKL9CDE47aDvjEHvUNt+izJfT4KVF2v2JkC+bmlH9K08q3PqHeMI9Z5up+XMusnTqlP985KF+SI5J3ZOIhhNYWRlIGJ5IENpcmNsZSB3aXRoIGxvdmU=",
        "proof": {
          "RootHash": "72FE6BF6D4109105357AECE0A82E99D0F6288854D16D8767C5E72C57F876A14D",
          "Data": "5wHwYl3uCkaoo2GaChQmSIu8hxpJxLcCuIi8fiHN4TMwrRIU/Af1cEG7Rcs/6LjTl7YjRSymJfYaFAoFdWF0b20SCzE0OTk5OTk1MDAwEhMKDQoFdWF0b20SBDUwMDAQwJoMGmoKJuta6YchAwswBShaB1wkZBctLIhYqBC3JrAI28XGzxP+rVEticGEEkAc+khTkKL9CDE47aDvjEHvUNt+izJfT4KVF2v2JkC+bmlH9K08q3PqHeMI9Z5up+XMusnTqlP985KF+SI5J3ZOIhhNYWRlIGJ5IENpcmNsZSB3aXRoIGxvdmU=",
          "Proof": {
            "total": "2",
            "index": "0",
            "leaf_hash": "eoJxKCzF3m72Xiwb/Q43vJ37/2Sx8sfNS9JKJohlsYI=",
            "aunts": [
              "eWb+HG/eMmukrQj4vNGyFYb3nKQncAWacq4HF5eFzDY="
            ]
          }
        }
      }
    ],
    "total_count": "2"
  }
}
```

### `GET​/tx`

**Description**

Get transactions by hash

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>hash</b>
      </td>
      <td style="text-align:left">string * required</td>
      <td style="text-align:left">Transaction hash to retrieve</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>prove</b>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>Include proofs of the transactions inclusion in the block</p>
        <p>Default value : false</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "hash": "D70952032620CC4E2737EB8AC379806359D8E0B17B0488F627997A0B043ABDED",
    "height": "1000",
    "index": 0,
    "tx_result": {
      "log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "gas_wanted": "200000",
      "gas_used": "28596",
      "tags": [
        {
          "key": "YWN0aW9u",
          "value": "c2VuZA==",
          "index": false
        }
      ]
    },
    "tx": "5wHwYl3uCkaoo2GaChQmSIu8hxpJxLcCuIi8fiHN4TMwrRIU/Af1cEG7Rcs/6LjTl7YjRSymJfYaFAoFdWF0b20SCzE0OTk5OTk1MDAwEhMKDQoFdWF0b20SBDUwMDAQwJoMGmoKJuta6YchAwswBShaB1wkZBctLIhYqBC3JrAI28XGzxP+rVEticGEEkAc+khTkKL9CDE47aDvjEHvUNt+izJfT4KVF2v2JkC+bmlH9K08q3PqHeMI9Z5up+XMusnTqlP985KF+SI5J3ZOIhhNYWRlIGJ5IENpcmNsZSB3aXRoIGxvdmU="
  }
}
```

### `GET​/broadcast_evidence`

**Description**

Broadcast evidence of the misbehavior

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **evidence** | string \* required | JSON evidence |

**Example JSON Output**

```javascript
{
  "error": "",
  "result": "",
  "id": 0,
  "jsonrpc": "2.0"
}
```

## **Transactions**

**Transactions broadcast APIs**

### `GET​/broadcast_tx_sync`

**Description**

Returns with the response from CheckTx. Does not wait for DeliverTx result.

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **tx** | string \* required | The transaction |

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "code": "0",
    "data": "",
    "log": "",
    "codespace": "ibc",
    "hash": "0D33F2F03A5234F38706E43004489E061AC40A2E"
  },
  "error": ""
}
```

### `GET​/broadcast_tx_async`

**Description**

Returns right away, with no response. Does not wait for CheckTx nor DeliverTx

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **tx** | string \* required | The transaction |

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "code": "0",
    "data": "",
    "log": "",
    "codespace": "ibc",
    "hash": "0D33F2F03A5234F38706E43004489E061AC40A2E"
  },
  "error": ""
}
```

### `GET​/broadcast_tx_commit`

**Description**

Returns with the responses from CheckTx and DeliverTx

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **tx** | string \* required | The transaction |

**Example JSON Output**

```javascript
{
  "error": "",
  "result": {
    "height": "26682",
    "hash": "75CA0F856A4DA078FC4911580360E70CEFB2EBEE",
    "deliver_tx": {
      "log": "",
      "data": "",
      "code": "0"
    },
    "check_tx": {
      "log": "",
      "data": "",
      "code": "0"
    }
  },
  "id": 0,
  "jsonrpc": "2.0"
}
```

### `GET​/check_tx`

**Description**

Checks the transaction without executing it

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **tx** | string \* required | The transaction |

**Example JSON Output**

```javascript
{
  "error": "",
  "result": {
    "code": "0",
    "data": "",
    "log": "",
    "info": "",
    "gas_wanted": "1",
    "gas_used": "0",
    "events": [
      {
        "type": "app",
        "attributes": [
          {
            "key": "YWN0aW9u",
            "value": "c2VuZA==",
            "index": false
          }
        ]
      }
    ],
    "codespace": "bank"
  },
  "id": 0,
  "jsonrpc": "2.0"
}
```

## **ABCI**

**ABCI APIs**

### `GET​/abci_info` _\*\*_

**Description**

Get some info about the application

**Parameters**

No parameters

**Example JSON Output**

```javascript
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "response": {
      "data": "{\"size\":0}",
      "version": "0.16.1",
      "app_version": "1314126"
    }
  }
}
```

### `GET​/abci_query`

**Description**

Query the application for some information

**Parameters**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>path</b>
      </td>
      <td style="text-align:left">string * required</td>
      <td style="text-align:left">Path to the data (&quot;/a/b/c&quot;)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>data</b>
      </td>
      <td style="text-align:left">string * required</td>
      <td style="text-align:left">Data</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>height</b>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">
        <p>Height (0 means latest)</p>
        <p>Default value : 0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>prove</b>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>Include proofs of the transactions inclusions in the block</p>
        <p>Default value : false</p>
      </td>
    </tr>
  </tbody>
</table>

**Example JSON Output**

```javascript
{
  "error": "",
  "result": {
    "response": {
      "log": "exists",
      "height": "0",
      "proof": "010114FED0DAD959F36091AD761C922ABA3CBF1D8349990101020103011406AA2262E2F448242DF2C2607C3CDC705313EE3B0001149D16177BC71E445476174622EA559715C293740C",
      "value": "61626364",
      "key": "61626364",
      "index": "-1",
      "code": "0"
    }
  },
  "id": 0,
  "jsonrpc": "2.0"
}
```

## **Unsafe**

**Unsafe APIs**

### `GET​/dial_seeds`

**Description**

Dial Seeds \(unsafe\)

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **peers** | \(array\[string\]\) | List of seed nodes to dial |

**Example JSON Output**

```javascript
{
  "Log": "Dialing seeds in progress. See /net_info for details"
}
```

### `GET​/dial_peers`

**Description**

Add Peers/Persistent Peers \(unsafe\)

**Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| **hash** | string \* required | Have the peers you are dialing be persistent |
| **persistent** | boolean | Have the peers you are dialing be unconditional |
| **unconditional** | boolean | Have the peers you are dialing be private |
| **peers** | \(array\[string\]\) | Array of peers to dial |

**Example JSON Output**

```javascript
{
  "Log": "Dialing seeds in progress. See /net_info for details"
}
```

