# Fuzzing

This library uses Google's honggfuzz, for more information see the [official page](https://honggfuzz.dev/) or the [rust docs](https://docs.rs/honggfuzz/latest/honggfuzz/)

### Dependencies

* C compiler: cc
* GNU Make: make
* GNU Binutils development files for the BFD library: `libbfd-dev`
* libunwind development files: `libunwind-dev/libunwind8-dev`
* liblzma development files: `liblzma-dev`

To install on Debian:

```bash
sudo apt install build-essential binutils-dev libunwind-dev
cargo install honggfuzz
```

The best place to start probing is in the avx2 optimized versions.

### Usage:

```bash
cargo hfuzz run <TARGET>
```
To run different security levels and modes:

```bash
cargo hfuzz run <TARGET> --features " avx2 kyber512 90s"
```

Current targets are: 

* keypair
* encap
* decap