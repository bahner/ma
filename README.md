# 間

間 is a messaging protocol which uses existing tech and protocols as much as possible, but it deviates where necessary.

The gist is to be able to pass messages between traditional objects in programming. It's a complex RPC mechanism, which doesn't fit well into existing categories.

It is written to be a message passing infrastructure for distributed MOOs, but can be used in many other places. It is designed versioned, so that ut can merge with official DIDs whn they catch up and start to be more stable. The message protocol should be registered formally with the W3 DID registry, but probably isn't acceptable in its current form.

The protocol is inherently and highly distributed. No common infrastructure is required, but can help.

Concretely when you teleport from one "room" to another, you shouldn't be ablebtobtell whether its on the same server or another.

A small world should be able to run in the browser. Think that you can create a "homeroom" in the browser and it should be reachable from any other browser without requiring public IPs or a "server" of any kind. All processes are servers.
