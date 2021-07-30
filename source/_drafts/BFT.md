 
### pbft

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


### hotstuff

#### feature 
1. the cost for a new leader to drive the protocol to consensus is no greater than that for the current leader.


#### basic 
1. lockedQC: store the highest QC for 
