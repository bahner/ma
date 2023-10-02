# Rendezvous

Rendezvous is a part of peer discovery in libp2p when using GossipSub. It is also used for other protocols. It is a way to find peers thar are connected to the 間.

## Rendezvous strings

`/ma/0.0.1`

All rendezvous strings must start with `/ma` and the version number. The version number is the version defined by this spec and may change in the future.

## My SPACE™

If you have your [own world or namespace][SPACE], you can use this tag to signify that you are sending messages for that world or namespace.

`/ma/0.0.1/myspace`

This could mean that others won't see you. Implementers are free to parse this as they see fit. Think of the rendezvous string as a radio station that you tune into. If you don't know the station, you won't hear it.

[SPACE]: <https://github.com/bahner/SPACE> "Spaces for Punk Actors in Cybernetic Entities"
