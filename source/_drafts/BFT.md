### bft algorithm
1. the practical aspect is that a stable leader can drive a consensus decision in just two rounds of message exchanges.
> the pre-prepare and prepare phase decide sequence order within a view.
  the prepare and commit phase decide liveness

2. authenticator complexity
an  authenticator is either a partial signature or a signature.
> a. like bit complexity and unlike message complexity, it hides unneccessary details about the transmission topology. for example, n messages carrying one authenticator count the same as one message carrying n authenticators.
 b. authenticator complexity is better suited than bit complexity for capturing costs in protocals like ours that reach consensus repeatedly, where each consensus decision(or each view proposed on the way to that consensus decision) is identified by a monotonically increasing counter.
 c. in practice, crypographic operations to produce or verify digital signatures and to produce or combine partial signatures are the most computationally intensive operations in protocols.

### pbft(pratical bft)

#### two requirement
1. deterministic
2. must start in the same state

#### practical aspect
1. a stable leader can drive a consensus decision in just two rounds of message exchanges.

#### all the procedure
1. client request
`<request, o, t, c>sig_c`

t: timestamp
o: operation
c: the client
sig_c: the client signature


2. the reply
`<reply, v, t, c, i, r>sig_r`

v: current view
t: timestamp
c: the client
i: the replica number
r: the result of operation execution
sig_r: the replica signature

3. three phase protocal
- The pre-prepare and prepare phases are used to totally order requests sent in the same view even when the primary,
which proposes the ordering of requests, is faulty.
- The prepare and commit phases are used to ensure that requests that commit are totally ordered across views

- h and H = h + k,  sequence number should between [h, H]

- pre-prepare
`<<pre-prepare, v, n, d>sig_p, m>`

v: the view
n: sequence number
d: message digest
m: client request message
sig_p: primary signature

- prepare
`<prepare, v, n, d, i>sig_backup`

i: backup i

- commit
`<commit, v, n, D(m), i>sig_backup`

- stable checkpoint
`<checkpoint, n, d, i>sig_i`

n: sequence number
d: the digest of the checkpoint state

The low-water mark is equal to the sequence number of the last stable checkpoint. The high
water mark , where is big enough so that replicas do not stall waiting for a checkpoint to become stable.

#### view-change complexity
commonly O(n^4), using threshold signature, it's O(n^3)

[current bft algorithm complexity](/images/2022/bft_algorithm_complexity.png)

- view-change message
`<view-change, v+1, n, C, P, i>sig_i`
> n is the sequence number of last stable checkpoint s known to i
  C is a set of 2f+1 valid checkpoint message proving the correctness of s
  P is a set of request m with sequence higher than n.

- new-view message
`<new-view, v+1, V, Q>sig_primary`
> V is a set containing the valid view-change message
  Q is a set of pre-prepare messages


### hotstuff

#### feature
1. the cost for a new leader to drive the protocol to consensus is no greater than that for the current leader.
2. implement linear view change.

### problem
1. the crux of the difficulty is that there maybe exist an honest replica that has the highest QC, but the leader does not known about it.

#### basic
- messages
<m.type, m.viewNumber, m.node, m.justify>[ m.partialSig]
m.type: {NEW-VIEW, PREPARE, PRE-COMMIT, COMMIT, DECIDE}

- m.justify
QC: <type, viewNumber, node>


1. lockedQC: store the highest QC for viewchange, always pre-committed qc.
