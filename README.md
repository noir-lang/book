# The Noir Programming Language

![Deploy Status](https://github.com/noir-lang/book/workflows/github%20pages/badge.svg)

This repository contains the source of "The Noir Programming Language" book.

You can read the book here: https://noir-lang.github.io/book/

## Deploy

The book is deployed using [peaceiris's GitHub Pages Action](https://github.com/peaceiris/actions-gh-pages).

## Local Serve

Alternatively, the book can also be served and viewed locally.

### Requirements

- Install [Rust](https://www.rust-lang.org/tools/install)
- Install [mdBook](https://github.com/rust-lang-nursery/mdBook)

  ```bash
  $ cargo install mdbook
  ```

### Serve

To serve the book, run:

```bash
$ mdbook serve --open
```

A local server will start and hot-builds your local book. The `--open` flag will open the book in your default web browser.

To learn more about mdBook, visit [mdBook Documentation](https://rust-lang.github.io/mdBook/).

## Get In Touch

Join our [Discord]'s `#🖤│noir` channel for Noir discussions.

[discord]: https://discord.gg/aztec
