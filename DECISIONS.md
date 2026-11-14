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

**D4. A list is written in `[ ]`, with items separated by commas.** Like a list in Fale (Fale D3, D36: `[ ]` holds):

```
details:
    author = ["Tankun", "Multifinity"]
end details
```

The host decides which keys take a list. Claude had proposed repeating the key; the owner wrote this instead.
(Owner, 2026-11-14)

**D5. A long list may break between items, with a comma allowed after the last.** One item per line, indented, so
adding an item is a one-line change:

```
details:
    author = [
        "Tankun",
        "Multifinity",
    ]
end details
```

Claude proposed it; the owner chose: "yea". (Owner, 2026-11-14)

**D6. Inside text, `\"` is a quote and `\\` is a backslash.** `description = "Says \"hi\" to the world"`. Almost every
programming language does this, so it's learned once (Fale D29). Claude proposed it over doubling (`""`), noting that
Fale's text has the same question; the owner chose: "yup". (Owner, 2026-11-14)

**D7. A backslash before anything other than `"` or `\` is refused.** Otherwise `"line one\nline two"` would quietly
mean a backslash and an `n`, when someone used to other languages expects a new line. The error explains, and offers
`\\` for a real backslash, so a Windows path is written `"C:\\Users"`. Claude proposed it; the owner chose: "yea".
(Owner, 2026-11-14)

**D8. Every `key = value` sits inside a block.** A `key = value` outside any block is refused. Blocks are what make
a file SIML: each one names what its lines are for. Claude had proposed allowing loose keys and letting the host
decide; the owner said: "Tbh, the blocks is what makes it SIML". (Owner, 2026-11-14)

**D9. Indentation is 4 spaces per level, and a tab character is refused.** A tab and spaces can look identical on
screen while meaning different things to the reader, the classic invisible Python error. The error offers to convert
the tab. Editors insert spaces when the Tab key is pressed. Fale uses the same rule for its code (Fale D54). Claude
proposed it; the owner asked "What does that mean?", then chose: "yea". (Owner, 2026-11-14)

**D10. A SIML file is UTF-8, accepts LF and CRLF line endings, and ends in `.siml`.** UTF-8 so any language's
names work. Both line endings, since Windows editors write CRLF and refusing it would trip Windows users for nothing.
`.siml` is the owner's name for it (D1). Claude proposed them together; the owner chose: "yes". (Owner, 2026-11-14)

**D11. SIML refuses mistakes of shape; the host refuses mistakes of meaning.** SIML refuses what any reader can see
without knowing the host: an unclosed quote or block, an `end` that doesn't match, a `key = value` outside a block
(D8), a tab (D9), a bad backslash (D7), an unbalanced `( )` comment, a line that isn't a block, a `key = value` or a
comment, a key or block name that isn't lowercase letters, digits and `_` starting with a letter, and the same key
twice in one block (lists use `[ ]`, D4). The host refuses an unknown block, key or bare word, text where a word
belongs or the other way round, a list where the key doesn't take one, and a missing required key. Both kinds are
shown in the host's own error layout. Claude proposed the split; the owner chose: "yea". (Owner, 2026-11-14)

## Open

- When Cyborg and Jernal move from D1's syntax to D2's.
