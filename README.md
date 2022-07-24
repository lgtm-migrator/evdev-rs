# evdev-rs

[![Build Status](https://travis-ci.org/ndesh26/evdev-rs.svg?branch=master)](https://travis-ci.org/ndesh26/evdev-rs)
[![Latest Version](https://img.shields.io/crates/v/evdev-rs.svg)](https://crates.io/crates/evdev-rs)
[![Documentation](https://docs.rs/evdev-rs/badge.svg)](https://docs.rs/evdev-rs)

A Rust wrapper for libevdev

```toml
# Cargo.toml
[dependencies]
evdev-rs = "0.6.0"
```

to enable serialization support, enable the feature "serde"
```toml
# Cargo.toml
[dependencies]
evdev-rs = { version = "0.6.0", features = ["serde"] }
```

Why a libevdev wrapper?
-----------------------
The evdev protocol is simple, but quirky, with a couple of behaviors that
are non-obvious. libevdev transparently handles some of those quirks.

The [evdev](https://github.com/emberian/evdev) crate is an implementation
of evdev in Rust which provides most of the same features.

`evdev-rs` crate closely follows libevdev and hence enjoys all the complex handling
that libevdev does. Some of the things that libevdev handles transparently, which may or
may not be in evdev crate:

* handling of fake multitouch devices
* synching of slots and per-slot state
* transparent generation of missing tracking ids after SYN_DROPPED
* various boundary checks with defined error codes if you request invalid data
  (e.g. event codes that don't exist on the device)
* fd swapping on the same context
* disabling/enabling events on a per-context basis, so you can disable/enable ABS_FOO
  and then not care about quirks in the client-side code.

Development
-----------

`src/enums.rs` can be generated by running `./tools/make-enums.sh`.
