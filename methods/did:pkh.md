# did:pkh

The [Public Key Hash DID method](https://github.com/w3c-ccg/did-pkh/blob/main/did-pkh-method-draft.md) encoding uses CAIP-2 and CAIP-10 to uniquely identify blockchain account IDs.

## Method Multicodec

`0xca`

## CAIP-2 Encodings
    
| CAIP-2 Namespace | Integer Code | CAIP-2 Reference Length | CAIP-2 Reference Encoding | Account ID Length  | Account ID Encoding    |
|:-----------------|:-------------|:------------------------|:--------------------------|--------------------|------------------------|
| bip122           | 0x01         | 32 [^fn1]               | bytes                     | 25 [^fn2]          | bytes                  |
| eip155           | 0x02         | Varint-prefixed [^fn3]  | utf-8 bytes               | 20 [^fn4]          | bytes                  |
| cosmos           | 0x03         | Varint-prefixed         | utf-8 bytes               | 20 or 32[^fn5]     | bytes, varint-prefixed |
| starknet         | 0x04         | Varint-prefixed         | utf-8 bytes               | 20 [^fn6]          | bytes                  |
| hedera           | 0x05         | Varint-prefixed         | utf-8 bytes               | 20, 32 or 33[^fn7] | bytes, varint-prefixed |
| lip9             | 0x06         | 32 [^fn8]               | bytes                     | 20 [^fn9]          | bytes                  |

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

## Notes

### Cosmos

Cosmos supports both `secp256k1` and `secp256r1` key types. In the case of `secp256k1`, the address is 20 bytes created from a hash of the public key, while `secp256r1` uses the public key itself as the address. Thus the varint prefix of the account ID encoding acts as a discriminant between address types:

* 20: Secp256k1 public key hash
* 32: Secp256r1 public key

### Hedera Hashgraph

Hedera Hashgraph supports several address representations, however only the [public key account alias](https://docs.hedera.com/hedera/core-concepts/accounts/account-properties#public-key-account-alias) and the [EVM account alias](https://docs.hedera.com/hedera/core-concepts/accounts/account-properties#evm-address-account-alias) are supported by `did:pkh`. They are represented here without shard and realm numbers. Similarly to cosmos, this allows the varint prefix account ID encoding to act as a discriminant between address types:

* 20: EVM account alias
* 32: Ed25519 Public Key account alias
* 33: Secp256k1 Public Key account alias

## References

[^fn1]: [bip-122](https://github.com/bitcoin/bips/blob/master/bip-0122.mediawiki#definition-of-chain-id)
[^fn2]: [BTC Address generation](https://en.bitcoin.it/wiki/Technical_background_of_version_1_Bitcoin_addresses)
[^fn3]: [Ethereum Chain IDs](https://chainid.network)
[^fn4]: [Ethereum Account Creation](https://ethereum.org/en/developers/docs/accounts/#account-creation)
[^fn5]: [Cosmos Accounts](https://docs.cosmos.network/v0.46/basics/accounts.html)
[^fn6]: [Starknet Contract Addresses](https://docs.starknet.io/documentation/architecture_and_concepts/Contracts/contract-address/)
[^fn7]: [Hedera Address Derivation](https://docs.hedera.com/hedera/core-concepts/accounts/account-properties)
[^fn8]: [LIP-0009](https://github.com/LiskHQ/lips/blob/main/proposals/lip-0009.md)
[^fn9]: [Lisk Addresses](https://lisk.com/documentation/understand-blockchain/lisk-protocol/accounts.html#address)
