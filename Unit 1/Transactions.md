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

![trans](/Unit%201/trans....png)


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


# Transaction Outputs and Inputs
Bitcoin transactions are built upon transaction outputs, which are discrete units of bitcoin currency recorded on the blockchain and universally recognized by the network. Nodes in the Bitcoin network keep track of all spendable outputs, known as Unspent Transaction Outputs (UTXO), which form the UTXO set. This set continually changes as new outputs are created and spent. Each transaction represents a change in this UTXO set.

When a user's wallet "receives" bitcoin, it means the wallet has detected a UTXO on the blockchain that it can spend with its controlled keys. The wallet's bitcoin "balance" is the sum of all spendable UTXO associated with the wallet, scattered across multiple transactions and blocks. Wallet applications calculate this balance by scanning the blockchain and aggregating the value of spendable UTXO. Most wallets maintain a database for quick reference of these spendable UTXO.

As transactions are built on the blockchain, they spend UTXO created by previous transactions, turning them into Spent Transaction Outputs (STXO). If a transaction creates change outputs, the UTXO set size increases. For instance, if a transaction spends one UTXO and creates two new ones (payment and change), it increases the UTXO set size by one.

**Figure 2. Transaction chain from Joe to Gopesh being built on the blockchain**
![UTXO & STXO](/Unit%201/Utxo.png)

A Bitcoin transaction output holds a value in satoshis, divisible down to eight decimal places. Once created, an output cannot be divided further. This means if a transaction output is larger than needed, it must be spent entirely, generating change.

For instance, if you have a 20-bitcoin output but only need to pay 1 bitcoin, the entire 20-bitcoin output must be spent. This creates two outputs: one for the payment and another for the change back to your wallet. Most transactions generate change due to this indivisible nature.

This process mirrors real-life scenarios where people pay with exact change or larger denominations, receiving change back. Similarly, Bitcoin transactions use available outputs to meet the transaction amount. The wallet selects outputs automatically, combining smaller units or using larger ones as needed.

Transactions consume previous unspent outputs and create new ones, facilitating the transfer of bitcoin value. However, the first transaction in each block, called the coinbase transaction, is unique. It's created by the winning miner and generates new bitcoin as a mining reward, without consuming previous outputs. This is how new bitcoin enters circulation during mining.

# Transaction Outputs