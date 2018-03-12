## Summary of different payment channel proposals

#### Common concepts

* _Limiting transaction publish and/or output spends._
Transaction publish is limited through the use of nLockTime to ensure that a redeem transaction can only be added to a block after channel close.
CheckLockTimeVerify (CLTV) is used to enforce output spends at a certain absolute height or time.
CheckSequenceVerify (CSV) is used to encumber an output and prevent it from being spent during a relative period (revocation or challenge period).
* _Revocation spends._


#### Useful links

[Payment channels - Bitcoin Wiki](https://en.bitcoin.it/wiki/Payment_channels)

[Channel malleability - SO](https://bitcoin.stackexchange.com/questions/48243/are-micropayment-channels-still-subject-to-malleability-after-bip65#48546)

[BIP-65 CLTV](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki)

[BIP-68 Relative lock time](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki)

Channels on Bitcoin Magazine for diagrams [one](https://bitcoinmagazine.com/articles/understanding-the-lightning-network-part-building-a-bidirectional-payment-channel-1464710791/) [two](https://bitcoinmagazine.com/articles/understanding-the-lightning-network-part-creating-the-network-1465326903/) [three](https://bitcoinmagazine.com/articles/understanding-the-lightning-network-part-completing-the-puzzle-and-closing-the-channel-1466178980/)

_This repo uses markdown with embedded mermaid that isn't fully support on Github_

A few options for rendering:

* Atom + Markdown Preview Enhanced
* [Mermaid live editor](https://mermaidjs.github.io/mermaid-live-editor/)
