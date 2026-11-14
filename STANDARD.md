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

## Not decided

- Encoding (UTF-8 assumed), line endings, and the file extension (`.siml` today).
- Which mistakes SIML itself refuses (an unclosed quote or block, a mismatched `end`, a bad key), and which are the
  host's to refuse.
