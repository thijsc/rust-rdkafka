# rust-rdkafka

[![crates.io](https://img.shields.io/crates/v/rdkafka.svg)](https://crates.io/crates/rdkafka)
[![docs.rs](https://docs.rs/rdkafka/badge.svg)](https://docs.rs/rdkafka/)
[![Build Status](https://travis-ci.org/fede1024/rust-rdkafka.svg?branch=master)](https://travis-ci.org/fede1024/rust-rdkafka)
[![Join the chat at https://gitter.im/rust-rdkafka/Lobby](https://badges.gitter.im/rust-rdkafka/Lobby.svg)](https://gitter.im/rust-rdkafka/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Kafka client library for Rust based on [librdkafka].

## The library
This library aims to provide a safe interface to librdkafka.
It currently exports some of the funcionalities provided by the producer and consumer
of librdkafka 0.9.2.

Producers and consumers can be accessed and polled directly, or alternatively
a [futures]-based interface can be used:

* A consumer will return a [`stream`] of messages, as they are received from Kafka.
* A producer will return a [`future`] that will eventually contain the delivery
status of the message.

[librdkafka]: https://github.com/edenhill/librdkafka
[futures]: https://github.com/alexcrichton/futures-rs
[`future`]: https://docs.rs/futures/0.1.3/futures/trait.Future.html
[`stream`]: https://docs.rs/futures/0.1.3/futures/stream/trait.Stream.html

*Warning*: this library is still at an early development stage, the API is very likely
to change and it shouldn't be considered production ready.

## Installation

Add this to your `Cargo.toml`:

```toml
[dependencies]
rdkafka = "^0.2.0"
```

This crate will compile librdkafka from sources and link it statically in your
executable. To compile librdkafka you'll need:

* the GNU toolchain
* GNU `make`
* `pthreads`
* `zlib`
* `libssl-dev`: optional, *not* included by default (feature: `ssl`).
* `libsasl2-dev`: optional, *not* included by default (feature: `sasl`).

To enable ssl and sasl, use the `features` field in `Cargo.toml`. Example:

```toml
[dependencies.rdkafka]
version = "^0.3.0"
features = ["ssl", "sasl"]
```

## Compiling from sources

To compile from sources, you'll have to update the submodule containing librdkafka:

```bash
git submodule update --init
```

and then compile using `cargo`, selecting the features that you want. Example:

```bash
cargo build --features "ssl sasl"
```

## Examples

You can find examples in the `examples` folder. To run them:

```bash
cargo run --example <example_name> -- <example_args>
```

## Tests

The unit tests can run without a Kafka broker present:

```
cargo test --lib
```

To run the full suite:

```
cargo test
```

In this case there is a broker expected to be running on
`localhost:9292`. Travis currently only runs the unit tests.

## Documentation

Documentation is available on [docs.rs](https://docs.rs/rdkafka/).

## Contributors

Thanks to:
* Thijs Cadier - [thijsc](https://github.com/thijsc)

## Alternatives

* [kafka-rust]: a pure Rust implementation of the Kafka client.

[kafka-rust]: https://github.com/spicavigo/kafka-rust
