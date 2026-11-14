# SIML

**Simple, and also ML inside there.** *(placeholder tagline)*

SIML is a plain format for settings and manifests. It's made to be read by someone who has never coded: named blocks,
`key = value`, and comments in brackets, like an aside in a sentence.

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

SIML only knows blocks, `key = value`, quotes and comments. Whatever reads a SIML file, its host, decides which blocks
and keys exist and what they mean. The rules are in [`STANDARD.md`](STANDARD.md), and every decision behind them is in
[`DECISIONS.md`](DECISIONS.md).

Used by [Fale](https://github.com/Soclets/Fale), [Cyborg](https://github.com/Soclets/Cyborg) and
[Jernal](https://github.com/Soclets/Jernal-lang).

## Licences

- [`LICENSE`](LICENSE): Apache-2.0 WITH LLVM-exception, for the code.
- [`LICENSE-CC-BY-4.0`](LICENSE-CC-BY-4.0): CC BY 4.0, for this repo's writing: its Markdown files, including this
  README, `STANDARD.md` and `DECISIONS.md`. Credit them as `SIML GitHub repo text: https://github.com/Soclets/SIML`,
  say they're under CC BY 4.0, and say whether you changed them.

## Design & Impl credit (tools excluded)

Tankun Sriket (Tancum Srigay, TandzInfinity18, TandzNaN, Tandz): Owner and designer.
Anthropic's Claude (usually the latest Opus, multiple): Design help.
