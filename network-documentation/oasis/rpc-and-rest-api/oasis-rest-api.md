---
description: Learn how to interact with Figment's Oasis REST API
---

# Oasis REST API

## Source Documentation

You can review the full documentation on [**Figment's Github here**](https://github.com/figment-networks/oasishub-indexer#available-endpoints).

## Methods

### `GET/health`

**Description**

Check the endpoint's health.

**Parameters**

No parameters.

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/health
```

**Example JSON output**

```javascript
ok
```

### `GET/status`

**Description**

Check the status of the application and the chain.

**Parameters**

No parameters.

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/status
```

**Example JSON output**

```javascript
{
 "app_name": "oasishub-indexer",
 "app_version": "0.7.2",
 "go_version": "1.14",
 "chain_app_version": 1703936,
 "chain_block_version": 11,
 "chain_id": "c93ff310b77d68d236d35f9df5d9a37073a88d388a29bd88d8",
 "chain_name": "testnet-2020-09-15",
 "genesis_height": 1,
 "genesis_time": "2020-09-15T09:24:48.619538826+02:00",
 "last_index_version": 2,
 "last_indexed_height": 308,
 "last_indexed_time": "2020-08-06T17:20:03Z",
 "last_indexed_at": "2020-08-28T20:14:23.814427Z",
 "indexing_lag": 508813
}
```

### `GET/block`

**Description**

Return block information by height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer | Block height. Default: 0 = last block |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/block?height=300
```

**Example JSON output**

```javascript
{
 "app_version": 4294967296,
 "block_version": 11,
 "chain_id": "c93ff310b77d68d236d35f9df5d9a37073a88d388a29bd88d8",
 "height": 300,
 "time": "2020-09-15T10:07:19+02:00",
 "last_block_id_hash":
 "7CAA343A9FF4AD7C720346A6378B578D769E46D633091EC88D655313BCB2F3D8",
 "last_commit_hash":
 "42C3977D4C658FD807DD21BD7485D00869B6C089ECEEFBAE8B7932801531DCE5",
 "data_hash":
 "E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855",
 "validators_hash":
 "4246BB476F9329E17D838A769BAA0A756037EE99982E8F11417D1433C3845F4C",
 "next_validators_hash":
 "4246BB476F9329E17D838A769BAA0A756037EE99982E8F11417D1433C3845F4C",
 "consensus_hash":
 "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
 "app_hash": "DB98AF442B8A0331EBD45B9F38755C12F83C3486C4F32F05A3396BEE8CCF301F",
 "last_results_hash":
 "E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855",
 "evidence_hash":
 "E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855",
 "proposer_address": "A9972E73FDAAFF793118561456D8C89A610D9E2B"
}
```

### `GET/block_times/:limit`

**Description**

Get the last X block times.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **limit** | integer \* required | limit of blocks queried |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/block_times/5
```

**Example JSON output**

```javascript
{
 "start_height": 304,
 "end_height": 308,
 "start_time": "2020-08-06T17:19:35Z",
 "end_time": "2020-08-06T17:20:03Z",
 "count": 5,
 "diff": 28,
 "avg": 5.6
}
```

### `GET/blocks_summary`

**Description**

Get a summary of block data over a defined period of time.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **interval** | string \* required | Time interval: `hour` or  `day` |
| **period** | string \* required | Summary period \(i.e. 24 hours\) |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/blocks_summary?interval=hour&period=8%20hours
```

**Example JSON output**

```javascript
[
 {
  "id": 479,
  "created_at": "2020-10-20T18:00:27.020065Z",
  "updated_at": "2020-10-20T19:00:27.011807Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-20T18:00:00Z",
  "count": 610,
  "block_time_avg": 5.886885
 },
 {
  "id": 480,
  "created_at": "2020-10-20T19:00:27.015561Z",
  "updated_at": "2020-10-20T20:00:27.011526Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-20T19:00:00Z",
  "count": 611,
  "block_time_avg": 5.88707
 },
 {
  "id": 481,
  "created_at": "2020-10-20T20:00:27.014892Z",
  "updated_at": "2020-10-20T21:00:23.01481Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-20T20:00:00Z",
  "count": 610,
  "block_time_avg": 5.888525
 },
 {
  "id": 482,
  "created_at": "2020-10-20T21:00:23.018495Z",
  "updated_at": "2020-10-20T22:00:23.013671Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-20T21:00:00Z",
  "count": 611,
  "block_time_avg": 5.88216
 },
 {
  "id": 483,
  "created_at": "2020-10-20T22:00:23.017555Z",
  "updated_at": "2020-10-20T23:00:23.014185Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-20T22:00:00Z",
  "count": 607,
  "block_time_avg": 5.920923
 },
 {
  "id": 484,
  "created_at": "2020-10-20T23:00:23.018068Z",
  "updated_at": "2020-10-21T00:00:23.012465Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-20T23:00:00Z",
  "count": 608,
  "block_time_avg": 5.904605
 },
 {
  "id": 485,
  "created_at": "2020-10-21T00:00:23.016585Z",
  "updated_at": "2020-10-21T01:00:23.012607Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-21T00:00:00Z",
  "count": 610,
  "block_time_avg": 5.895082
 },
 {
  "id": 487,
  "created_at": "2020-10-21T01:00:23.016834Z",
  "updated_at": "2020-10-21T02:00:23.015921Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-21T01:00:00Z",
  "count": 611,
  "block_time_avg": 5.883797
 },
 {
  "id": 488,
  "created_at": "2020-10-21T02:00:23.019662Z",
  "updated_at": "2020-10-21T03:00:23.013096Z",
  "index_version": 4,
  "time_interval": "hour",
  "time_bucket": "2020-10-21T02:00:00Z",
  "count": 610,
  "block_time_avg": 5.891803
 }
 ]
```

### `GET/transactions`

**Description**

Get a list of transactions at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/transactions?height=3000
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "public_key": "I/Vnwyi7FJdROFe64fbaqE3t55OLcUBY8hVK64VNrqc=",
   "hash":
   "dea9ee824c213baaa4b826d16617cf8f256cc1e42b08f464726cff274a866ad5",
   "nonce": 494,
   "fee": 0,
   "gas_limit": 1172,
   "gas_price": 0,
   "method": "registry.RegisterNode",
   "signature_verified": true
  },
  {
   "public_key": "ejPrx9xTpKV3GTZgthFQWf3UPMFFBseRtc0A17ak1TU=",
   "hash":
   "8b3d3bf3b888a2ff57b286368a8fd0b0baba0a15c5034470e885be40d09d60b8",
   "nonce": 492,
   "fee": 0,
   "gas_limit": 1172,
   "gas_price": 0,
   "method": "registry.RegisterNode",
   "signature_verified": true
  },
  {
   "public_key": "4rUqFOE27urnaltMm2XqyuxcghXs4xRep3AV3mXSTt4=",
   "hash":
   "326f722ab9871c5b748383957657d6972b1c3ba7a8b848069cd0da5032936beb",
   "nonce": 492,
   "fee": 0,
   "gas_limit": 1172,
   "gas_price": 0,
   "method": "registry.RegisterNode",
   "signature_verified": true
  },
  {
   "public_key": "70ADXhkVY/lhHUrQ97yLuAikRrLc8Ypkp3vkO0VnEXk=",
   "hash":
   "4f3b7d7ff1fdf644d7fa5346cac2ba343117c47c15785b1cafdf0e51c0590464",
   "nonce": 494,
   "fee": 0,
   "gas_limit": 1172,
   "gas_price": 0,
   "method": "registry.RegisterNode",
   "signature_verified": true
  },
  {
   "public_key": "hDQp4FhwWREN09nSGMPJAEYKeCmxG/joQivxfY3vyi8=",
   "hash":
   "9275891ff310cf848b6847fc9b9c217beb4a919990fbcb49bbe054388784c086",
   "nonce": 492,
   "fee": 0,
   "gas_limit": 1172, 
   "gas_price": 0,
   "method": "registry.RegisterNode",
   "signature_verified": true
  }
 ]
}
```

### `GET/staking`

**Description**

Get staking data at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/staking?height=3000
```

**Example JSON output**

```javascript
{
 "total_supply": 10000000000000000000,
 "common_pool": 1872841004008158000,
 "debonding_interval": 336,
 "min_delegation_amount": 100000000000
}
```

### `GET/delegations`

**Description**

Get a list of delegations at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/delegations?height=3000
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "validator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "delegator_uid": "oasis1qpdks9ccwxa27hyccd78d58vhpl9wyddmy4xvhvk",
   "shares": 6081081000000000
  },
  {
   "validator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "delegator_uid": "oasis1qp7hpak0wuymn3pqtwf2cpaxsm25v6ydhuzkxupe",
   "shares": 41340000000000000
  },
  {
   "validator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "delegator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "shares": 947568821268224
  },
  {
   "validator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "delegator_uid": "oasis1qrad7s7nqm4gvyzr8yt2rdk0ref489rn3vn400d6",
   "shares": 44785000000000000
  },
  {
   "validator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "delegator_uid": "oasis1qqs6ylpfurhf6gc9mw232fkmrt3d0673lyzc5xf2",
   "shares": 27027027000000000
  },
  {
   "validator_uid": "oasis1qq3xrq0urs8qcffhvmhfhz4p0mu7ewc8rscnlwxe",
   "delegator_uid": "oasis1qq3xrq0urs8qcffhvmhfhz4p0mu7ewc8rscnlwxe",
   "shares": 51870937969335
  },
  {
   "validator_uid": "oasis1qq3xrq0urs8qcffhvmhfhz4p0mu7ewc8rscnlwxe",
   "delegator_uid": "oasis1qpdks9ccwxa27hyccd78d58vhpl9wyddmy4xvhvk",
   "shares": 12162162000000000
  }
 ]
}
```

### `GET/delegations/:address`

**Description**

Get a list of delegations for an address at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Address of the account. |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/delegations/oasis1qresj0vhmwawll6fe2vw2nlapkp6nj6etcx7a32h?height=3000
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "validator_uid": "",
   "delegator_uid": "oasis1qz22xm9vyg0uqxncc667m4j4p5mrsj455c743lfn",
   "shares": 947568821268224
  }
 ]
}
```

### `GET/debonding_delegations`

**Description**

Get a list of unbonding delegations at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/debonding_delegations?height=3000
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "validator_uid": "oasis1qq0xmq7r0z9sdv02t5j9zs7en3n6574gtg8v9fyt",
   "delegator_uid": "oasis1qq0xmq7r0z9sdv02t5j9zs7en3n6574gtg8v9fyt",
   "shares": 200479964729758,
   "debond_end": 502
  },
  {
   "validator_uid": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "delegator_uid": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "shares": 25160,
   "debond_end": 783
  },
  {
   "validator_uid": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "delegator_uid": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "shares": 25160831413870,
   "debond_end": 783
  },
  {
   "validator_uid": "oasis1qp4rp7adhegfktyg4aq3w6jelqumx6klfv5t7kvv",
   "delegator_uid": "oasis1qp4rp7adhegfktyg4aq3w6jelqumx6klfv5t7kvv",
   "shares": 60253851657470,
   "debond_end": 644
  },
  {
   "validator_uid": "oasis1qrs8zlh0mj37ug0jzlcykz808ylw93xwkvknm7yc",
   "delegator_uid": "oasis1qrs8zlh0mj37ug0jzlcykz808ylw93xwkvknm7yc",
   "shares": 30185987205492,
   "debond_end": 624
  },
  {
   "validator_uid": "oasis1qp4f47plgld98n5g2ltalalnndnzz96euv9n89lz",
   "delegator_uid": "oasis1qp4f47plgld98n5g2ltalalnndnzz96euv9n89lz",
   "shares": 10057247902324,
   "debond_end": 753
  },
  {
   "validator_uid": "oasis1qp4f47plgld98n5g2ltalalnndnzz96euv9n89lz",
   "delegator_uid": "oasis1qp4f47plgld98n5g2ltalalnndnzz96euv9n89lz",
   "shares": 90515231120916,
   "debond_end": 753
  },
  {
   "validator_uid": "oasis1qqx820g2geqzeyeyfnm5hgz72eaj9emajgqmscy0",
   "delegator_uid": "oasis1qqx820g2geqzeyeyfnm5hgz72eaj9emajgqmscy0",
   "shares": 25170015125066,
   "debond_end": 812
  },
  {
   "validator_uid": "oasis1qzugextrcdueshq63w7l9x4xglnusznsgqa95w7e",
   "delegator_uid": "oasis1qzugextrcdueshq63w7l9x4xglnusznsgqa95w7e",
   "shares": 100291669527,
   "debond_end": 548
  },
  {
   "validator_uid": "oasis1qz72lvk2jchk0fjrz7u2swpazj3t5p0edsdv7sf8",
   "delegator_uid": "oasis1qz72lvk2jchk0fjrz7u2swpazj3t5p0edsdv7sf8",
   "shares": 1303746994205131,
   "debond_end": 542
  },
  {
   "validator_uid": "oasis1qr0jwz65c29l044a204e3cllvumdg8cmsgt2k3ql",
   "delegator_uid": "oasis1qr0jwz65c29l044a204e3cllvumdg8cmsgt2k3ql",
   "shares": 50181679498740,
   "debond_end": 594
  },
  {
   "validator_uid": "oasis1qr0jwz65c29l044a204e3cllvumdg8cmsgt2k3ql",
   "delegator_uid": "oasis1qr0jwz65c29l044a204e3cllvumdg8cmsgt2k3ql",
   "shares": 50198690719128,
   "debond_end": 619
  }
 ]
}
```

