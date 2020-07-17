# Stingy spammer attack

Isthmus / Mitchell 2020-07-13


## Description 
The stingy spammer attack is an inexpensive way to bloat privacy coins that meet two criteria:
-  The protocol accepts transactions with `fee=0`
-  The protocol does not verify that `sum(inputs)>0`

Privacy protocols typically allow the creation of dummy outputs that contain no value. Due to encrypted transaction amounts, an outside observer cannot distinguish between value-bearing versus 0-value outputs.

A stingy spammer creates 0-value/0-fee transactions to waste space on the blockchain. Suppose a protocol allows `N` outputs per transaction, the attacker uses a single dummy output to create a 1-in/N-out transaction, then uses those `N` outputs to create `N` 1-in/N-out transactions. After `F` cycles of  then the amount of space wasted is approximately `(size of 1-in/N-out transaction)*N^F`


## Notes
Whether or not this is a practical concern largely depends on whether the commonly-used transaction selection algorithms (solo and/or pool) will include the 0-fee transactions. In some ecosystems, these 0-fee transactions may be valid, but not relayed by nodes, in which case the stingy spammer may need to enumerate the p2p network and flood transactions to peers, to bypass this.

## Examples
### Zcash proof of concept
In response to my [Zcash forum post](https://forum.zcashcommunity.com/t/possible-to-generate-a-transaction-with-0-zec/36826) about zero value transactions, community member @dontpanicburns created this 1-in/2-out/0-fee/0-value example transaction: [b30fbafb6282698bbb4eaedf39d30fc185d1da26d23831bee514ae2fec4f8c80](https://explorer.zcashfr.io/insight/tx/b30fbafb6282698bbb4eaedf39d30fc185d1da26d23831bee514ae2fec4f8c80)
