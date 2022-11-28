# multidid

> A very compact representation of DIDs and DID URLs

Multidid is a representation stategy for DIDs and DID URLs that is very compact and extensible. It allows any DID method to be represented as a byte string.

## Format

```
<multicodec-did><method-multicodec><method-bytes><url-length><url-bytes>
```

Where:

* `multicodec-did` - the value `0xd1d`
* `method-multicodec` - a varint encoded multicode for the [DID Method](https://www.w3.org/TR/did-core/#a-simple-example)
* `method-bytes` - data representing the method-id
* `url-length` - a varint describing the length of the `url-bytes` parameter
* `url-bytes` - a UTF-8 encoded string representing the [DID URL parameters](https://www.w3.org/TR/did-core/#did-url-syntax)

## Method multicodes

By default any DID method can be represented using the `0x00` code as the `method-multicodec`. Any DID method can add an additional, more optimized, representation by submitting a specification to the `methods` folder in this repo, claiming a prefix in the [multicodec table](https://github.com/multiformats/multicodec/blob/master/table.csv), and adding it to the method table below.

### Method specific identifier length

The main constraint of all specific `method-multicodec`'s is that given a code, the length of the method specific identifier, the `method-bytes`, MUST be known. Otherwise it would be impossible to know when to start parsing the `url-bytes`.

### Regsitered method multicodes

| Code                                                   | Method                          |
| ------------------------------------------------------ | ------------------------------- |
| 0x00                                                   | [did:*](./methods/did:.md)      |
| 0xe7, 0xeb, 0xec, 0xed, 0x1200, 0x1201, 0x1202, 0x1205 | [did:key](./methods/did:key.md) |
| 0xca                                                   | did:pkh                         |
