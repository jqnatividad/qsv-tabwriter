NOTE: qsv-tabwriter is a renamed fork of tabwriter with the following changes:
* It implements LeftTabEnd and LeftFwf alignment
* updated to 2024 edition
* applied numerous clippy lint suggestions
* is BufWriter-backed to minimize syscalls

tabwriter is a crate that implements
[elastic tabstops](http://nickgravgaard.com/elastictabstops/index.html). It
provides both a library for wrapping Rust `Writer`s and a small program that
exposes the same functionality at the command line.

Dual-licensed under MIT or the [UNLICENSE](http://unlicense.org).


### Simple example of library

```rust
use std::io::Write;

use qsv_tabwriter::TabWriter;

let mut tw = TabWriter::new(vec![]);
tw.write_all(b"
Bruce Springsteen\tBorn to Run
Bob Seger\tNight Moves
Metallica\tBlack
The Boss\tDarkness on the Edge of Town
").unwrap();
tw.flush().unwrap();

let written = String::from_utf8(tw.into_inner().unwrap()).unwrap();

assert_eq!(&written, "
Bruce Springsteen  Born to Run
Bob Seger          Night Moves
Metallica          Black
The Boss           Darkness on the Edge of Town
");
```


### Documentation

The API is fully documented with some examples:
[https://docs.rs/qsv-tabwriter/latest/tabwriter/](https://docs.rs/qsv-tabwriter/latest/tabwriter/).


### Installation

This crate works with Cargo. Assuming you have Rust and
[Cargo](http://crates.io/) installed, simply check out the source and run
tests:

```bash
git clone git://github.com/jqnatividad/qsv-tabwriter
cd qsv-tabwriter
cargo test
```

You can also add `qsv-tabwriter` as a dependency to your project's `Cargo.toml`:

```toml
[dependencies]
qsv-tabwriter = "2"
```


### Dealing with ANSI escape codes

If you want `tabwriter` to be aware of ANSI escape codes, then you should
enable the `TabWriter::ansi` option. Previously this was done by enabling the
crate feature `ansi_formatting`, but that feature is now deprecated. (If you
use it, then `TabWriter::ansi` will be automatically enabled for you. Otherwise
it is disabled by default.)


### Minimum Rust version policy

This crate's minimum supported `rustc` version is `1.90.0`.

The current policy is to use the latest Rust stable.
