# Rendezvous

The rendezvous is just a text string uses as a rendezvous string in libp2p DHT peer discovery.
Since i don't know where or if I should register a namespace, I just invent my own and trademark it.

I propose that all elements of a Sub-Etha™ rendezvous connection string should be trademarked.

## Sub-Etha™

Since we don't have any registered namespace, we just invent our own :-)
Since we haven't registered it anywhere, just state that we intend to trademark it, then others stay away :-)

The namespace is easily just `Sub-Etha™` and this is the only rendezvous string you need really. We do need one, though.

Using this signifies that you are sending Sub-Etha™ structured messages over it, which can be used for authenticated and encrypted messages using the spec.

This can be used for chat messages and such.

To start sending message for fun and profit, use: `Sub-Etha™`
This signifies that you are folloing the Sub-Etha™ message format.

Rendezvous string: `Sub-Etha™`

## SPACE™

I see SPACE™ as an implementation or POC for this type of actor messaging. So while Sub-Etha™ can be used in general, the MOO in intend to write, should probably use SPACE™ as well.

So SPACE™ messages extend the Sub-Etha™ messages with types of messages, eg: Policies, Commands, Objects etc.

Rendezvous string: `Sub-Etha™:SPACE™`

## The Earth™

Someone should implement a paved version. If you do that, you can use the following rendezvous string to stand out from the crowd.

Rendezvous string: `Sub-Etha™:SPACE™:The Earth™`

## Technicalities

A rendezvous string should match the following BNF and regexes:

```BNF
<string> ::= "Sub-Etha™" | "Sub-Etha™" <element-list>
<element-list> ::= ":" <element> | ":" <element> <element-list>
<element> ::= <printable-chars> "™"
<printable-chars> ::= <printable-char> | <printable-char> <printable-chars>
<printable-char> ::= "any printable UTF-8 character"
```

```go
// golang regex
^Sub-Etha™(:[\pL\pM\pN\pP\pS]+™)*$
```

```elixir
defmodule SubEtha.Rendezvous do
  @pattern ~r/^Sub-Etha™(:[^\x00-\x1F]+™)*$/

  @doc """
  Checks if a given string is valid according to the specified pattern and is composed of printable characters.
  """
  def isValid?(str) do
    is_printable = String.printable?(str)
    is_match = Regex.match?(@pattern, str)
    is_printable and is_match
  end
end
```

### Multibase

I suspect multibasing the actual is a thought to be had, but that add's an unneeded layer of quickly parsing messages on gossipsub. Better just leave it as string, I think.

2023-09-23: bahner
