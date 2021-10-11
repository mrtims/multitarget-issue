arm.rs is destined for thumbv7em-none-eabihf, while win.rs is for x86_64-pc-windows-msvc.
```bash
cargo build --bin arm --target thumbv7em-none-eabihf
```
Should build arm.rs just fine, and
```bash
cargo build --bin win --target x86_64-pc-windows-msvc
```
should build win.rs.

However with the cargo.toml file here, the arm build fails with:
```bash
Compiling byteorder v1.4.3
error[E0463]: can't find crate for `std`
  |
  = note: the `thumbv7em-none-eabihf` target may not support the standard library
  = note: `std` is required by `byteorder` because it does not declare `#![no_std]`

error: aborting due to previous error

For more information about this error, try `rustc --explain E0463`.
error: could not compile `byteorder`

To learn more, run the command again with --verbose.
```

Commenting out either heapless from the ARM dependencies or embedded-graphics-simulator from the windows dependencies fixes this issue.
However having both at the same time seems to cause some kind of std/no_std clash.


