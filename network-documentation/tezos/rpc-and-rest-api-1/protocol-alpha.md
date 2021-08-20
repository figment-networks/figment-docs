---
description: Learn how to interact with the Tezos RPC
---

# Protocol Alpha

## Block Context

### **`GET ../<block_id>`**

**Description**

Get all the information about a block

**JSON Output**

```javascript
{ "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
    "chain_id": $Chain_id,
    "hash": $block_hash,
    "header": $raw_block_header,
    "metadata"?: $block_header_metadata,
    "operations": [ [ $operation ... ] ... ] }
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $block_header_metadata:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "next_protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "test_chain_status": $test_chain_status,
      "max_operations_ttl": integer ∈ [-2^30-2, 2^30+2],
      "max_operation_data_length": integer ∈ [-2^30-2, 2^30+2],
      "max_block_header_length": integer ∈ [-2^30-2, 2^30+2],
      "max_operation_list_length":
        [ { "max_size": integer ∈ [-2^30-2, 2^30+2],
            "max_op"?: integer ∈ [-2^30-2, 2^30+2] } ... ],
      "baker": $Signature.Public_key_hash,
      "level":
        { "level":
            integer ∈ [-2^31-2, 2^31+2]
            /* The level of the block relative to genesis. This is also the
               Shell's notion of level */,
          "level_position":
            integer ∈ [-2^31-2, 2^31+2]
            /* The level of the block relative to the block that starts
               protocol alpha. This is specific to the protocol alpha. Other
               protocols might or might not include a similar notion. */,
          "cycle":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current cycle's number. Note that cycles are a
               protocol-specific notion. As a result, the cycle number starts
               at 0 with the first block of protocol alpha. */,
          "cycle_position":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current level of the block relative to the first block of
               the current cycle. */,
          "voting_period":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current voting period's index. Note that cycles are a
               protocol-specific notion. As a result, the voting period index
               starts at 0 with the first block of protocol alpha. */,
          "voting_period_position":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current level of the block relative to the first block of
               the current voting period. */,
          "expected_commitment":
            boolean
            /* Tells wether the baker of this block has to commit a seed
               nonce hash. */ },
      "voting_period_kind":
        "proposal" || "testing_vote" || "testing" || "promotion_vote",
      "nonce_hash": $cycle_nonce /* Some */ || null /* None */,
      "consumed_gas": $positive_bignum,
      "deactivated": [ $Signature.Public_key_hash ... ],
      "balance_updates": $operation_metadata.alpha.balance_updates }
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $error:
    /* The full list of RPC errors would be too long to include.
       It is available at RPC `/errors` (GET).
       Errors specific to protocol Alpha have an id that starts with
       `proto.alpha`. */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "chain_id": $Chain_id,
      "hash": $Operation_hash,
      "branch": $block_hash,
      "contents": [ $operation.alpha.operation_contents_and_result ... ],
      "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature": $Signature }
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $operation.alpha.internal_operation_result:
    { /* reveal */
      "kind": "reveal",
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "public_key": $Signature.Public_key,
      "result": $operation.alpha.operation_result.reveal }
    || { /* transaction */
         "kind": "transaction",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "result": $operation.alpha.operation_result.transaction }
    || { /* origination */
         "kind": "origination",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "result": $operation.alpha.operation_result.origination }
    || { /* delegation */
         "kind": "delegation",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "delegate"?: $Signature.Public_key_hash,
         "result": $operation.alpha.operation_result.delegation }
  $operation.alpha.operation_contents_and_result:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2],
      "metadata":
        { "balance_updates": $operation_metadata.alpha.balance_updates,
          "delegate": $Signature.Public_key_hash,
          "slots": [ integer ∈ [0, 255] ... ] } }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ],
         "metadata": {  } }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass",
         "metadata": {  } }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.reveal,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.transaction,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.origination,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.delegation,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
  $operation.alpha.operation_result.delegation:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.origination:
    { /* Applied */
      "status": "applied",
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum }
  $operation.alpha.operation_result.reveal:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.transaction:
    { /* Applied */
      "status": "applied",
      "storage"?: $micheline.michelson_v1.expression,
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum,
      "allocated_destination_contract"?: boolean }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "storage"?: $micheline.michelson_v1.expression,
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum,
         "allocated_destination_contract"?: boolean }
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $raw_block_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $test_chain_status:
    /* The status of the test chain: not_running (there is no test chain at
       the moment), forking (the test chain is being setup), running (the
       test chain is running). */
    { /* Not_running */
      "status": "not_running" }
    || { /* Forking */
         "status": "forking",
         "protocol": $Protocol_hash,
         "expiration": $timestamp.protocol }
    || { /* Running */
         "status": "running",
         "chain_id": $Chain_id,
         "genesis": $block_hash,
         "protocol": $Protocol_hash,
         "expiration": $timestamp.protocol }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/big_maps/<big_map_id>/<script_expr>`**

**Description**

Access the value associated with a key in a big map

**JSON Output**

```javascript
  $micheline.michelson_v1.expression
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/constants`**

**Description**

Get all constants

**JSON Output**

```javascript
  { "proof_of_work_nonce_size": integer ∈ [0, 255],
    "nonce_length": integer ∈ [0, 255],
    "max_revelations_per_block": integer ∈ [0, 255],
    "max_operation_data_length": integer ∈ [-2^30-2, 2^30+2],
    "max_proposals_per_delegate": integer ∈ [0, 255],
    "preserved_cycles": integer ∈ [0, 255],
    "blocks_per_cycle": integer ∈ [-2^31-2, 2^31+2],
    "blocks_per_commitment": integer ∈ [-2^31-2, 2^31+2],
    "blocks_per_roll_snapshot": integer ∈ [-2^31-2, 2^31+2],
    "blocks_per_voting_period": integer ∈ [-2^31-2, 2^31+2],
    "time_between_blocks": [ $int64 ... ],
    "endorsers_per_block": integer ∈ [0, 2^16-1],
    "hard_gas_limit_per_operation": $bignum,
    "hard_gas_limit_per_block": $bignum,
    "proof_of_work_threshold": $int64,
    "tokens_per_roll": $mutez,
    "michelson_maximum_type_size": integer ∈ [0, 2^16-1],
    "seed_nonce_revelation_tip": $mutez,
    "origination_size": integer ∈ [-2^30-2, 2^30+2],
    "block_security_deposit": $mutez,
    "endorsement_security_deposit": $mutez,
    "baking_reward_per_endorsement": [ $mutez ... ],
    "endorsement_reward": [ $mutez ... ],
    "cost_per_byte": $mutez,
    "hard_storage_limit_per_operation": $bignum,
    "test_chain_duration": $int64,
    "quorum_min": integer ∈ [-2^31-2, 2^31+2],
    "quorum_max": integer ∈ [-2^31-2, 2^31+2],
    "min_proposal_quorum": integer ∈ [-2^31-2, 2^31+2],
    "initial_endorsers": integer ∈ [0, 2^16-1],
    "delay_per_missing_endorsement": $int64 }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`GET ../<block_id>/context/constants/errors`**

**Description**

Get the schema for all the RPC errors from this protocol version \_\_

**JSON Output**

```text
  any
