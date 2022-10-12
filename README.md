# The Noir Programming Language

![Deploy Status](https://github.com/noir-lang/book/workflows/github%20pages/badge.svg)

This repository contains the source of "The Noir Programming Language" book.

You can read the book here: https://noir-lang.github.io/book/

## Deploy

The book is deployed using [peaceiris's GitHub Pages Action](https://github.com/peaceiris/actions-gh-pages).

## Local Build

Alternatively, the book can also be built and viewed locally.

### Requirements

- Install [Rust](https://www.rust-lang.org/tools/install)
- Install [mdBook](https://github.com/rust-lang-nursery/mdBook)

  ```bash
  $ cargo install mdbook
  ```

### Building

To build the book, run:

```bash
$ mdbook build
```

The output will be in the `book` subdirectory. To check it out, open it in your web browser.

You can open the `index.html` in the subdirectory from your GUI, or alternatively using commands:

_Firefox_

```bash
$ firefox book/index.html                       # Linux
$ open -a "Firefox" book/index.html             # macOS
$ Start-Process "firefox.exe" .\book\index.html # Windows (PowerShell)
$ start firefox.exe .\book\index.html           # Windows (Cmd)
```

_Chrome_

```bash
$ google-chrome book/index.html                 # Linux
$ open -a "Google Chrome" book/index.html       # macOS
$ Start-Process "chrome.exe" .\book\index.html  # Windows (PowerShell)
$ start chrome.exe .\book\index.html            # Windows (Cmd)
```

## Get In Touch

Join our [Discord]'s `#🖤│noir` channel for Noir discussions.

[discord]: https://discord.gg/aztec
