### structure 

1. tangle -> DAG where vertices represent transactions, and edges represent approvals.
2. If there is an edge from A to B, we say that "A approves B". When a node issues a new transaction, it must choose 2 previous ones to approve, thereby adding 2 new edges to the graph.
3. If there is some directed path from A to B, we say that that A references B.
4. All the IOTA tokens were created in the genesis, and no new ones will ever be created. 

### some defination

1. genesis: the first transaction in tangle.
2. tip: the transacton with no approval
3. own weight: a property related to a  transaction
4. cumulative weight: own weight puls all the weights approved or directly approved  transactions
4. minimum weight magnitude(mwm): the difficulty of pow; (iota v1.4, the mwm in mainnet is 14, testnet is 9)
5. snapshot: it is a method to reduce the size of the Tangle database by removing all the transactions from tangle, leaving only a record of addresses with corresponding balances. Addresses with zero balances also removed from this record.
6. latestmilestone: the latest milestone produced by coordinator
7. latestSolidSubtangleMilestone: all the apporved transactions is direct or indirect referenced by  the subtangle

### consensus on IOTA  --- by coordiator

1. coordinator is an entity controlled by IOTA Foundation. which issue zero-valued transactiono every-two-minutes, calld milestone.
2. any transactions referenced by milestone is confirmed, and others is not.


### bundles

1. There are no hard constraints on the number of inputs and outputs in a bundle. However given the networking and PoW contraints bundles over 30 inputs/outputs are not advised.
2. the amount is a negative integer in input, which means take token from this address



 
### synchronization

a node is synchronised when
1. the latestMilestoneIndex is updated to the actual last milestone index validated by the coordinator
2. the latestSolidSubtangleMilestoneIndex is the same as the lastMilestoneIndex.

### transaction

1. a transaction is  2673 trytes (about 1.55 kbytes)

### seed & private keys & address

1. addresses: generate from seed and key index; max key index allowed is 2^53 - 1  (about 9 * 10^15).