```

### **`GET ../<block_id>/context/contracts`**

**Description**

Get all existing contracts \(including non-empty default contracts\) _\*\*_

**JSON Output**

```javascript
[ $contract_id ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

**`GET ../<block_id>/context/contracts/<contract_id>`**

**Description**

Access the complete status of a contract _\*\*_

**JSON Output**

```javascript
{ "balance": $mutez,
    "delegate"?: $Signature.Public_key_hash,
    "script"?: $scripted.contracts,
    "counter"?: $positive_bignum }
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/balance`**

**Description**

Access the balance of a contract _\*\*_

**JSON Output**

```javascript
 $mutez
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`POST ../<block_id>/context/contracts/<contract_id>/big_map_get`**

**Description**

Access the value associated with a key in a big map of the contract \(deprecated\) _\*\*_

**JSON Output**

```javascript
$micheline.michelson_v1.expression /* Some */ || null /* None */
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/counter`**

**Description**

Access the counter of a contract, if any

**JSON Output**

```javascript
  $bignum
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
```

### **`GET ../<block_id>/context/contracts/<contract_id>/delegate`**

**Description**

Access the delegate of a contract, if any _\*\*_

**JSON Output**

```javascript
  $Signature.Public_key_hash
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/entrypoints`**

**Description**

Return the list of entrypoints of the contract

**JSON Output**

```javascript
{ "unreachable"?: [ { "path": [ $michelson.v1.primitives ... ] } ... ],
    "entrypoints": { *: $micheline.michelson_v1.expression } }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/entrypoints/<string>`**

**Description**

Return the type of the given entrypoint of the contract _\*\*_

**JSON Output**

```javascript
$micheline.michelson_v1.expression
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/manager_key`**

**Description**

Access the manager of a contract _\*\*_

**JSON Output**

```javascript
  $Signature.Public_key /* Some */ || null /* None */
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/script`**

**Description**

Access the code and data of the contract _\*\*_

**JSON Output**

```javascript
$scripted.contracts
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/contracts/<contract_id>/storage`**

**Description**

Access the data of the contract _\*\*_

**JSON Output**

```javascript
$micheline.michelson_v1.expression
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/delegates?[active]&[inactive]`**

**Description**

List all registered delegates _\*\*_

_Optional query arguments :_

* _active_
* _inactive_

**JSON Output**

```javascript
[ $Signature.Public_key_hash ... ]
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/delegates/<pkh>`**

**Description**

Get everything about a delegate _\*\*_

**JSON Output**

```javascript
{ "balance": $mutez,
    "frozen_balance": $mutez,
    "frozen_balance_by_cycle":
      [ { "cycle": integer ∈ [-2^31-2, 2^31+2],
          "deposit": $mutez,
          "fees": $mutez,
          "rewards": $mutez } ... ],
    "staking_balance": $mutez,
    "delegated_contracts": [ $contract_id ... ],
    "delegated_balance": $mutez,
    "deactivated": boolean,
    "grace_period": integer ∈ [-2^31-2, 2^31+2] }
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/delegates/<pkh>/balance`**

**Description**

Return the full balance of a given delegate, including the frozen balances _\*\*_

**JSON Output**

```javascript
  $mutez
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`GET ../<block_id>/context/delegates/<pkh>/deactivated`**

**Description**

Tell whether the delegate is currently tagged as deactivated or not _\*\*_

**JSON Output**

```javascript
  boolean
```

### **`GET ../<block_id>/context/delegates/<pkh>/delegated_balance`**

**Description**

Return the balance of all the contracts that delegate to a given delegate.

this excludes the delegate's own balance and its frozen balances.

**JSON Output**

```javascript
  $mutez
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`GET ../<block_id>/context/delegates/<pkh>/delegated_contracts`**

**Description**

Return the list of contracts that delegate to a given delegate _\*\*_

**JSON Output**

```javascript
 [ $contract_id ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/delegates/<pkh>/frozen_balance`**

**Description**

Return the total frozen balances of a given delegate. _\*\*_

This includes the frozen deposits, rewards and fees.

**JSON Output**

```javascript
  $mutez
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`GET ../<block_id>/context/delegates/<pkh>/frozen_balance_by_cycle`**

**Description**

Return the frozen balances of a given delegate. _\*\*_

Indexed by the cycle by which it will be unfrozen.

**JSON Output**

```javascript
  [ { "cycle": integer ∈ [-2^31-2, 2^31+2],
      "deposit": $mutez,
      "fees": $mutez,
      "rewards": $mutez } ... ]
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`GET ../<block_id>/context/delegates/<pkh>/grace_period`**

**Description**

Return the cycle by the end of which the delegate might be deativated if she fails to execute any delegate action.

A deactivated delegate might be reactivated \(without loosing any rolls\) by simply re-registering as a delegate. For deactivated delegates, this value contains the cycle by which they were deactivated.

**JSON Output**

```javascript
  integer ∈ [-2^31-2, 2^31+2]
```

### **`GET ../<block_id>/context/delegates/<pkh>/staking_balance`**

**Description**

Return the total amount of tokens delegated to a given delegate

This includes the balances of all the contracts that delegate to it, but also the balance of the delegate itself and its frozen fees and deposits. The rewards do not count in the delegated balance until they are unfrozen.

**JSON Output**

```javascript
  $mutez
  $mutez: $positive_bignum
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
```

### **`GET ../<block_id>/context/nonces/<block_level>`**

**Description**

Get info about the nonce of a previous block _\*\*_

**JSON Output**

```javascript
  { /* Revealed */
    "nonce": /^[a-zA-Z0-9]+$/ }
  || { /* Missing */
       "hash": $cycle_nonce }
  || { /* Forgotten */
        }
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/context/raw/bytes?[depth=<int>]`**

**Description**

Return the raw context. _\*\*_

_Optional query arguments :_

* _depth = &lt;int&gt;_

**JSON Output**

```javascript
  $raw_context
  $raw_context:
    /^[a-zA-Z0-9]+$/
    /* Key */
    || { /* Dir */
         *: $raw_context }
    || null
    /* Cut */
```

### **`POST ../<block_id>/context/seed`**

**Description**

Post the seed of the cycle to which the block belongs _\*\*_

**JSON Output**

```javascript
  /^[a-zA-Z0-9]+$/
```

### **`POST ../<block_id>/endorsing_power`**

**Description**

Get the endorsing power of an endorsement, that is, the number of slots that the endorser has

**JSON Output**

```javascript
 integer ∈ [-2^30-2, 2^30+2]
```

## Block Info

### **`GET ../<block_id>/hash`**

**Description**

Get the block's hash, its unique identifier. _\*\*_

**JSON Output**

```javascript
  $block_hash
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/header`**

**Description**

Get the whole block header _\*\*_

**JSON Output**

```javascript
$block_header
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "chain_id": $Chain_id,
      "hash": $block_hash,
      "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/header/protocol_data`**

**Description**

Get the version-specific fragment of the block header

**JSON Output**

```javascript
  { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
    "priority": integer ∈ [0, 2^16-1],
    "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
    "seed_nonce_hash"?: $cycle_nonce,
    "signature": $Signature }
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/header/protocol_data/raw`**

**Description**

Get the version-specific fragment of the block header \(unparsed\) _\*\*_

**JSON Output**

```javascript
  /^[a-zA-Z0-9]+$/
```

### **`GET ../<block_id>/header/raw`**

**Description**

Get the whole block header \(unparsed\) _\*\*_

**JSON Output**

```javascript
  /^[a-zA-Z0-9]+$/
```

### **`GET ../<block_id>/header/shell`**

**Description**

Get the shell-specific fragment of the block header _\*\*_

**JSON Output**

```javascript
 $block_header.shell
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.shell:
    /* Shell header
       Block header's shell-related content. It contains information such as
       the block level, its predecessor and timestamp. */
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash }
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

## Helpers

### **`GET ../<block_id>/helpers/baking_rights?(level=<block_level>)*&(cycle=<block_cycle>)*&(delegate=<pkh>)*&[max_priority=<int>]&[all]`**

**Description**

Retrieve the list of delegates allowed to bake a block

By default, it gives the best baking priorities for bakers that have at least one opportunity below the 64th priority for the next block. Parameters \`level\` and \`cycle\` can be used to specify the \(valid\) level\(s\) in the past or future at which the baking rights have to be returned. Parameter \`delegate\` can be used to restrict the results to the given delegates. If parameter \`all\` is set, all the baking opportunities for each baker at each level are returned, instead of just the first one. Returns the list of baking slots. Also returns the minimal timestamps that correspond to these slots. The timestamps are omitted for levels in the past, and are only estimates for levels later that the next block, based on the hypothesis that all predecessor blocks were baked at the first priority.

Optional query arguments :

* level = &lt;block\_level&gt;
* cycle = &lt;block\_cycle&gt;
* delegate = &lt;pkh&gt;
* max\_priority = &lt;int&gt;
* all

**JSON Output**

```javascript
  [ { "level": integer ∈ [-2^31-2, 2^31+2],
      "delegate": $Signature.Public_key_hash,
      "priority": integer ∈ [0, 2^16-1],
      "estimated_time"?: $timestamp.protocol } ... ]
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/helpers/complete/<prefix>`**

**Description**

Try to complete a prefix of a Base58Check-encoded data _\*\*_

This RPC is actually able to complete hashes of block, operations, public\_keys and contracts_._

**JSON Output**

```javascript
  [ $unistring ... ]
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/helpers/current_level?[offset=<int32>]`**

**Description**

Return the level of the interrogated block or the one of a block located "offset" blocks after in the chain \(or before when negative\) _\*\*_

For instance, the next block if \`offset\` is 1.

Optional query arguments :

* offset = &lt;int32&gt;

**JSON Output**

```javascript
{ "level":
      integer ∈ [-2^31-2, 2^31+2]
      /* The level of the block relative to genesis. This is also the Shell's
         notion of level */,
    "level_position":
      integer ∈ [-2^31-2, 2^31+2]
      /* The level of the block relative to the block that starts protocol
         alpha. This is specific to the protocol alpha. Other protocols might
         or might not include a similar notion. */,
    "cycle":
      integer ∈ [-2^31-2, 2^31+2]
      /* The current cycle's number. Note that cycles are a protocol-specific
         notion. As a result, the cycle number starts at 0 with the first
         block of protocol alpha. */,
    "cycle_position":
      integer ∈ [-2^31-2, 2^31+2]
      /* The current level of the block relative to the first block of the
         current cycle. */,
    "voting_period":
      integer ∈ [-2^31-2, 2^31+2]
      /* The current voting period's index. Note that cycles are a
         protocol-specific notion. As a result, the voting period index
         starts at 0 with the first block of protocol alpha. */,
    "voting_period_position":
      integer ∈ [-2^31-2, 2^31+2]
      /* The current level of the block relative to the first block of the
         current voting period. */,
    "expected_commitment":
      boolean
      /* Tells wether the baker of this block has to commit a seed nonce
         hash. */ }
```

### **`GET ../<block_id>/helpers/endorsing_rights?(level=<block_level>)*&(cycle=<block_cycle>)*&(delegate=<pkh>)*`**

**Description**

Retrieve the delegates allowed to endorse a block

By default, it gives the endorsement slots for delegates that have at least one in the next block. Parameters \`level\` and \`cycle\` can be used to specify the \(valid\) level\(s\) in the past or future at which the endorsement rights have to be returned. Parameter \`delegate\` can be used to restrict the results to the given delegates. Returns the list of endorsement slots. Also returns the minimal timestamps that correspond to these slots. The timestamps are omitted for levels in the past, and are only estimates for levels later that the next block, based on the hypothesis that all predecessor blocks were baked at the first priority.

Optional query arguments :

* level = &lt;block\_level&gt;
* cycle = &lt;block\_cycle&gt;
* delegate = &lt;pkh&gt;

**JSON Output**

```javascript
 [ { "level": integer ∈ [-2^31-2, 2^31+2],
      "delegate": $Signature.Public_key_hash,
      "slots": [ integer ∈ [0, 2^16-1] ... ],
      "estimated_time"?: $timestamp.protocol } ... ]
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/forge/operations`**

**Description**

Forge an operation _\*\*_

**JSON Output**

```javascript
  /^[a-zA-Z0-9]+$/
```

### **`POST ../<block_id>/helpers/forge/protocol_data`**

**Description**

Forge the protocol-specific part of a block header _\*\*_

**JSON Output**

```javascript
  { "protocol_data": /^[a-zA-Z0-9]+$/ }
```

### **`POST ../<block_id>/helpers/forge_block_header`**

**Description**

Forge a block header

**JSON Output**

```javascript
  { "block": /^[a-zA-Z0-9]+$/ }
```

### **`GET ../<block_id>/helpers/levels_in_current_cycle?[offset=<int32>]`**

**Description**

Get the levels of a cycle _\*\*_

Optional query arguments :

* offset = &lt;int32&gt;

**JSON Output**

```javascript
  { "first": integer ∈ [-2^31-2, 2^31+2],
    "last": integer ∈ [-2^31-2, 2^31+2] }
```

### **`POST ../<block_id>/helpers/parse/block`**

**Method**

Parse a block _\*\*_

**JSON Output**

```javascript
$block_header.alpha.signed_contents
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $block_header.alpha.signed_contents:
    { "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/parse/operations`**

**Description**

Parse operations _\*\*_

**JSON Output**

```javascript
[ { "branch": $block_hash,
      "contents": [ $operation.alpha.contents ... ],
      "signature": $Signature } ... ]
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/preapply/block?[sort]&[timestamp=<date>]`**

**Description**

Simulate the validation of a block that would contain the given operations and return the resulting fitness and context hash

Optional query arguments :

* sort
* timestamp = &lt;date&gt;

**JSON Output**

```javascript
{ "shell_header": $block_header.shell,
    "operations":
      [ { "applied":
            [ { "hash": $Operation_hash,
                "branch": $block_hash,
                "data": /^[a-zA-Z0-9]+$/ } ... ],
          "refused":
            [ { "hash": $Operation_hash,
                "branch": $block_hash,
                "data": /^[a-zA-Z0-9]+$/,
                "error": $error } ... ],
          "branch_refused":
            [ { "hash": $Operation_hash,
                "branch": $block_hash,
                "data": /^[a-zA-Z0-9]+$/,
                "error": $error } ... ],
          "branch_delayed":
            [ { "hash": $Operation_hash,
                "branch": $block_hash,
                "data": /^[a-zA-Z0-9]+$/,
                "error": $error } ... ] } ... ] }
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.shell:
    /* Shell header
       Block header's shell-related content. It contains information such as
       the block level, its predecessor and timestamp. */
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash }
  $error:
    /* The full list of error is available with the global RPC `GET errors` */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/preapply/operations`**

**Description**

Simulate the validation of an operation _\*\*_

**JSON Output**

```javascript
 [ $operation.alpha.operation_with_metadata ... ]
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $error:
    /* The full list of RPC errors would be too long to include.
       It is available at RPC `/errors` (GET).
       Errors specific to protocol Alpha have an id that starts with
       `proto.alpha`. */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $operation.alpha.internal_operation_result:
    { /* reveal */
      "kind": "reveal",
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "public_key": $Signature.Public_key,
      "result": $operation.alpha.operation_result.reveal }
    || { /* transaction */
         "kind": "transaction",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "result": $operation.alpha.operation_result.transaction }
    || { /* origination */
         "kind": "origination",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "result": $operation.alpha.operation_result.origination }
    || { /* delegation */
         "kind": "delegation",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "delegate"?: $Signature.Public_key_hash,
         "result": $operation.alpha.operation_result.delegation }
  $operation.alpha.operation_contents_and_result:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2],
      "metadata":
        { "balance_updates": $operation_metadata.alpha.balance_updates,
          "delegate": $Signature.Public_key_hash,
          "slots": [ integer ∈ [0, 255] ... ] } }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ],
         "metadata": {  } }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass",
         "metadata": {  } }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.reveal,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.transaction,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.origination,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.delegation,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
  $operation.alpha.operation_result.delegation:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.origination:
    { /* Applied */
      "status": "applied",
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum }
  $operation.alpha.operation_result.reveal:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.transaction:
    { /* Applied */
      "status": "applied",
      "storage"?: $micheline.michelson_v1.expression,
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum,
      "allocated_destination_contract"?: boolean }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "storage"?: $micheline.michelson_v1.expression,
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum,
         "allocated_destination_contract"?: boolean }
  $operation.alpha.operation_with_metadata:
    { /* Operation_with_metadata */
      "contents": [ $operation.alpha.operation_contents_and_result ... ],
      "signature"?: $Signature }
    || { /* Operation_without_metadata */
         "contents": [ $operation.alpha.contents ... ],
         "signature"?: $Signature }
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/entrypoint`**

**Description**

Return the type of the given entrypoint

**JSON Output**

```javascript
{ "entrypoint_type": $micheline.michelson_v1.expression }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/entrypoints`**

**Description**

Return the list of entrypoints of the given script _\*\*_

**JSON Output**

```javascript
{ "unreachable"?: [ { "path": [ $michelson.v1.primitives ... ] } ... ],
    "entrypoints": { *: $micheline.michelson_v1.expression } }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/pack_data`**

**Description**

Compute the serialized version of some data expression using the same algorithm as script instruction PACK _\*\*_

**JSON Output**

```javascript
  { "packed": /^[a-zA-Z0-9]+$/,
    "gas": $bignum /* Limited */ || "unaccounted" }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
```

### **`POST ../<block_id>/helpers/scripts/run_code`**

**Description**

Run a piece of code in the current context _\*\*_

**JSON Output**

```javascript
{ "storage": $micheline.michelson_v1.expression,
    "operations": [ $operation.alpha.internal_operation ... ],
    "big_map_diff"?: $contract.big_map_diff }
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation.alpha.internal_operation:
    { /* Reveal */
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "kind": "reveal",
      "public_key": $Signature.Public_key }
    || { /* Transaction */
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "kind": "transaction",
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "kind": "origination",
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "kind": "delegation",
         "delegate"?: $Signature.Public_key_hash }
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/run_operation`**

**Description**

Run an operation without signature checks _\*\*_

**JSON Output**

```javascript
$operation.alpha.operation_with_metadata
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $error:
    /* The full list of RPC errors would be too long to include.
       It is available at RPC `/errors` (GET).
       Errors specific to protocol Alpha have an id that starts with
       `proto.alpha`. */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $operation.alpha.internal_operation_result:
    { /* reveal */
      "kind": "reveal",
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "public_key": $Signature.Public_key,
      "result": $operation.alpha.operation_result.reveal }
    || { /* transaction */
         "kind": "transaction",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "result": $operation.alpha.operation_result.transaction }
    || { /* origination */
         "kind": "origination",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "result": $operation.alpha.operation_result.origination }
    || { /* delegation */
         "kind": "delegation",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "delegate"?: $Signature.Public_key_hash,
         "result": $operation.alpha.operation_result.delegation }
  $operation.alpha.operation_contents_and_result:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2],
      "metadata":
        { "balance_updates": $operation_metadata.alpha.balance_updates,
          "delegate": $Signature.Public_key_hash,
          "slots": [ integer ∈ [0, 255] ... ] } }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ],
         "metadata": {  } }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass",
         "metadata": {  } }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.reveal,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.transaction,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.origination,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.delegation,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
  $operation.alpha.operation_result.delegation:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.origination:
    { /* Applied */
      "status": "applied",
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum }
  $operation.alpha.operation_result.reveal:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.transaction:
    { /* Applied */
      "status": "applied",
      "storage"?: $micheline.michelson_v1.expression,
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum,
      "allocated_destination_contract"?: boolean }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "storage"?: $micheline.michelson_v1.expression,
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum,
         "allocated_destination_contract"?: boolean }
  $operation.alpha.operation_with_metadata:
    { /* Operation_with_metadata */
      "contents": [ $operation.alpha.operation_contents_and_result ... ],
      "signature"?: $Signature }
    || { /* Operation_without_metadata */
         "contents": [ $operation.alpha.contents ... ],
         "signature"?: $Signature }
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/trace_code`**

**Description**

Run a piece of code in the current context, keeping a trace _\*\*_

**JSON Output**

```javascript
{ "storage": $micheline.michelson_v1.expression,
    "operations": [ $operation.alpha.internal_operation ... ],
    "trace": $scripted.trace,
    "big_map_diff"?: $contract.big_map_diff }
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $micheline.location:
    /* Canonical location in a Micheline expression
       The location of a node in a Micheline expression tree in prefix order,
       with zero being the root and adding one for every basic node, sequence
       and primitive application. */
    integer ∈ [-2^30-2, 2^30+2]
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation.alpha.internal_operation:
    { /* Reveal */
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "kind": "reveal",
      "public_key": $Signature.Public_key }
    || { /* Transaction */
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "kind": "transaction",
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "kind": "origination",
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "kind": "delegation",
         "delegate"?: $Signature.Public_key_hash }
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $scripted.trace:
    [ { "location": $micheline.location,
        "gas": $bignum /* Limited */ || "unaccounted",
        "stack":
          [ { "item": $micheline.michelson_v1.expression,
              "annot"?: $unistring } ... ] } ... ]
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/typecheck_code`**

**Description**

Typecheck a piece of code in the current context _\*\*_

**JSON Output**

```javascript
{ "type_map":
      [ { "location": $micheline.location,
          "stack_before":
            [ [ $micheline.michelson_v1.expression, [ $unistring ... ] ] ... ],
          "stack_after":
            [ [ $micheline.michelson_v1.expression, [ $unistring ... ] ] ... ] } ... ],
    "gas": $bignum /* Limited */ || "unaccounted" }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $micheline.location:
    /* Canonical location in a Micheline expression
       The location of a node in a Micheline expression tree in prefix order,
       with zero being the root and adding one for every basic node, sequence
       and primitive application. */
    integer ∈ [-2^30-2, 2^30+2]
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`POST ../<block_id>/helpers/scripts/typecheck_data`**

**Description**

Check that some data expression is well formed and of a given type in the current context _\*\*_

**JSON Output**

```javascript
  { "gas": $bignum /* Limited */ || "unaccounted" }
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
```

## Block Operations

**`GET ../<block_id>/live_blocks`**

**Description**

List the ancestor of the given block _\*\*_

If referred to as the branch in an operation header, are recent enough for that operation to be included in the current block.

**JSON Output**

```javascript
[ $block_hash ... ]
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/metadata`**

**Description**

Get all the metadata associated to the block _\*\*_

**JSON Output**

```javascript
$block_header_metadata
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header_metadata:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "next_protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "test_chain_status": $test_chain_status,
      "max_operations_ttl": integer ∈ [-2^30-2, 2^30+2],
      "max_operation_data_length": integer ∈ [-2^30-2, 2^30+2],
      "max_block_header_length": integer ∈ [-2^30-2, 2^30+2],
      "max_operation_list_length":
        [ { "max_size": integer ∈ [-2^30-2, 2^30+2],
            "max_op"?: integer ∈ [-2^30-2, 2^30+2] } ... ],
      "baker": $Signature.Public_key_hash,
      "level":
        { "level":
            integer ∈ [-2^31-2, 2^31+2]
            /* The level of the block relative to genesis. This is also the
               Shell's notion of level */,
          "level_position":
            integer ∈ [-2^31-2, 2^31+2]
            /* The level of the block relative to the block that starts
               protocol alpha. This is specific to the protocol alpha. Other
               protocols might or might not include a similar notion. */,
          "cycle":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current cycle's number. Note that cycles are a
               protocol-specific notion. As a result, the cycle number starts
               at 0 with the first block of protocol alpha. */,
          "cycle_position":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current level of the block relative to the first block of
               the current cycle. */,
          "voting_period":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current voting period's index. Note that cycles are a
               protocol-specific notion. As a result, the voting period index
               starts at 0 with the first block of protocol alpha. */,
          "voting_period_position":
            integer ∈ [-2^31-2, 2^31+2]
            /* The current level of the block relative to the first block of
               the current voting period. */,
          "expected_commitment":
            boolean
            /* Tells wether the baker of this block has to commit a seed
               nonce hash. */ },
      "voting_period_kind":
        "proposal" || "testing_vote" || "testing" || "promotion_vote",
      "nonce_hash": $cycle_nonce /* Some */ || null /* None */,
      "consumed_gas": $positive_bignum,
      "deactivated": [ $Signature.Public_key_hash ... ],
      "balance_updates": $operation_metadata.alpha.balance_updates }
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $test_chain_status:
    /* The status of the test chain: not_running (there is no test chain at
       the moment), forking (the test chain is being setup), running (the
       test chain is running). */
    { /* Not_running */
      "status": "not_running" }
    || { /* Forking */
         "status": "forking",
         "protocol": $Protocol_hash,
         "expiration": $timestamp.protocol }
    || { /* Running */
         "status": "running",
         "chain_id": $Chain_id,
         "genesis": $block_hash,
         "protocol": $Protocol_hash,
         "expiration": $timestamp.protocol }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/minimal_valid_time?[priority=<int>]&[endorsing_power=<int>]`**

**Description**

Get the minimal valid time for a block given a priority and an endorsing power _\*\*_

Optional query arguments :

* priority = &lt;int&gt;
* endorsing\_power = &lt;int&gt;

**JSON Output**

```javascript
 $timestamp.protocol
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/operation_hashes`**

**Description**

Get the hashes of all the operations included in the block _\*\*_

**JSON Output**

```javascript
  [ [ $Operation_hash ... ] ... ]
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/operation_hashes/<list_offset>`**

**Description**

Get all the operations included in 'n-th' validation pass of the block _\*\*_

**JSON Output**

```javascript
  [ $Operation_hash ... ]
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/operation_hashes/<list_offset>/<operation_offset>`**

**Description**

Get the hash of then 'm-th' operation in the 'n-th' validation pass of the block _\*\*_

**JSON Output**

```javascript
  $Operation_hash
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/operations`**

**Description**

Get all the operations included in the block _\*\*_

**JSON Output**

```javascript
[ [ $operation ... ] ... ]
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $error:
    /* The full list of RPC errors would be too long to include.
       It is available at RPC `/errors` (GET).
       Errors specific to protocol Alpha have an id that starts with
       `proto.alpha`. */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "chain_id": $Chain_id,
      "hash": $Operation_hash,
      "branch": $block_hash,
      "contents": [ $operation.alpha.operation_contents_and_result ... ],
      "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature": $Signature }
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $operation.alpha.internal_operation_result:
    { /* reveal */
      "kind": "reveal",
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "public_key": $Signature.Public_key,
      "result": $operation.alpha.operation_result.reveal }
    || { /* transaction */
         "kind": "transaction",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "result": $operation.alpha.operation_result.transaction }
    || { /* origination */
         "kind": "origination",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "result": $operation.alpha.operation_result.origination }
    || { /* delegation */
         "kind": "delegation",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "delegate"?: $Signature.Public_key_hash,
         "result": $operation.alpha.operation_result.delegation }
  $operation.alpha.operation_contents_and_result:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2],
      "metadata":
        { "balance_updates": $operation_metadata.alpha.balance_updates,
          "delegate": $Signature.Public_key_hash,
          "slots": [ integer ∈ [0, 255] ... ] } }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ],
         "metadata": {  } }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass",
         "metadata": {  } }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.reveal,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.transaction,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.origination,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.delegation,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
  $operation.alpha.operation_result.delegation:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.origination:
    { /* Applied */
      "status": "applied",
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum }
  $operation.alpha.operation_result.reveal:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.transaction:
    { /* Applied */
      "status": "applied",
      "storage"?: $micheline.michelson_v1.expression,
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum,
      "allocated_destination_contract"?: boolean }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "storage"?: $micheline.michelson_v1.expression,
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum,
         "allocated_destination_contract"?: boolean }
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/operations/<list_offset>`**

**Description**

Get all the operations included in 'n-th' validation pass of the block _\*\*_

**JSON Output**

```javascript
[ $operation ... ]
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $error:
    /* The full list of RPC errors would be too long to include.
       It is available at RPC `/errors` (GET).
       Errors specific to protocol Alpha have an id that starts with
       `proto.alpha`. */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "chain_id": $Chain_id,
      "hash": $Operation_hash,
      "branch": $block_hash,
      "contents": [ $operation.alpha.operation_contents_and_result ... ],
      "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature": $Signature }
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $operation.alpha.internal_operation_result:
    { /* reveal */
      "kind": "reveal",
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "public_key": $Signature.Public_key,
      "result": $operation.alpha.operation_result.reveal }
    || { /* transaction */
         "kind": "transaction",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "result": $operation.alpha.operation_result.transaction }
    || { /* origination */
         "kind": "origination",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "result": $operation.alpha.operation_result.origination }
    || { /* delegation */
         "kind": "delegation",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "delegate"?: $Signature.Public_key_hash,
         "result": $operation.alpha.operation_result.delegation }
  $operation.alpha.operation_contents_and_result:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2],
      "metadata":
        { "balance_updates": $operation_metadata.alpha.balance_updates,
          "delegate": $Signature.Public_key_hash,
          "slots": [ integer ∈ [0, 255] ... ] } }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ],
         "metadata": {  } }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass",
         "metadata": {  } }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.reveal,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.transaction,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.origination,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.delegation,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
  $operation.alpha.operation_result.delegation:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.origination:
    { /* Applied */
      "status": "applied",
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum }
  $operation.alpha.operation_result.reveal:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.transaction:
    { /* Applied */
      "status": "applied",
      "storage"?: $micheline.michelson_v1.expression,
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum,
      "allocated_destination_contract"?: boolean }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "storage"?: $micheline.michelson_v1.expression,
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum,
         "allocated_destination_contract"?: boolean }
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/operations/<list_offset>/<operation_offset>`**

**Description**

Get the 'm-th' operation in the 'n-th' validation pass of the block _\*\*_

**JSON Output**

```javascript
 $operation
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Ed25519.Public_key_hash:
    /* An Ed25519 public key hash (Base58Check-encoded) */
    $unistring
  $Operation_hash:
    /* A Tezos operation ID (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $Signature:
    /* A Ed25519, Secp256k1 or P256 signature (Base58Check-encoded) */
    $unistring
  $Signature.Public_key:
    /* A Ed25519, Secp256k1, or P256 public key (Base58Check-encoded) */
    $unistring
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $bignum:
    /* Big number
       Decimal representation of a big number */
    string
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header.alpha.full_header:
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "priority": integer ∈ [0, 2^16-1],
      "proof_of_work_nonce": /^[a-zA-Z0-9]+$/,
      "seed_nonce_hash"?: $cycle_nonce,
      "signature": $Signature }
  $contract.big_map_diff:
    [ { /* update */
        "action": "update",
        "big_map": $bignum,
        "key_hash": $script_expr,
        "key": $micheline.michelson_v1.expression,
        "value"?: $micheline.michelson_v1.expression }
      || { /* remove */
           "action": "remove",
           "big_map": $bignum }
      || { /* copy */
           "action": "copy",
           "source_big_map": $bignum,
           "destination_big_map": $bignum }
      || { /* alloc */
           "action": "alloc",
           "big_map": $bignum,
           "key_type": $micheline.michelson_v1.expression,
           "value_type": $micheline.michelson_v1.expression } ... ]
  $contract_id:
    /* A contract handle
       A contract notation as given to an RPC or inside scripts. Can be a
       base58 implicit contract hash or a base58 originated contract hash. */
    $unistring
  $cycle_nonce:
    /* A nonce hash (Base58Check-encoded) */
    $unistring
  $entrypoint:
    /* entrypoint
       Named entrypoint to a Michelson smart contract */
    "default"
    || "root"
    || "do"
    || "set_delegate"
    || "remove_delegate"
    || string
    /* named */
  $error:
    /* The full list of RPC errors would be too long to include.
       It is available at RPC `/errors` (GET).
       Errors specific to protocol Alpha have an id that starts with
       `proto.alpha`. */
    any
  $fitness:
    /* Block fitness
       The fitness, or score, of a block, that allow the Tezos to decide
       which chain is the best. A fitness value is a list of byte sequences.
       They are compared as follows: shortest lists are smaller; lists of the
       same length are compared according to the lexicographical order. */
    [ /^[a-zA-Z0-9]+$/ ... ]
  $inlined.endorsement:
    { "branch": $block_hash,
      "operations": $inlined.endorsement.contents,
      "signature"?: $Signature }
  $inlined.endorsement.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
  $int64:
    /* 64 bit integers
       Decimal representation of 64 bit integers */
    string
  $micheline.michelson_v1.expression:
    { /* Int */
      "int": $bignum }
    || { /* String */
         "string": $unistring }
    || { /* Bytes */
         "bytes": /^[a-zA-Z0-9]+$/ }
    || [ $micheline.michelson_v1.expression ... ]
    /* Sequence */
    || { /* Generic prim (any number of args with or without annot) */
         "prim": $michelson.v1.primitives,
         "args"?: [ $micheline.michelson_v1.expression ... ],
         "annots"?: [ string ... ] }
  $michelson.v1.primitives:
    "ADD"
    | "IF_NONE"
    | "SWAP"
    | "set"
    | "nat"
    | "CHECK_SIGNATURE"
    | "IF_LEFT"
    | "LAMBDA"
    | "Elt"
    | "CREATE_CONTRACT"
    | "NEG"
    | "big_map"
    | "map"
    | "or"
    | "BLAKE2B"
    | "bytes"
    | "SHA256"
    | "SET_DELEGATE"
    | "CONTRACT"
    | "LSL"
    | "SUB"
    | "IMPLICIT_ACCOUNT"
    | "PACK"
    | "list"
    | "PAIR"
    | "Right"
    | "contract"
    | "GT"
    | "LEFT"
    | "STEPS_TO_QUOTA"
    | "storage"
    | "TRANSFER_TOKENS"
    | "CDR"
    | "SLICE"
    | "PUSH"
    | "False"
    | "SHA512"
    | "CHAIN_ID"
    | "BALANCE"
    | "signature"
    | "DUG"
    | "SELF"
    | "EMPTY_BIG_MAP"
    | "LSR"
    | "OR"
    | "XOR"
    | "lambda"
    | "COMPARE"
    | "key"
    | "option"
    | "Unit"
    | "Some"
    | "UNPACK"
    | "NEQ"
    | "INT"
    | "pair"
    | "AMOUNT"
    | "DIP"
    | "ABS"
    | "ISNAT"
    | "EXEC"
    | "NOW"
    | "LOOP"
    | "chain_id"
    | "string"
    | "MEM"
    | "MAP"
    | "None"
    | "address"
    | "CONCAT"
    | "EMPTY_SET"
    | "MUL"
    | "LOOP_LEFT"
    | "timestamp"
    | "LT"
    | "UPDATE"
    | "DUP"
    | "SOURCE"
    | "mutez"
    | "SENDER"
    | "IF_CONS"
    | "RIGHT"
    | "CAR"
    | "CONS"
    | "LE"
    | "NONE"
    | "IF"
    | "SOME"
    | "GET"
    | "Left"
    | "CAST"
    | "int"
    | "SIZE"
    | "key_hash"
    | "unit"
    | "DROP"
    | "EMPTY_MAP"
    | "NIL"
    | "DIG"
    | "APPLY"
    | "bool"
    | "RENAME"
    | "operation"
    | "True"
    | "FAILWITH"
    | "parameter"
    | "HASH_KEY"
    | "EQ"
    | "NOT"
    | "UNIT"
    | "Pair"
    | "ADDRESS"
    | "EDIV"
    | "CREATE_ACCOUNT"
    | "GE"
    | "ITER"
    | "code"
    | "AND"
  $mutez: $positive_bignum
  $operation:
    { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
      "chain_id": $Chain_id,
      "hash": $Operation_hash,
      "branch": $block_hash,
      "contents": [ $operation.alpha.operation_contents_and_result ... ],
      "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature"?: $Signature }
    || { "protocol": "ProtoALphaALphaALphaALphaALphaALphaALphaALphaDdp3zK",
         "chain_id": $Chain_id,
         "hash": $Operation_hash,
         "branch": $block_hash,
         "contents": [ $operation.alpha.contents ... ],
         "signature": $Signature }
  $operation.alpha.contents:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2] }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/ }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/ }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ] }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass" }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash }
  $operation.alpha.internal_operation_result:
    { /* reveal */
      "kind": "reveal",
      "source": $contract_id,
      "nonce": integer ∈ [0, 2^16-1],
      "public_key": $Signature.Public_key,
      "result": $operation.alpha.operation_result.reveal }
    || { /* transaction */
         "kind": "transaction",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "result": $operation.alpha.operation_result.transaction }
    || { /* origination */
         "kind": "origination",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "result": $operation.alpha.operation_result.origination }
    || { /* delegation */
         "kind": "delegation",
         "source": $contract_id,
         "nonce": integer ∈ [0, 2^16-1],
         "delegate"?: $Signature.Public_key_hash,
         "result": $operation.alpha.operation_result.delegation }
  $operation.alpha.operation_contents_and_result:
    { /* Endorsement */
      "kind": "endorsement",
      "level": integer ∈ [-2^31-2, 2^31+2],
      "metadata":
        { "balance_updates": $operation_metadata.alpha.balance_updates,
          "delegate": $Signature.Public_key_hash,
          "slots": [ integer ∈ [0, 255] ... ] } }
    || { /* Seed_nonce_revelation */
         "kind": "seed_nonce_revelation",
         "level": integer ∈ [-2^31-2, 2^31+2],
         "nonce": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_endorsement_evidence */
         "kind": "double_endorsement_evidence",
         "op1": $inlined.endorsement,
         "op2": $inlined.endorsement,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Double_baking_evidence */
         "kind": "double_baking_evidence",
         "bh1": $block_header.alpha.full_header,
         "bh2": $block_header.alpha.full_header,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Activate_account */
         "kind": "activate_account",
         "pkh": $Ed25519.Public_key_hash,
         "secret": /^[a-zA-Z0-9]+$/,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates } }
    || { /* Proposals */
         "kind": "proposals",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposals": [ $Protocol_hash ... ],
         "metadata": {  } }
    || { /* Ballot */
         "kind": "ballot",
         "source": $Signature.Public_key_hash,
         "period": integer ∈ [-2^31-2, 2^31+2],
         "proposal": $Protocol_hash,
         "ballot": "nay" | "yay" | "pass",
         "metadata": {  } }
    || { /* Reveal */
         "kind": "reveal",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "public_key": $Signature.Public_key,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.reveal,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Transaction */
         "kind": "transaction",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "amount": $mutez,
         "destination": $contract_id,
         "parameters"?:
           { "entrypoint": $entrypoint,
             "value": $micheline.michelson_v1.expression },
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.transaction,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Origination */
         "kind": "origination",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "balance": $mutez,
         "delegate"?: $Signature.Public_key_hash,
         "script": $scripted.contracts,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result":
               $operation.alpha.operation_result.origination,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
    || { /* Delegation */
         "kind": "delegation",
         "source": $Signature.Public_key_hash,
         "fee": $mutez,
         "counter": $positive_bignum,
         "gas_limit": $positive_bignum,
         "storage_limit": $positive_bignum,
         "delegate"?: $Signature.Public_key_hash,
         "metadata":
           { "balance_updates": $operation_metadata.alpha.balance_updates,
             "operation_result": $operation.alpha.operation_result.delegation,
             "internal_operation_results"?:
               [ $operation.alpha.internal_operation_result ... ] } }
  $operation.alpha.operation_result.delegation:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.origination:
    { /* Applied */
      "status": "applied",
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum }
  $operation.alpha.operation_result.reveal:
    { /* Applied */
      "status": "applied",
      "consumed_gas"?: $bignum }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "consumed_gas"?: $bignum }
  $operation.alpha.operation_result.transaction:
    { /* Applied */
      "status": "applied",
      "storage"?: $micheline.michelson_v1.expression,
      "big_map_diff"?: $contract.big_map_diff,
      "balance_updates"?: $operation_metadata.alpha.balance_updates,
      "originated_contracts"?: [ $contract_id ... ],
      "consumed_gas"?: $bignum,
      "storage_size"?: $bignum,
      "paid_storage_size_diff"?: $bignum,
      "allocated_destination_contract"?: boolean }
    || { /* Failed */
         "status": "failed",
         "errors": [ $error ... ] }
    || { /* Skipped */
         "status": "skipped" }
    || { /* Backtracked */
         "status": "backtracked",
         "errors"?: [ $error ... ],
         "storage"?: $micheline.michelson_v1.expression,
         "big_map_diff"?: $contract.big_map_diff,
         "balance_updates"?: $operation_metadata.alpha.balance_updates,
         "originated_contracts"?: [ $contract_id ... ],
         "consumed_gas"?: $bignum,
         "storage_size"?: $bignum,
         "paid_storage_size_diff"?: $bignum,
         "allocated_destination_contract"?: boolean }
  $operation_metadata.alpha.balance_updates:
    [ { "kind": "contract",
        "contract": $contract_id,
        "change": $int64 }
      || { "kind": "freezer",
           "category": "rewards",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "fees",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 }
      || { "kind": "freezer",
           "category": "deposits",
           "delegate": $Signature.Public_key_hash,
           "cycle": integer ∈ [-2^31-2, 2^31+2],
           "change": $int64 } ... ]
  $positive_bignum:
    /* Positive big number
       Decimal representation of a positive big number */
    string
  $script_expr:
    /* A script expression ID (Base58Check-encoded) */
    $unistring
  $scripted.contracts:
    { "code": $micheline.michelson_v1.expression,
      "storage": $micheline.michelson_v1.expression }
  $timestamp.protocol:
    /* A timestamp as seen by the protocol: second-level precision, epoch
       based. */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/protocols`**

**Description**

Get the current and next protocol _\*\*_

**JSON Output**

```javascript
 { "protocol": $Protocol_hash,
    "next_protocol": $Protocol_hash,
    ... }
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/required_endorsements?[block_delay=<int64>]`**

**Description**

Get the minimum number of endorsements for a block to be valid.

Given a delay of the block's timestamp with respect to the minimum time to bake at the block's priority.

Optional query arguments :

* block\_delay = &lt;int64&gt;

**JSON Output**

```javascript
 integer ∈ [-2^30-2, 2^30+2]
