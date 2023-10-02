# 間

This is the spec for the actual 間 messages supported by the rest of this spec.

## MIME Type

Though we don't have any registered [MIME] type, at least not yet, we use the following base MIME type:

`application/x-ma-message`

NB! There is no strong correlation with actual MIME types. This is just a convention that makes sense.
The MIME registry is a valuable database and there are lot of tools for parsing them. So we use it.

### Versioning

Versioning is hinted by adding a version number to the MIME type. The version number is the version of this spec. It is not the version of the message itself. The version of the message is defined in the message itself.

`application/x-ma-message; version=0.0.1`

[MIME]: <https://www.iana.org/assignments/media-types/media-types.xhtml> "IANA MIME Media Types"
