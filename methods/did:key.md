# did:key

The [Key DID method](https://w3c-ccg.github.io/did-method-key) encoding leverages the existing multicodes used by the Key DID method.

## Method multicodec

| Code   | Method identifier length (bytes)                             |
| ------ | ------------------------------------------------------------ |
| 0xe7   | 33                                                           |
| 0xea   | ?? (not part of the Key DID spec)                            |
| 0xeb   | 96                                                           |
| 0xec   | 32                                                           |
| 0xed   | 32                                                           |
| 0x1200 | 33                                                           |
| 0x1201 | 49                                                           |
| 0x1202 | 67                                                           |
| 0x1205 | 270 or 526 (see [RSA Public Key representation](https://w3c-ccg.github.io/did-method-key/#rsa-repr) for how to distinguish these two cases) |

## Format

```
<multidid-code><method-code><method-bytes><url-length><url-bytes>
```

Where:

* `multidid-code` - a varint encoding of `0xd1d`
* `method-code` - a varint encoding of one of the codes in the table above
* `method-bytes` - MUST contain exactly the number of bytes specified byte the method code
* `url-length` - a varint describing the length of the `url-bytes` parameter
* `url-bytes` - a UTF-8 encoded string representing the [DID URL parameters](https://www.w3.org/TR/did-core/#did-url-syntax)

## Examples

Displayed using base 16.

```
// did:key:z6MkiTBz1ymuepAQ4HEHYSF1H8quG5GLVVQR3djdX3mDooWp
0x9d1aed013b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2900

// did:key:z6MkiTBz1ymuepAQ4HEHYSF1H8quG5GLVVQR3djdX3mDooWp#z6MkiTBz1ymuepAQ4HEHYSF1H8quG5GLVVQR3djdX3mDooWp
0x9d1aed013b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2931237a364d6b6954427a31796d75657041513448454859534631483871754735474c5656515233646a6458336d446f6f5770

// did:key:zQ3shokFTS3brHcDQrn82RUDfCZESWL1ZdCEJwekUDPQiYBme
0x9d1ae70103874c15c7fda20e539c6e5ba573c139884c351188799f5458b4b41f7924f235cd00
```

