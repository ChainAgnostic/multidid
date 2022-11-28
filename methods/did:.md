# did:*

The "any" DID method encoding allows any DID to be represented as a MultiDID by essentially putting the entire DID string in the URL portion of the multidid byte string.

## Method multicodec

`0x00`

## Format

```
<multicodec-did><method-multicodec><method-bytes><url-length><url-bytes>
```

Where:

* `multicodec-did` - the value `0xd1d`
* `method-multicodec` - a varint encoding of `0x00`
* `method-bytes` - MUST contain exactly zero bytes
* `url-length` - a varint describing the length of the `url-bytes` parameter
* `url-bytes` - a UTF-8 encoded string representing the DID and URL component (e.g. everything except `did:`)

## Examples

Displayed using base 16.

```
// did:example:123456
0x0d1d000e6578616d706c653a313233343536

// did:example:123456?versionId=1
0x0d1d001a6578616d706c653a3132333435363f76657273696f6e49643d31
```
