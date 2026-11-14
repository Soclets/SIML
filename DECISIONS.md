# SIML: design decisions

The owner decides; Claude proposes and records. Each entry says what was chosen and whose idea it was. Numbers are
permanent, so a decision is never renumbered. A changed decision gets a new entry that says which one it replaces.
New entries go just before "Open".

## Decided

**D1. SIML is the owner's own format.** It was made for Cyborg's manifest, `CyJet.siml`, on 2026-11-10 (Cyborg D228
to D231), after the owner asked for "a more no fluff, straight-forward syntax" than TOML. The owner named it: "It's
called `.siml`. Simple, and also ML inside there". Jernal adopted it for `Journey.siml` (Jernal D75: "`siml` is a lot
more straight-forward"). That first version had one fact per line, values after the key separated by spaces, `//`
comments, and dotted prefixes for scope. D2 replaces it. (Owner, 2026-11-10)

**D2. Redesigned from scratch: named blocks, `key = value`, `( )` comments, quoted text and bare host words.** Designed
in Fale's design session (Fale D52) for Fale's manifest:

```
details:
    name = "Hello"
    description = "Says hello to the world"    (this is a comment)
end details

permissions:
    files = allowed
    terminal = allowed
end permissions
```

- The host defines everything: block names, keys, and which values are allowed. SIML only knows blocks,
  `key = value`, quotes and comments.
- A block opens with `name:` and closes with `end name`; lines inside are indented.
- `( )` is a comment, anywhere outside quotes, including on a line of its own. Brackets inside a comment balance.
  Inside quotes, `(` is just a character.
- Quotes mean text, even without a space. A bare word is one the host knows, like a `one_of` value, and the host
  refuses a word it doesn't know.

The owner said "Let's make an siml standard actually, scratch syntax. Let's get it, propose"; Claude proposed a
line-based design; the owner sketched this instead: "Things like `name` and other settings are definiable by that
SIML's host, rather than fixed"; Claude filled in indentation, comment and quoting rules; the owner chose: "yea".
(Owner, 2026-11-14)

**D3. SIML has its own repository, `Soclets/SIML`.** SIML belongs to every language that uses it, so its standard
lives on its own, and Fale, Cyborg and Jernal point at it. Jernal's design session suggested a shared repo. The owner
chose: "yup. SIML in big letters". (Owner, 2026-11-14)

## Open

- Lists, such as several authors.
- How to write a `"` inside text.
- Whether a `key = value` can sit outside any block.
- Spaces or tabs for indentation, and how many.
- Encoding (UTF-8 assumed), line endings, and the file extension (`.siml` today).
- Which mistakes SIML itself refuses, and which are the host's to refuse.
- When Cyborg and Jernal move from D1's syntax to D2's.