```

## Votes

### **`GET ../<block_id>/votes/ballot_list`**

**Description**

Get ballots cast so far during a voting period _\*\*_

**JSON Output**

```javascript
  [ { "pkh": $Signature.Public_key_hash,
      "ballot": "nay" | "yay" | "pass" } ... ]
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/votes/ballots`**

**Description**

Get sum of ballots cast so far during a voting period _\*\*_

**JSON Output**

```javascript
  { "yay": integer ∈ [-2^31-2, 2^31+2],
    "nay": integer ∈ [-2^31-2, 2^31+2],
    "pass": integer ∈ [-2^31-2, 2^31+2] }
```

### **`GET ../<block_id>/votes/current_period_kind`**

**Description**

Get current period kind _\*\*_

**JSON Output**

```javascript
  "proposal" || "testing_vote" || "testing" || "promotion_vote"
```

### **`GET ../<block_id>/votes/current_proposal`**

**Description**

Get current proposal under evaluation _\*\*_

**JSON Output**

```javascript
  $Protocol_hash /* Some */ || null /* None */
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/votes/current_quorum`**

**Description**

Get current expected quorum _\*\*_

**JSON Output**

```javascript
  integer ∈ [-2^31-2, 2^31+2]
```

### **`GET ../<block_id>/votes/listings`**

**Description**

Get the list of delegates with their voting weight, in number of rolls _\*\*_

**JSON Output**

```javascript
  [ { "pkh": $Signature.Public_key_hash,
      "rolls": integer ∈ [-2^31-2, 2^31+2] } ... ]
  $Signature.Public_key_hash:
    /* A Ed25519, Secp256k1, or P256 public key hash (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET ../<block_id>/votes/proposals`**

**Description**

Get the list of proposals with number of supporters _\*\*_

**JSON Output**

```javascript
  [ [ $Protocol_hash, integer ∈ [-2^31-2, 2^31+2] ] ... ]
  $Protocol_hash:
    /* A Tezos protocol ID (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

