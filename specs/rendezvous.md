# Rendezvous and MIME types

Though we don't have any registered [MIME] type, at least not yet, we use the following base MIME type:

`application/x-ma-message`

NB! There is no strong correlation with actual MIME types. This is just a convention that makes sense.
The MIME registry is a valuable database and there are lot of tools for parsing them. So we use it.

## Rendezvous strings

The rendezvous string is used for GossipSub and other rendezvous protocols. This is the only rendezvous string you need really. We do need one, though.

For the same of simplicity and ease of use, we use the following MIME types for the rendezvous strings:

`application/x-ma-message-rendezvous`

### My SPACE™

If you have your [own world or namespace][SPACE], you can use this tag to signify that you are sending messages for that world or namespace.

`application/x-ma-message-rendezvous+myspace`

This could mean that others won't see you. Implementers are free to parse this as they see fit. Think of the rendezvous string as a radio station that you tune into. If you don't know the station, you won't hear it.

[SPACE]: <https://github.com/bahner/SPACE> "Spaces for Punk Actors in Cybernetic Entities"
[MIME]: <https://www.iana.org/assignments/media-types/media-types.xhtml> "IANA MIME Media Types"
