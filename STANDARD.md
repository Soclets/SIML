# The SIML standard

A SIML file is read by a **host**: a program or language that decides which blocks and keys exist, which values they
take, and what they mean. SIML itself only knows the four things below (D2).

## 1. Blocks

A block opens with a name and `:`, and closes with `end` and the same name. Lines inside are indented by 4 spaces
per level, and a tab character is refused (D2, D9).

```
permissions:
    files = allowed
end permissions
```

## 2. `key = value`

Inside a block, each line is a key, `=`, and a value (D2). The host decides which keys exist. A `key = value`
outside any block is refused: blocks are what make a file SIML (D8).

## 3. Values

- **Text** is in quotes, even without a space: `"Hello"` (D2).
- **A bare word** is one the host knows, like `allowed`. The host refuses a word it doesn't know (D2).
- Inside quotes, every character is just a character, including `(` and `)` (D2), except that `\"` is a quote and
  `\\` is a backslash: `"Says \"hi\" to the world"` (D6). A
  backslash before anything else is refused, so a Windows path is written `"C:\\Users"` (D7).
- **A list** is in `[ ]`, with items separated by commas: `author = ["Tankun", "Multifinity"]` (D4). The host decides
  which keys take a list. A long list may break between items, one per line, with a comma allowed after the last
  (D5):

  ```
  author = [
      "Tankun",
      "Multifinity",
  ]
  ```

## 4. Comments

`( )` is a comment, anywhere outside quotes, including on a line of its own. Brackets inside a comment balance, so
`(see (this))` is one comment (D2).

```
description = "Says hello to the world"    (this is a comment)
(a whole line can be a comment)
```

## 5. Files

A SIML file is UTF-8, its lines may end in LF or CRLF, and its name ends in `.siml` (D10).

## 6. Mistakes

SIML refuses mistakes of shape, which any reader can see without knowing the host (D11):

- an unclosed quote, an unclosed block, or an `end` that doesn't match its block
- a `key = value` outside a block (D8), a tab (D9), or a backslash before anything but `"` or `\` (D7)
- an unbalanced `( )` comment
- a line that isn't a block, a `key = value` or a comment
- a key or block name that isn't lowercase letters, digits and `_`, starting with a letter
- the same key twice in one block

The host refuses mistakes of meaning: an unknown block, key or bare word; text where a word belongs, or the other way
round; a list where the key doesn't take one; a missing required key. Both kinds are shown in the host's own error
layout.

## Not decided

- When Cyborg and Jernal move from D1's syntax to this one.
