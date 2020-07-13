# Stingy Spammer attack

The stingy spammer attack is an inexpensive way to bloat privacy coins that meet two criteria:
-  The protocol accepts transactions with `fee=0`
-  The protocol does not verify that `sum(inputs)>0`

Privacy protocols typically allow the creation of dummy outputs that contain no value. Due to encrypted transaction amounts, an outside observer cannot distinguish between value-bearing versus 0-value outputs.

A stingy spammer creates 0-value/0-fee transactions to waste space on the blockchain. Suppose a protocol allows `N` outputs per transaction, the attacker uses a single dummy output to create a 1-in/N-out transaction, then uses those `N` outputs to create `N` 1-in/N-out transactions. After `F` cycles of  then the amount of space wasted is approximately `(size of 1-in/N-out transaction)*N^F`

Whether or not this is a practical concern largely depends on whether the commonly-used transaction selection algorithms (solo and/or pool) will include the 0-fee transactions. In some ecosystems, these 0-fee transactions may be valid, but not relayed by nodes, in which case the stingy spammer may need to enumerate the p2p network and flood transactions to peers, to bypass this.