### `GET/debonding_delegations/:address`

**Description**

Get a list of unbonding delegations for an address at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Address of the account |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/debonding_delegations/oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt?height=3000
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "delegator_uid": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "shares": 25160,
   "debond_end": 783
  },
  {
   "delegator_uid": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "shares": 25160831413870,
   "debond_end": 783
  }
 ]
}
```

### `GET/account/:address`

**Description**

Get the details for an account at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Address of the account |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/account/oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt?height=3000
```

**Example JSON output**

```javascript
{
 "general_balance": 99999993476,
 "general_nonce": 5,
 "escrow_active_balance": 36013963721772220,
 "escrow_active_total_shares": 36013963721772220,
 "escrow_debonding_balance": 25160831439030,
 "escrow_debonding_total_shares": 25160831439030
}
```

### `GET/validators`

**Description**

Get the list of validators at a given height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer | Block height. Default: 0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/validators?height=294601
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "height": 294601,
   "time": "2020-10-21T18:20:52Z",
   "entity_uid": "RFpWeibJDHnfgoq9mO1BJcxyDbIstDi22ZBhvgXvE1Y=",
   "address": "oasis1qptk3ydjxuq3eenqwljdy45uxdye5tfg4sqar0fz",
   "proposed": false,
   "voting_power": 2856488193592111,
   "total_shares": 45365768233650880,
   "active_escrow_balance": 45704540073260780,
   "commission": 5000,
   "rewards": 0,
   "precommit_validated": true,
   "entity_name": ""
  },
  {
   "height": 294601,
   "time": "2020-10-21T18:20:52Z",
   "entity_uid": "9D+kziTxFhg77+cyt+Fwd6eXREkZ1wHw7WX7VG57MeA=",
   "address": "oasis1qpn83e8hm3gdhvpfv66xj3qsetkj3ulmkugmmxn3",
   "proposed": false,
   "voting_power": 3060577020321578,
   "total_shares": 48607037157239100,
   "active_escrow_balance": 48970013384400830,
   "commission": 5000,
   "rewards": 0,
   "precommit_validated": true,
   "entity_name": ""
  },
  {
   "height": 294601,
   "time": "2020-10-21T18:20:52Z",
   "entity_uid": "kfr2A6K6TlvhQm4nz88Hczzkd2Aq5PlkxSpnmUUBAFs=",
   "address": "oasis1qr0jwz65c29l044a204e3cllvumdg8cmsgt2k3ql",
   "proposed": false,
   "voting_power": 12483625971867172,
   "total_shares": 198390369917524500,
   "active_escrow_balance": 199741201371222750,
   "commission": 15000,
   "rewards": 0,
   "precommit_validated": true,
   "entity_name": ""
  }
 ]
}
```

### `GET/validators/for_min_height/:height`

**Description**

Get the list of validators for all blocks higher than the provided height.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **height** | integer \* required | Block height. Default:0 = last |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/validators/for_min_height/3000
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "id": 72,
   "created_at": "2020-10-02T15:42:37.390745Z",
   "updated_at": "2020-10-21T18:58:04.87753Z",
   "started_at_height": 1,
   "started_at": "2020-10-01T16:00:00Z",
   "recent_at_height": 294979,
   "recent_at": "2020-10-21T18:57:54Z",
   "address": "oasis1qqf6wmc0ax3mykd028ltgtqr49h3qffcm50gwag3",
   "entity_uid": "D8oCKJab4LtOMQJR0YQZXx+fMw6QHyTiv3YCfN8tM18=",
   "recent_tendermint_address": "751FB63DFE5AC161B447F83DFB444C53B9CEC025",
   "recent_voting_power": 2149106241687197,
   "recent_total_shares": 34131370081831164,
   "recent_active_escrow_balance": 34386248318908044,
   "recent_commission": 5000,
   "recent_rewards": 0,
   "recent_as_validator_height": 294979,
   "recent_proposed_height": 294949,
   "accumulated_proposed_count": 2914,
   "accumulated_uptime": 294073,
   "accumulated_uptime_count": 294842,
   "logo_url": "",
   "entity_name": ""
  },
  {
   "id": 60,
   "created_at": "2020-10-02T15:42:37.369011Z",
   "updated_at": "2020-10-21T18:58:04.84607Z",
   "started_at_height": 1,
   "started_at": "2020-10-01T16:00:00Z",
   "recent_at_height": 294979,
   "recent_at": "2020-10-21T18:57:54Z",
   "address": "oasis1qpjuke27se2wnmvx6e8uc4l5h44yjp9h7g2clqfq",
   "entity_uid": "3DRMMM7ye2HREvk8zz06OjMG6BuWjs84PLdSYChNHAw=",
   "recent_tendermint_address": "A3A84620E8BF4352F66136F2F1BED2D8B260FFB8",
   "recent_voting_power": 2252410462624335,
   "recent_total_shares": 35772012376486948,
   "recent_active_escrow_balance": 36039142217139430,
   "recent_commission": 5000,
   "recent_rewards": 0,
   "recent_as_validator_height": 294979,
   "recent_proposed_height": 294966,
   "accumulated_proposed_count": 3051,
   "accumulated_uptime": 294099,
   "accumulated_uptime_count": 294846,
   "logo_url": "",
   "entity_name": ""
  },
  {
   "id": 20,
   "created_at": "2020-10-02T15:42:37.291957Z",
   "updated_at": "2020-10-21T18:58:04.769736Z",
   "started_at_height": 1,
   "started_at": "2020-10-01T16:00:00Z",
   "recent_at_height": 294979,
   "recent_at": "2020-10-21T18:57:54Z",
   "address": "oasis1qram2p9w3yxm4px5nth8n7ugggk5rr6ay5d284at",
   "entity_uid": "RZowTXmfT+b6H6Vuz97VECIy2cq8tytTilv8AxbtvO8=",
   "recent_tendermint_address": "4BFB3C2D1A495BBAE7569FFF15FEC5C2125F2083",
   "recent_voting_power": 2689563690248565,
   "recent_total_shares": 42714730379481500,
   "recent_active_escrow_balance": 43033705420630800,
   "recent_commission": 5000,
   "recent_rewards": 0,
   "recent_as_validator_height": 294979,
   "recent_proposed_height": 294917,
   "accumulated_proposed_count": 3644,
   "accumulated_uptime": 294104,
   "accumulated_uptime_count": 294857,
   "logo_url": "",
   "entity_name": ""
  }
 ]
}
```

