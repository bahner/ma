SPACE™ DID specs.
===

This is hopefully a NOOP document for the foreseeable future.

The intent is to keep Actor IDs in SPACE as close to the [DID spec](https://w3c.github.io/did-core/) as possible.

Actor ID
---

The actor ID is the IPNS identifier of the actor's public key. It is a [DID](https://w3c.github.io/did-core/) and can be resolved to a DID Document.

The actor ID is the only identifier that is guaranteed to be unique across all actors in the network.

We need to be able to publish RSA keys in order to be able to encrypt messages with the public key of the recipient. IPNS secret keys can't be used for this.

Method Name
---

The method name is `ipns`. This should probably be `did:ipid` or something, but we're using IPNS for now. It implies the spec for the key as defined by https://specs.ipfs.tech/ipns/ipns-record/

DID Example

```JSON
{
  "@context": "https://www.w3.org/ns/did/v1",
  "id": "did:ipns:k51qzi5uqu5dlvj2baxnqndepeb86cbk3ng7n3i46uzyxzyqj2xjonzllnv0v8",
  "authentication": [{
    "id": "did:ipns:k51qzi5uqu5dlvj2baxnqndepeb86cbk3ng7n3i46uzyxzyqj2xjonzllnv0v8",
    "type": "Ed25519VerificationKey2020",
    "controller": "did:ipns:k51qzi5uqu5dlvj2baxnqndepeb86cbk3ng7n3i46uzyxzyqj2xjonzllnv0v8",
    "publicKeyMultibase": "zH3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
  }],
  "verificationMethod": [
    {
      "controller": "did:ipns:k51qzi5uqu5dlvj2baxnqndepeb86cbk3ng7n3i46uzyxzyqj2xjonzllnv0v8",
      "id": "did:ipns:k51qzi5uqu5dlvj2baxnqndepeb86cbk3ng7n3i46uzyxzyqj2xjonzllnv0v8#key-1",
      "publicKeyMultiBase": {
      "type": "JsonWebKey2020"
    }
  ]
}
```