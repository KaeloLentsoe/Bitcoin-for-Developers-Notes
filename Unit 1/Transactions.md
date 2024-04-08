# Bitcoin transactions

Very understandably, given the name, when people visualize the Bitcoin network, they often picture individual coins moving around a network. However, when you dig into the software, you'll find that the concept of individual coins does not exist in the Bitcoin protocol. What exists is software that helps the network manage a shared ledger, the blockchain. It's a ledger that keeps track of the inputs and outputs of transactions. The unit that the software calculates transactions in is what has become known as a "satoshi," which is one hundred millionth (0.00000001) of what we generally think of as a Bitcoin.

![transaction](/Unit%201/how-do-bitcoin-transaction-work.webp)

This part covers transactions and starts by explaining transaction inputs and outputs, and unspent transaction outputs, or UTXOs.

## Introduction

Transactions are the cornerstone of the Bitcoin system. Everything else in Bitcoin is designed to ensure that transactions can be created, propagated on the network, validated, and finally added to the global ledger of transactions, known as the blockchain. 

Transactions are data structures that encode the transfer of value between participants in the Bitcoin system. Each transaction represents a public entry in Bitcoin's blockchain, which serves as the global double-entry bookkeeping ledger.

Let's examine all the various forms of transactions, what they contain, how to create them, how they are verified, and how they become part of the permanent record of all transactions. When we use the term "wallet" in this chapter, we are referring to the software that constructs transactions, not just the database of keys.

### Transactions in Detail
The block explorer application displays a transaction from Alice's "address" to Bob's "address." However, this representation provides a greatly simplified view of what is contained within a transaction.

**Figure 1. Alice's transaction to Bob's Cafe**
[trans](/Unit%201/trans....png)


### Transactions - Behind the Scenes
Behind the scenes, an actual transaction looks very different from what is displayed by a typical block explorer. In fact, many of the high-level constructs we see in various Bitcoin application user interfaces do not exist in the Bitcoin system itself.

Using Bitcoin Core's command-line interface (`getrawtransaction` and `decoderawtransaction`), we can retrieve Alice's "raw" transaction, decode it, and examine its contents. The result might look something like this:

```
Alice's transaction decoded:
```

```
{
  "txid": "abcdef123456...",
  "version": 1,
  "locktime": 0,
  "vin": [
    {
      "txid": "abc123...",
      "vout": 0,
      "scriptSig": {
        "asm": "3045022100...",
        "hex": "..."
      },
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 0.001,
      "n": 0,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160...",
        "hex": "..."
      }
    },
    {
      "value": 0.003,
      "n": 1,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160...",
        "hex": "..."
      }
    }
  ]
}
```

This raw transaction data reveals detailed information such as transaction IDs (`txid`), version numbers, locktimes, input (`vin`) and output (`vout`) details, script signatures (`scriptSig`), and script public keys (`scriptPubKey`).

This process allows us to access the raw data of the transaction and understand its true structure and content.