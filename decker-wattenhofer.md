##### Duplex Decker/Wattenhofer channels

* Bidirectional between Alice and Bob
* Required Relative CSV
* Uses refund transactions and requires malleability fix
* Requires negotiation of refund timeout

`
Replace by incentive: one party has multiple fully signed transactions, with different values transferred to it, of which only one may be committed. The party will commit the transaction transferring the highest amount to it.
`

##### Transaction formats

Setup transaction
```
OP_IF
  2 <Alice's pubkey> <Bob's pubkey> 2 OP_CHECKMULTISIG
OP_ELSE
  <timeout> OP_CSV
  2 <Alice's pubkey> <Bob's pubkey> 2 OP_CHECKMULTISIG
OP_ENDIF

OP_IF
    OP_2
    '[029bb30cc09bfbd126c7ca3f18e9f4d8ee0da727254490546b7278aab3fd76cfdf]' '[03e7e7c9ecbd81dfadb96c6f6e442b42e4492dc998e19e626fafd278eb65647aab]'
    OP_2
    CHECKMULTISIG
OP_ELSE
    144
    OP_CSV
    OP_2
    '[029bb30cc09bfbd126c7ca3f18e9f4d8ee0da727254490546b7278aab3fd76cfdf]' '[03e7e7c9ecbd81dfadb96c6f6e442b42e4492dc998e19e626fafd278eb65647aab]'
    OP_2
    CHECKMULTISIG
OP_ENDIF
```
