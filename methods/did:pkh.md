# did:pkh

The [Public Key Hash DID method](https://github.com/w3c-ccg/did-pkh/blob/main/did-pkh-method-draft.md) encoding uses CAIP-2 and CAIP-10 to uniquely identify blockchain account IDs.

## Method Multicodec

`0xca`

## CAIP-2 Encodings

| CAIP-2 Namespace | Integer Code | CAIP-2 Reference Length | CAIP-2 Reference Encoding | Account ID Length | Account ID Encoding |
|:-----------------|:-------------|:------------------------|:--------------------------|-------------------|---------------------|
| bip122           | 0x01         | 32 [^fn1]               | bytes                     | 25 [^fn2]         | bytes               |
| eip155           | 0x02         | Varint-prefixed [^fn3]  | utf-8 bytes               | 20 [^fn4]         | bytes               |
| cosmos           | 0x03         | Varint-prefixed         | utf-8 bytes               | [^fn5]            | bytes               |
| starknet         | 0x04         | Varint-prefixed         | utf-8 bytes               | 20 [^fn6]         | bytes               |
| hedera           | 0x05         | Varint-prefixed         | utf-8 bytes               | Variable          | 3 Varints [^fn7]    |
| lip9             | 0x06         | 32 [^fn8]               | bytes                     | 20 [^fn9]         | bytes               |

## Format

```
<multidid-code><method-code><caip2-namespace><caip2-ref-length?><caip2-ref><account-id><url-length><url-bytes>
```

Where:

* `multidid-code` - a varint encoding of `0xd1d`
* `method-code` - a varint encoding of `0xca`
* `caip2-namespace` - a varint encoding of the Integer Code associated with the CAIP-2 Namespace found in the table above
* `caip2-ref-length` - If the CAIP-2 Reference is not a fixed length, MUST contain the varint-encoded byte-length of the CAIP-2 Reference
* `caip2-ref` - CAIP-2 reference identifying the chain
* `account-id` - CAIP-10 account ID
* `url-length` - a varint describing the length of the `url-bytes` parameter
* `url-bytes` - a UTF-8 encoded string representing the [DID URL parameters](https://www.w3.org/TR/did-core/#did-url-syntax)

## References

[^fn1]: [bip-122](https://github.com/bitcoin/bips/blob/master/bip-0122.mediawiki#definition-of-chain-id)
[^fn2]: [BTC Address generation](https://en.bitcoin.it/wiki/Technical_background_of_version_1_Bitcoin_addresses)
[^fn3]: [Ethereum Chain IDs](https://chainid.network)
[^fn4]: [Ethereum Account Creation](https://ethereum.org/en/developers/docs/accounts/#account-creation)
[^fn5]: [Cosmos Accounts](https://docs.cosmos.network/v0.46/basics/accounts.html)
[^fn6]: [Starknet Contract Addresses](https://docs.starknet.io/documentation/architecture_and_concepts/Contracts/contract-address/)
[^fn7]: [Hedera Address Derivation](https://docs.hedera.com/hethers/application-programming-interface/utilities/addresses#derivation)
[^fn8]: [LIP-0009](https://github.com/LiskHQ/lips/blob/main/proposals/lip-0009.md)
[^fn9]: [Lisk Addresses](https://lisk.com/documentation/understand-blockchain/lisk-protocol/accounts.html#address)
