# Hello Linux RISC-V 64

This tiny tool lets you print some information from `/proc` and `uname` from
Linux on RISC-V 64. 

## Build

### Rust Version

You will need [Rust](https://www.rust-lang.org/) and the linker from
`riscv64-linux-gnu-gcc`.

```sh
cargo build --release
```

or `zig` linker:

```sh
cargo install cargo-zigbuild

cargo zigbuild --release
```

### Zig version
You will need [Zig](https://ziglang.org/)

```sh
# zig version v0.11 or higher (default self-hosting compiler [stage3]) 
zig build -Doptimize=<mode> -Dtarget=arch-os-libc
# mode = ReleaseSafe|ReleaseFast|ReleaseSmall

# specific target
zig build -Doptimize=<mode> -Dtarget=riscv64-linux -Dcpu=baseline_rv64+v # Allwinner D1

# more features RISC-V: https://github.com/lupyuen/zig-bl602-nuttx/issues/1

# Execute (after builded)
./zig-out/bin/hello-zig
# or run directly (default: host target) 
zig build run -Doptimize=<mode> -Dtarget=riscv64-linux

# all targets
zig targets | jq .libc
```

## Run via [`cpu`](https://github.com/u-root/cpu)

```sh
cpu -key ~/.ssh/cpu_rsa -timeout9p 2000ms target-host \
  ./target/riscv64gc-unknown-linux-gnu/release/hello-rust
  or
  ./zig-out/bin/hello-zig
```
