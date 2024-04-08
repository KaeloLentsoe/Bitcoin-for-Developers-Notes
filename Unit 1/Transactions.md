# Bitcoin transactions

Very understandably, given the name, when people visualize the Bitcoin network, they often picture individual coins moving around a network. However, when you dig into the software, you'll find that the concept of individual coins does not exist in the Bitcoin protocol. What exists is software that helps the network manage a shared ledger, the blockchain. It's a ledger that keeps track of the inputs and outputs of transactions. The unit that the software calculates transactions in is what has become known as a "satoshi," which is one hundred millionth (0.00000001) of what we generally think of as a Bitcoin.

![transaction](/how-do-bitcoin-transaction-work.webp)

This part covers transactions and starts by explaining transaction inputs and outputs, and unspent transaction outputs, or UTXOs.

## Introduction

Transactions are the cornerstone of the Bitcoin system. Everything else in Bitcoin is designed to ensure that transactions can be created, propagated on the network, validated, and finally added to the global ledger of transactions, known as the blockchain. Transactions are data structures that encode the transfer of value between participants in the Bitcoin system. Each transaction represents a public entry in Bitcoin's blockchain, which serves as the global double-entry bookkeeping ledger.
Let's examine all the various forms of transactions, what they contain, how to create them, how they are verified, and how they become part of the permanent record of all transactions. When we use the term "wallet" in this chapter, we are referring to the software that constructs transactions, not just the database of keys.