##### CheckLockTimeVerify channel

* Unidirectional from Alice to Bob
* Required CLTV (BIP-65)
* Sidesteps malleability using p2sh address
* Requires negotiation of refund timeout

```mermaid
sequenceDiagram
  participant A as Alice
  participant B as Bob
  participant C as Chain
  Note over A,C: Channel Create
  A->>A: Generate K1
  Note right of A: K1 is Alice's half of the multi-sig
  A->>+B: Request K2
  B->>-A: K2
  Note right of B: K2 is Bob's part of the multi-sig
  A->>A: Generate p2sh address (P1) and funding transaction into P1 (T1)
  Note right of A: P1 p2sh is K1 & K2 sign OR K1 after refund time
  A->>C: Broadcast T1

  Note over A,C: Channel Opened

  loop Make payments
    A->>A: Generate & sign T2 payment from P1 to B
    A->>B: Forward T2
    B->>B: Verify & Hold Updated T2
  end

  Note over A,C: Channel Close
  B->>C: Sign & Broadcast Latest T2
```

##### A1 p2sh formats

\#1
```
IF
    2 <Alice's pubkey> <Bob's pubkey> 2 CHECKMULTISIG
ELSE
    <now + refund timeout> CHECKLOCKTIMEVERIFY DROP
    <Alice's pubkey> CHECKSIG
ENDIF

OP_IF
    OP_2
    '[029bb30cc09bfbd126c7ca3f18e9f4d8ee0da727254490546b7278aab3fd76cfdf]' '[03e7e7c9ecbd81dfadb96c6f6e442b42e4492dc998e19e626fafd278eb65647aab]'
    OP_2
    CHECKMULTISIG
OP_ELSE
    144
    CHECKLOCKTIMEVERIFY
    DROP
    '[029bb30cc09bfbd126c7ca3f18e9f4d8ee0da727254490546b7278aab3fd76cfdf]'
    CHECKSIG
OP_ENDIF
```
