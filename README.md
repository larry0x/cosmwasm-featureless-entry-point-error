# cosmwasm-featureless-entry-point-error

Running the following command:

```bash
docker run --rm -v "$(pwd)":/code \
  --mount type=volume,source="$(basename "$(pwd)")_cache",target=/target \
  --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
  cosmwasm/optimizer:0.16.0
```

Results in error:

```plain
Building outer with features {}
Building "outer" ...
   Compiling outer v0.0.0 (/code/contracts/outer)
error: linking with `rust-lld` failed: exit status: 1
  |

...
          rust-lld: error: duplicate symbol: instantiate
          >>> defined in /target/wasm32-unknown-unknown/release/deps/outer.outer.df9355434b583e16-cgu.2.rcgu.o
          >>> defined in /target/wasm32-unknown-unknown/release/deps/libinner.rlib(inner.inner.755fed0be595de25-cgu.2.rcgu.o)

error: could not compile `outer` (lib) due to 1 previous error
thread 'main' panicked at src/pkg_build.rs:79:9:
assertion failed: error_code.success()
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```
