# ckb-auth-examples
This is example projects for [ckb-auth](https://github.com/nervosnetwork/ckb-auth)

Before compilation, ensure that submodules and their dependencies are updated:

```shell
git submodule update --init --recursive
```

## Rust Example

### Install Tools
The Rust example relies on capsule and cross; they need to be installed before compiling:

```shell
cargo install ckb-capsule --version "0.10.2"
cargo install cross --git https://github.com/cross-rs/cross
```

- The `capsule` version required is 0.10.2.
- The `cross` requires the main branch (some bugs have been resolved, and a new version has not been released yet).

### Build
In the `Rust` directory:

```shell
capsule build --release
```

### Test
In the `Rust/tests` directory:

```shell
cargo test
```

The compilation of `deps/ckb-auth` occurs in `Rust/tests/build.rs`. Subsequently, `auth` and `secp256k1_data_20210801` are copied to `Rust/build` for testing.

Note: The provided tests cover only a few simple cases; more test cases are available in ckb-auth.

## C Example

### Build
In the `C` directory:

```shell
make all-via-docker
# Build with GNU toolchain
```

or

```shell
make -f Makefile.clang all
# Build with LLVM toolchain
```

The compilation results are stored in `C/build`.

When compiling within Docker, ensure that the Docker mapping directory is this repository, as the code depends on `ckb_auth.h`.

### Test
The contract interfaces of the C example and Rust example are the same. Thus, the C example generally uses Rust's tests. Here, copy the C binary directly to `Rust/build/debug` and rename it to `auth-rust-example`.

In actual use:
- Copy `Rust/tests` to the C language contract directory.
- Modify the name in `src/lib.rs`.
- Copy `auth` and `secp256k1_data_20210801` to the `build` directory.