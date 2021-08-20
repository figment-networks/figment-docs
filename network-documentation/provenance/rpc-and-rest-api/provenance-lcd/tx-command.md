---
description: Submit transactions using the `provenanced` transaction command.
---

# Tx Command



{% hint style="info" %}
This section uses the `provenanced` application to connect to the Provenance testnet.  Follow the installation instructions in the [Using Provenanced ](https://docs.provenance.io/blockchain/using-provenance)section.

You will need a key pair stored in the local Keyring to run the transaction commands in this section.
{% endhint %}

### Create and Submit a Transaction

With a key pair and address we can submit transactions to the blockchain.

{% hint style="info" %}
Use `provenanced tx --help` to view the types of transactions supported by Provenance.

Transaction requests from the command-line follow the form:

```bash
provenanced tx [moduleName] [command] <arguments> --flag <flagArg>
```
{% endhint %}

First find an existing Hash holder address that we can transfer some of our Hash to.  Using the `provenanced` query commands and the Marker module, we can list everyone holding Hash:

```bash
provenanced --testnet q marker holding nhash --node=tcp://rpc-0.test.provenance.io:26657
```

```bash
balances:
- address: tp1qgjnuqnrqwhg2kfl0dk9rhkcga5lehns2hdycm
  coins:
  - amount: "963530000"
    denom: nhash
- address: tp1pr93cqdh4kfnmrknhwa87a5qrwxw9k3dhkszp0
  coins:
  - amount: "99089999999600000000"
    denom: nhash
- address: tp1pmc6v4p8rak0lmzcrsm9t2hzm9vnzwy2a5xyhv
  coins:
  - amount: "866545000"
    denom: nhash
- address: tp1zk3qvk6dvpk6394chmvq5gtrw5arqzsag072h5
```

Let's pick an account with a small amount of Hash, like the first address in our list `tp1qgjnuqnrqwhg2kfl0dk9rhkcga5lehns2hdycm` \(note, the list may be different when you run this command\).

{% hint style="info" %}
What is `nhash`?  `nhash` is the smallet unit of Hash, a nano-Hash, where 1 Hash = 1,000,000,000 `nhash`. 
{% endhint %}

Now, let's transfer 1`nhash` to the other address:

```bash
provenanced --testnet tx bank send tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs tp1qgjnuqnrqwhg2kfl0dk9rhkcga5lehns2hdycm 1nhash \
 --node=tcp://rpc-0.test.provenance.io:26657 \
 --chain-id pio-testnet-1 \
 --gas 65000 
 --gas-prices 1nhash
```

The CLI will prompt us to confirm our transaction request:

```bash
{"body":{"messages":[{"@type":"/cosmos.bank.v1beta1.MsgSend","from_address":"tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs","to_address":"tp1qgjnuqnrqwhg2kfl0dk9rhkcga5lehns2hdycm","amount":[{"denom":"nhash","amount":"1"}]}],"memo":"","timeout_height":"0","extension_options":[],"non_critical_extension_options":[]},"auth_info":{"signer_infos":[],"fee":{"amount":[{"denom":"nhash","amount":"60000"}],"gas_limit":"200000","payer":"","granter":""}},"signatures":[]}

confirm transaction before signing and broadcasting [y/N]:
```

Once confirmed, the transaction will be signed using the private key portion of our key pair associated to address `tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs` \(remember we stored our key in a local keyring\) and submitted to the blockchain:

```javascript
{
  "height": "211721",
  "txhash": "903A2DFC2E3178D4AB078306E357C28A7B6167F01181AC1A17F1CCC857202D13",
  "codespace": "",
  "code": 0,
  "data": "0A060A0473656E64",
  "raw_log": "[{\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"send\"},{\"key\":\"sender\",\"value\":\"tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs\"},{\"key\":\"module\",\"value\":\"bank\"}]},{\"type\":\"transfer\",\"attributes\":[{\"key\":\"recipient\",\"value\":\"tp1qgjnuqnrqwhg2kfl0dk9rhkcga5lehns2hdycm\"},{\"key\":\"sender\",\"value\":\"tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs\"},{\"key\":\"amount\",\"value\":\"1nhash\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "send"
            },
            {
              "key": "sender",
              "value": "tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs"
            },
            {
              "key": "module",
              "value": "bank"
            }
          ]
        },
        {
          "type": "transfer",
          "attributes": [
            {
              "key": "recipient",
              "value": "tp1qgjnuqnrqwhg2kfl0dk9rhkcga5lehns2hdycm"
            },
            {
              "key": "sender",
              "value": "tp1cuknswnphchtkwe68t4nshcaj4l4azv9ml2qhs"
            },
            {
              "key": "amount",
              "value": "1nhash"
            }
          ]
        }
      ]
    }
  ],
  "info": "",
  "gas_wanted": "65000",
  "gas_used": "61579",
  "tx": null,
  "timestamp": ""
}
```

{% hint style="info" %}
Gas, gas, and more gas: notice that the transaction response includes `gas_wanted` and a `gas_used` values.  When we submitted our transaction we indicated we were willing to pay 65,000 units of gas \(`--gas 65000`\) at 1 nhash per unit \(`--gas-prices 1nhash`\).  The actual cost of the transaction was 61,579 units of gas at our 1 nhash per unit price.  Refer to the [Cosmos Introduction to Gas and Fees](https://docs.cosmos.network/master/basics/gas-fees.html) and the [Provenance Gas and Fees](https://docs.provenance.io/blockchain/basics/gas-and-fees) section.
{% endhint %}

Responses in the transactions are:

* `height` is the block number our transaction was included in
* `txhash` is a unique identifier for our transfer transaction \(it is a crypto hash of the transaction request\)
* A zero value `code` indicates the transaction was successful.

{% hint style="info" %}
The `--node=tcp://rpc-0.test.provenance.io:26657` flag is not necessary when running against a locally installed node.
{% endhint %}

