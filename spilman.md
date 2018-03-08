Spilman payment channels [original source](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2013-April/002433.html)

* Unidirectional from Alice to Bob
* Expects to use nSequence
* Affected by malleability

```mermaid
sequenceDiagram
  participant A as Alice
  participant B as Bob
  participant C as Chain
  Note over A,C: Channel Create
  A->>A: Generate K1
  Note right of A: K1 is Alice's side of the channel
  A->>+B: Request K2
  B->>-A: K2
  Note right of B: K2 is Bob's part of the channel
  A->>A: Generate Funding transaction (T1)
  A->>A: Generate Refund transaction (T2)
  Note right of A: T2 uses nLockTime to prevent premature broadcast
  A->>+B: Request to sign Refund (T2)
  B->>-A: Signed Refund (T2)
  A->>B: Signed T1
  B->>C: Broadcast T1
  Note right of B: This allows B to confirm the transaction
  Note over A,C: Channel Opened

  Note over A,B: Make payments
  A->>A: Generate T3 based off T1 output
  A->>B: Send T3
  B->>B: Verify & Hold T3
  loop Make updates
    A->>A: Increase payment & re-sign
    A->>B: Send payment increase & signature
    B->>B: Verify & Hold Updated T3
  end

  Note over A,C: Channel Close
  B->>C: Sign & Broadcast Latest T3
```