### `GET/validator/:address`

**Description**

Get validator details from its account address.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | The validator's address |
| **sequences\_limit** | integer | Number of sequences to include |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/validator/oasis1qqf6wmc0ax3mykd028ltgtqr49h3qffcm50gwag3?sequences_limit=1
```

**Example JSON output**

```javascript
{
 "id": 72,
 "created_at": "2020-10-02T15:42:37.390745Z",
 "updated_at": "2020-10-21T19:02:34.606486Z",
 "started_at_height": 1,
 "started_at": "2020-10-01T16:00:00Z",
 "recent_at_height": 295025,
 "recent_at": "2020-10-21T19:02:26Z",
 "address": "oasis1qqf6wmc0ax3mykd028ltgtqr49h3qffcm50gwag3",
 "entity_uid": "D8oCKJab4LtOMQJR0YQZXx+fMw6QHyTiv3YCfN8tM18=",
 "recent_tendermint_address": "751FB63DFE5AC161B447F83DFB444C53B9CEC025",
 "recent_voting_power": 2149106241687197,
 "recent_total_shares": 34131370081831164,
 "recent_active_escrow_balance": 34386248318908044,
 "recent_as_validator_height": 295025,
 "recent_proposed_height": 294949,
 "accumulated_proposed_count": 2914,
 "uptime": 0.9973922302704755,
 "logo_url": "",
 "entity_name": "",
 "last_sequences": [
    {
        "id": 72078735,
        "height": 295025,
        "time": "2020-10-21T19:02:26Z",
        "entity_uid": "D8oCKJab4LtOMQJR0YQZXx+fMw6QHyTiv3YCfN8tM18=",
        "address": "oasis1qqf6wmc0ax3mykd028ltgtqr49h3qffcm50gwag3",
        "proposed": true,
        "voting_power": 2149106241687197,
        "total_shares": 34131370081831164,
        "active_escrow_balance": 34386248318908044,
        "commission": 15000,
        "rewards": 0,
        "precommit_validated": true
    }
 ]
}
```

### `GET/validators_summary`

**Description**

Get a summary of all active validators during a given time period.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **interval** | string \* required | Time interval: `hour` or  `day` |
| **period** | string \* required | Summary period \(i.e. 24 hours\) |
| **address** | string | Address of validator |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/validators_summary?address=oasis1qqf6wmc0ax3mykd028ltgtqr49h3qffcm50gwag3&interval=hour&period=2%20hours
```

