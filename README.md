# Rust Foreign Function Interface

Based on https://doc.rust-lang.org/1.5.0/book/ffi.html and https://doc.rust-lang.org/cargo/reference/build-script-examples.html

Tested on Ubuntu 20.04.1 LTS with cargo 1.47.0 (f3c7e066a 2020-08-28)


## File structure
```
├── build.rs
├── Cargo.toml
├── lib
│   ├── libsnappy.so -> libsnappy.so.1
│   ├── libsnappy.so.1 -> libsnappy.so.1.1.6
│   ├── libsnappy.so.1.1.6
│   └── snappy-c.h
├── snappy-1.1.6.zip
└── src
    └── main.rs

```

## Build libsnappy

Uncompress snappy-1.1.6.zip

```
cd snappy-1.1.6
mkdir build
cd build && cmake ../ && make
```
Copy libsnappy.* from snappy-1.1.6/build to rust_ffi/lib

## Build and run ffi_test application

```
$ cargo build
```
Output example:

```
    Updating crates.io index
   Compiling libc v0.2.81
   Compiling ffi_test v0.1.0 (/home/oleksandr/rust_sandbox/rust_ffi)
    Finished dev [unoptimized + debuginfo] target(s) in 2.48s

```

```
$ cargo run
```

Output example:

```
    Finished dev [unoptimized + debuginfo] target(s) in 0.01s
     Running `target/debug/ffi_test`
max compressed length of a 200 byte buffer: 265

```

## Notes: 

In some cases libc crate requires nightly build:

```
rustup install nightly
```

And building and running with +nightly option

```
cargo +nightly build 
cargo +nightly run
```

## Links

https://doc.rust-lang.org/1.5.0/book/ffi.html

https://doc.rust-lang.org/cargo/reference/build-scripts.html#outputs-of-the-build-script

https://doc.rust-lang.org/cargo/reference/build-script-examples.html

https://doc.rust-lang.org/1.5.0/book/rust-inside-other-languages.html

https://github.com/google/snappy

https://github.com/google/snappy/releases/tag/1.1.6 (1.1.6 builds *.so, 1.1.8 builds *.a by default)
