# did:*

The "any" DID method encoding allows any DID to be represented as a multidid by essentially putting the entire DID ASCII string in the URL portion of the multidid byte string.

## Method multicodec

`0x55`

## Format

```
<multidid-code><method-code><method-bytes><url-length><url-bytes>
```

Where:

* `multidid-code` - a varint encoding of `0xd1d`
* `method-code` - a varint encoding of `0x55`
* `method-bytes` - MUST contain exactly zero bytes
* `url-length` - a varint describing the length of the `url-bytes` parameter
* `url-bytes` - a UTF-8 encoded string representing the DID and URL component (e.g. everything except `did:`)

## Examples

Displayed using base 16.

```
// did:example:123456
0x9d1a550e6578616d706c653a313233343536

// did:example:123456?versionId=1
0x9d1a551a6578616d706c653a3132333435363f76657273696f6e49643d31
```
