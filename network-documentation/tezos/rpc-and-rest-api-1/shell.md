---
description: Learn how to interact with the Tezos RPC
---

# Shell

## Chain Info

### **`PATCH /chains/<chain_id>`**

**Description**

Forcefully set the bootstrapped flag of the node _\*\*_

**JSON Output**

```javascript
  any
```

### **`GET /chains/<chain_id>/blocks?[length=<int>]&(head=<block_hash>)*&[min_date=<date>]`**

**Description**

List block hashes from '', up to the last checkpoint, sorted with decreasing fitness.

Without arguments it returns the head of the chain. Optional arguments allow to return the list of predecessors of a given block or of a set of blocks.

Optional query arguments :

* length = &lt;int&gt; : The requested number of predecessors to return \(per request; see next argument\).
* head = &lt;block\_hash&gt; : An empty argument requests blocks starting with the current head. A non empty list allows to request one or more specific fragments of the chain.
* min\_date = &lt;date&gt; : When \`min\_date\` is provided, blocks with a timestamp before \`min\_date\` are filtered out

**JSON Output**

```javascript
  [ [ $block_hash ... ] ... ]
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### `GET /chains/<chain_id>/chain_id`

**Description**

Get the chain unique identifier

**JSON Output**

```javascript
  $Chain_id
  $Chain_id:
    /* Network identifier (Base58Check-encoded) */
    $unistring
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET /chains/<chain_id>/checkpoint`**

**Description**

Get the current checkpoint for this chain _\*\*_

**JSON Output**

```javascript
  { "block": $block_header,
    "save_point": integer ∈ [-2^31-2, 2^31+2],
    "caboose": integer ∈ [-2^31-2, 2^31+2],
    "history_mode": "full" | "archive" | "rolling" }
  $Context_hash:
    /* A hash of context (Base58Check-encoded) */
    $unistring
  $Operation_list_list_hash:
    /* A list of list of operations (Base58Check-encoded) */
    $unistring
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $block_header:
    /* Block header
       Block header. It contains both shell and protocol specific data. */
    { "level": integer ∈ [-2^31-2, 2^31+2],
      "proto": integer ∈ [0, 255],
      "predecessor": $block_hash,
      "timestamp": $timestamp.protocol,
      "validation_pass": integer ∈ [0, 255],
      "operations_hash": $Operation_list_list_hash,
      "fitness": $fitness,
      "context": $Context_hash,
      "protocol_data": /^[a-zA-Z0-9]+$/ }
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

### **`GET /chains/<chain_id>/invalid_blocks`**

**Description**

List blocks that have been declared invalid along with the errors that led to them being declared invalid

**JSON Output**

```javascript
  [ { "block": $block_hash,
      "level": integer ∈ [-2^31-2, 2^31+2],
      "errors": $error } ... ]
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $error:
    /* The full list of error is available with the global RPC `GET errors` */
    any
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`GET /chains/<chain_id>/invalid_blocks/<block_hash>`**

**Description**

Get the errors that appear during the block \(in\)validation

**JSON Output**

```javascript
  { "block": $block_hash,
    "level": integer ∈ [-2^31-2, 2^31+2],
    "errors": $error }
  $block_hash:
    /* A block identifier (Base58Check-encoded) */
    $unistring
  $error:
    /* The full list of error is available with the global RPC `GET errors` */
    any
  $unistring:
    /* Universal string representation
       Either a plain UTF8 string, or a sequence of bytes for strings that
       contain invalid byte sequences. */
    string || { "invalid_utf8_string": [ integer ∈ [0, 255] ... ] }
```

### **`DELETE /chains/<chain_id>/invalid_blocks/<block_hash>`**

**Description**

Remove an invalid block for the Tezos storage _\*\*_

**JSON Output**

```javascript
  {  }
```

### **`GET /chains/<chain_id>/is_bootstrapped`**

**Description**

Get the bootstrap status of a chain _\*\*_

**JSON Output**

```javascript
  { "bootstrapped": boolean,
    "sync_state": "sync" | "stuck" | "unsync" }
```