**Example JSON output**

```javascript
[
 {
  "time_bucket": "2020-10-20T19:00:00Z",
  "time_interval": "hour",
  "voting_power_avg": 2839546761061643.5,
  "voting_power_max": 12479047230101820,
  "voting_power_min": 6296627070993,
  "total_shares_avg": 45126947609382110,
  "total_shares_max": 198379453452858300,
  "total_shares_min": 100037249606298,
  "active_escrow_balance_avg": 45433470051629280,
  "active_escrow_balance_max": 199667940334482240,
  "active_escrow_balance_min": 100747640035131,
  "commission_avg": 9480,
  "commission_max": 50000,
  "commission_min": 1000,
  "validated_sum": 46791,
  "not_validated_sum": 256,
  "proposed_sum": 611,
  "uptime_avg": 0.9945586328565051
 },
 {
  "time_bucket": "2020-10-20T20:00:00Z",
  "time_interval": "hour",
  "voting_power_avg": 2839592637175597,
  "voting_power_max": 12479246270905140,
  "voting_power_min": 6296727502195,
  "total_shares_avg": 45127021049462970,
  "total_shares_max": 198379928069266080,
  "total_shares_min": 100037329384794,
  "active_escrow_balance_avg": 45434201576619144,
  "active_escrow_balance_max": 199671125038130560,
  "active_escrow_balance_min": 100749246959989,
  "commission_avg": 9480,
  "commission_max": 50000,
  "commission_min": 1000,
  "validated_sum": 46899,
  "not_validated_sum": 71,
  "proposed_sum": 610,
  "uptime_avg": 0.9984883968490526
 },
 {
  "time_bucket": "2020-10-20T21:00:00Z",
  "time_interval": "hour",
  "voting_power_avg": 2839638387572298.5,
  "voting_power_max": 12479445314883160,
  "voting_power_min": 6296827934999,
  "total_shares_avg": 45127094721467976,
  "total_shares_max": 198380402686809380,
  "total_shares_min": 100037409163354,
  "active_escrow_balance_avg": 45434938876873290,
  "active_escrow_balance_max": 199674309792574900,
  "active_escrow_balance_min": 100750853910478,
  "commission_avg": 9475,
  "commission_max": 50000,
  "commission_min": 1000,
  "validated_sum": 46957,
  "not_validated_sum": 90,
  "proposed_sum": 611,
  "uptime_avg": 0.9980870193636151
 }
]
```

