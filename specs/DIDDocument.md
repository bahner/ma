# DIDDocument

The DIDDocument is a [DID Core][did-core] document that contains the public key of the entity. It *does not* use JSON-LD for parsing, but it is a JSON document.

When linked data is needed IPLD will be used. This is not applicable for the DID Document itself in relation to the DID Core spec. The document might have extended attributes, but that should be handled as part of this spec which is solely for the purpose of message passing.

[Go-間] is a  reference implementation of this spec and it is used for message passing. It is not a general purpose DID implementation, even though you should be able to use it as such for simple purposes.

## Context

The context is the following:

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1"
  ]
}
```

NB! This means it's a list with only one element for now.

### Example

```json
{
  "@context": [
    "https://w3id.org/did/v1"
  ],
  "id": "did:space:k51qzi5uqu5djc9hvdmnt98yzvmxexsnzixlypjzdi9iega7d90dkes42zg3yx#bahner",
  "controller": [
    "did:space:k51qzi5uqu5djc9hvdmnt98yzvmxexsnzixlypjzdi9iega7d90dkes42zg3yx#bahner"
  ],
  "verificationMethod": [
    {
      "id": "k51qzi5uqu5djc9hvdmnt98yzvmxexsnzixlypjzdi9iega7d90dkes42zg3yx#enc-1",
      "type": "Multikey",
      "publicKeyMultibase": "zHQvVtPU4yRuoBDCT7uPXT3v8CYcFXsusB9ePZDBGNF9Z"
    },
    {
      "id": "k51qzi5uqu5djc9hvdmnt98yzvmxexsnzixlypjzdi9iega7d90dkes42zg3yx#sig-1",
      "type": "Multikey",
      "publicKeyMultibase": "z4Mt59JrpHYqrUkitUwMzhNhMtvTzgLP3SJcpBsA7GdJS"
    }
  ]
}
```

This is a normal DIDDocument according to this spec. This is what you will need and it's complete.

## Identifier

Formatting of the identifier is defined in the neighbouring [DID] spec.

## Controller

The controller is the same as the identifier. You are free to add more controllers.

## [VerificationMethod]

The keys in the VerificationMethod are the keys used for signing and encryption. The keys are encoded according to the [Multicodec spec][multicodecspec] as `PublicKeyMultiBase` keys.

The order of events is:

* Find the appropriate Multicodec code for the key type and prepend those bytes to the key.
* Multibase encode the resulting bytes with `base58btc`.

This is all fairly common and well-documented in DID Core. There is nothing special about this

### Multikey

The only supported VerificationMethod is `Multikey`.

`Multikey` is a verification method that is used to carry a multicodec encoded public key, which is further multibase encoded.

This is a [bit of a moving target in the DID specs][did-key], but the work is progressing well enough.

### [PublicKeyMultibase]

The base is `base58btc`. While this is not a requirement, it is the default for [DID Core][PublicKeyMultibase] and is used for all multibase encoded data.

### Multicodec

All keys are prefixed with a bytecode according to the [Multicodec spec][multicodecspec]. This is used to identify the key type. The Multicodec is encoded as a varint.

### Key types

Only very modern keys are used. They are well enough implemented and are the most secure keys available.We need keys which work fast, as we are using them for encryption and signing in real time.

`Multikey` all the way! The whole architecture is based on it. Since we need an IPFS daemon, the required tools are readily available. This is [not out of draft status][did-key] yet, but the spec is stable enough for our purposes.

 We do not support JSON-LD version. There's no need for it. We are using a JSON document, but we are not using JSON-LD. The spec does not block us from doing this in the future.

#### Signing keys

An ed25519 public key encoded acoording Multicodec format "[ed25519-pub][multicodec]". This is the standard format for ed25519 public keys.

The key is encoded as a 32 byte sequence.

#### Encryption

Either an X25519 or X448 key encoded according to Multicodec format "[x25519-pub][multicodec]" or "[x448-pub][multicodec]". This is the standard format for X25519 and X448 public keys. The keys are encoded as a 32 or 56 byte sequence respectively.

##### X448

X448 is considered to be very safe, but X25519 should be safe enough for our purposes.

X448 is not stamped imprimatur by W3, but I suspect it's forthcoming. By using X448 we are future proofing our encryption, but it is not formally supported. But since we are using multicodec, it shouldn't matter.

So our context doesn't have a suite spec for X448 but it should work without any problems.

If unsure, just stick with X25519. It's more than safe enough for current standards.

X448 is supported along the lines of JWK in [rfc8037], but we use it as a Multikey.

### Rekeying

You may rekey as you see fit. Messaging actors should not rely on key persistence, even if implementers might. They should then create their DIDDocuments accordingly. Multiple keys are supported and can be used for verification. This is standard DID practice.

[did-core]: <https://www.w3.org/TR/did-core/> "Decentralized Identifiers (DIDs) v1.0"
[DID]: <./DID.md> "DID"
[multicodec]: <https://github.com/multiformats/multicodec/blob/master/table.csv> "Multicodec table"
[multicodecspec]: <https://github.com/multiformats/multicodec> "Multicodec spec"
[PublicKeyMultibase]: <https://www.w3.org/TR/did-core/#dfn-publickeymultibase> "PublicKeyMultibase in DID Core"
[Go-間]: <https://github.com/bahner/go-ma/> "Go-間 DID Document implementation"
[VerificationMethod]: <https://www.w3.org/TR/did-core/#verification-methods> "VerificationMethod in DID Core"
[rfc8037]: <https://tools.ietf.org/html/rfc8037> "rfc8037"
[did-key]: <https://w3c-ccg.github.io/did-method-key/> "did-key"
