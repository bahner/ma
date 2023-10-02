# DIDDocument

The DIDDocument is a [DID Core][did-core] document that contains the public key of the entity. It *does not* use JSON-LD for parsing, but it is a JSON document.

When linked data is needed IPLD will be used. This is not applicable for the DID Document itself in relation to the DID Core spec. The document might have extended attributes, but that should be handled as part of this spec which is solely for the purpose of message passing.

[Go-間] is a  reference implementation of this spec and it is used for message passing. It is not a general purpose DID implementation, even though you should be able to use it as such for the .

## Context

The context is the following:

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1"
    ]
}
```

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

The identifier is defined in the neighbouring [DID] spec.

## Controller

The controller is the same as the identifier. You are free to add more controllers.

## [VerificationMethod]

The supported VerificationMethod  `Multikey`

`Multikey` is a verification method that is used to carry a multicodec encoded public key, which is further multibase encoded.

The key is first Multicodec encoded, then multibase encoded. The Multicodec is used to identify the key type and the multibase is used to encode the key.

This is a bit of a moving target in the DID specs, as they are catching up.

### [PublicKeyMultibase]

The base is `base58btc`. While this is not a requirement, it is the default for [DID Core][PublicKeyMultibase] and is used for all multibase encoded data.

### Multicodec

All keys are prefixed with a bytecode according to the [Multicodec spec][multicodecspec]. This is used to identify the key type. The Multicodec is encoded as a varint.

### Key types

Only very modern keys are used. They are well enough implemented and are the most secure keys available.We need keys which work fast, as we are using them for encryption and signing in real time.

#### Signing keys

An ed25519 public key encoded acoording Multicodec format "[ed25519-pub][multicodec]". This is the standard format for ed25519 public keys.

The key is encoded as a 32 byte sequence.

#### Encryption

Either an X25519 or X448 key encoded according to Multicodec format "[x25519-pub][multicodec]" or "[x448-pub][multicodec]". This is the standard format for X25519 and X448 public keys. The keys are encoded as a 32 or 56 byte sequence respectively.

X448 is considered to be very safe, but X25519 should be safe enough for our purposes.

### Rekeying

You may rekey as you see fit. Messaging actors should not rely on key persistence, even if implementers might. They should then create their DIDDocuments accordingly. Multiple keys are supported and can be used for verification. This is standard DID practice.

[did-core]: <https://www.w3.org/TR/did-core/> "Decentralized Identifiers (DIDs) v1.0"
[DID]: <./DID.md> "DID"
[multicodec]: <https://github.com/multiformats/multicodec/blob/master/table.csv> "Multicodec table"
[multicodecspec]: <https://github.com/multiformats/multicodec> "Multicodec spec"
[PublicKeyMultibase]: <https://www.w3.org/TR/did-core/#dfn-publickeymultibase> "PublicKeyMultibase in DID Core"
[Go-間]: <https://github.com/bahner/go-ma/> "Go-間 DID Document implementation"
[VerificationMethod]: <https://www.w3.org/TR/did-core/#verification-methods> "VerificationMethod in DID Core"