### `GET/system_events/:address`

**Description**

Get all system events for a given account.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **address** | string \* required | Address of the account |
| **after** | integer | Returns events from blocks after the provided provided height |
| **kind** | string | Type of system event |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/system_events/oasis1qqf6wmc0ax3mykd028ltgtqr49h3qffcm50gwag3&after=300
```

**Example JSON output**

```javascript
{
 "items": [
  {
   "height": 1,
   "time": "2020-10-01T16:00:00Z",
   "actor": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "kind": "joined_active_set",
   "data": {}
  },
  {
   "height": 15600,
   "time": "2020-10-02T17:33:48Z",
   "actor": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "kind": "commission_change_3",
   "data": {
    "after": 10000,
    "before": 5000,
    "change": -100
   }
  },
  {
   "height": 250800,
   "time": "2020-10-18T18:39:22Z",
   "actor": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "kind": "commission_change_3",
   "data": {
    "after": 15000,
    "before": 10000,
    "change": -50
   }
  },
  {
   "height": 268579,
   "time": "2020-10-19T23:40:10Z",
   "actor": "oasis1qzmwdlxy7cltmwt99u9pwqt3g0rdwgsqyvcqymmt",
   "kind": "active_escrow_balance_change_1",
   "data": {
    "after": 35988698190236376,
    "before": 36013859021650250,
    "change": 0.1
   }
  }
 ]
}
```

### `POST/transactions`

**Description**

Broadcast a transaction.

**Parameters**

| **Parameter** | Type | Description |
| :--- | :--- | :--- |
| **tx\_raw** | string \* required | Base64 encoded string of a cbor marshalled [transaction.SignedTransaction](https://pkg.go.dev/github.com/oasisprotocol/oasis-core/go/consensus/api/transaction#SignedTransaction) |

**Example Request**

```javascript
oasis--testnet.datahub.figment.io/transactions
```

**Example POST Body**

```javascript
{
 "tx_raw": "omlzaWduYXR1cmWiaXNpZ25hdHVyZVhA7B57K6i0/rqq02oMySmV5AsuUAiYf4N+H8K2OVN2Ubi7dHiuWEQSyq5S/43DzD63sqHF0nVpYKs3zqfaqdKDB2pwdWJsaWNfa2V5WCCth1d3RkFcjAMJgKhPg1SDE8txkHh60uKVe/z28yzJ1HN1bnRydXN0ZWRfcmF3X3ZhbHVlWGakY2ZlZaJjZ2FzGQPoZmFtb3VudEBkYm9keaJmYW1vdW50RQEqBfIAZ2FjY291bnRVAJTs8incWAoRxDVInbaXHIcZaYbnZW5vbmNlAGZtZXRob2Rxc3Rha2luZy5BZGRFc2Nyb3c=",
}
```

**Example JSON output**

```javascript
{
 "submitted": true
}
```

