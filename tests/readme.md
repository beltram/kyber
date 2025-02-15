# Testing

Without any feature flags `cargo test` will run through the key exchange functions and some doctests for the selected security level and mode. Running the Known Answer Tests require deterministic rng buffers from the test vector files. These files are quite large, you will need to generate them yourself. Instructions for building the KAT files are [here](./KAT/readme.md). Otherwise you can run:

```bash
cd KAT
./build_kats.sh
```

Which will clone the C reference repo, generate the KAT files, then rename and put them in the correct folder for testing.

To run the known answer tests you will need to use the `KAT` feature flag. To check different Kyber levels or 90's mode you will need to include those flags also. eg:
```bash
cargo test --features "KAT kyber1024 90s"
```

For applicible x86 architectures you must export the avx2 RUSTFLAGS if you don't want to test on reference

To run a matrix of all possible tests use the helper script from this folder:
```bash
./run_all_tests.sh
```

Test files:

* [kat.rs](./kat.rs)  - Runs a battery of test vectors using the Known Answer Test file of the selected security level and mode. There are 10,000 KATs per file.

* [kex.rs](./kex.rs) - Goes through a full key exchange procedure for both the UAKE and AKE functions.

* [kem.rs](./kem.rs) - A single run of random key generation, encapsulation and decapsulation.
