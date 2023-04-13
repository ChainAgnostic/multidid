# did:pkh

The [Public Key Hash DID method](https://github.com/w3c-ccg/did-pkh/blob/main/did-pkh-method-draft.md) encoding uses CAIP-2 and CAIP-10 to uniquely identify blockchain account IDs.

## Method Multicodec

`0xca`

## CAIP-2 Encodings

| CAIP-2 Namespace | Integer Code | CAIP-2 Reference Length | CAIP-2 Reference Encoding | Account ID Length | Account ID Encoding |
|:-----------------|:-------------|:------------------------|:--------------------------|-------------------|---------------------|
| bip122           | 0x01         | 32                      | bytes                     | 25                | bytes               |
| eip155           | 0x02         | Varint-prefixed         | bytes                     | 20                | bytes               |
| cosmos           | 0x03         | Varint-prefixed         | utf-8 bytes               |                   | bytes               |
| starknet         | 0x04         | Varint-prefixed         | utf-8 bytes               | 20                | bytes               |
| hedera           | 0x05         | Varint-prefixed         | utf-8 bytes               | Variable          | 3 Varints           |
| lip9             | 0x06         | 32                      | bytes                     | 20                | bytes               |

## Format

```
<multidid-code><method-code><caip2-namespace><chain-id-length?><caip2-ref><account-id><url-length><url-bytes>
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
