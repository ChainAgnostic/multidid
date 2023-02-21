# multidid

> A very compact representation of DIDs and DID URLs

Multidid is a representation strategy for DIDs and DID URLs that is very compact and extensible. It allows any DID method to be represented as a string of bytes.

## Format

```
<multidid-code><method-code><method-bytes><url-length><url-bytes>
```

Where:

* `multidid-code` - the value `0x0d1d` encoded as a 
  [multiformats varint][]
* `method-code` - a varint encoded multicode for the [DID
  Method](https://www.w3.org/TR/did-core/#a-simple-example)
* `method-bytes` - data representing the method-id
* `url-length` - a varint describing the length of the `url-bytes` parameter
* `url-bytes` - a *UTF-8* encoded string representing the [DID URL parameters](https://www.w3.org/TR/did-core/#did-url-syntax)

## Method multicodes

By default any DID method can be represented using the `0x55` code as the `method-code`. Any DID method can add an additional, more optimized, representation by submitting a specification to the `methods` folder in this repository, claiming a prefix in the [multicodec table](https://github.com/multiformats/multicodec/blob/master/table.csv), and adding it to the method table below.

### Method specific identifier length

The main constraint of all specific `method-multicodec`'s is that given a code, the length of the method specific identifier, the `method-bytes`, MUST be known. Otherwise it would be impossible to know when to start parsing the `url-bytes`.

### Registered method multicodes

| Code                                                   | Method                          |
| ------------------------------------------------------ | ------------------------------- |
| 0x55                                                   | [did:*](./methods/did:.md)      |
| 0xe7, 0xeb, 0xec, 0xed, 0x1200, 0x1201, 0x1202, 0x1205 | [did:key](./methods/did:key.md) |
| 0xca                                                   | did:pkh                         |

## Editors

* [Joel Thorstensson](https://github.com/oed), [3Box Labs](https://3boxlabs.com/)
* [Juan Caballero](https://github.com/bumblefudge), [CASA](https://github.com/chainAgnostic/CASA)

## Authors

* [Irakli Gozalishvili](https://github.com/Gozala), [DAG House](https://dag.house/)
* [Joel Thorstensson](https://github.com/oed), [3Box Labs](https://3boxlabs.com/)

## References

[multiformats varint]: https://github.com/multiformats/unsigned-varint