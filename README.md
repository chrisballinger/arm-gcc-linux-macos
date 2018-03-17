# ct-ng-nextthing-chip
crosstool-ng config for Next Thing [CHIP](https://en.wikipedia.org/wiki/CHIP_(computer)#CHIP)

This is intended for linking cross-compiled Rust `armv7-unknown-linux-gnueabihf` on macOS. Add it to your [crosstool-ng](https://github.com/crosstool-ng/crosstool-ng) samples folder.


```bash
# bison on macOS is too old
$ brew install bison
$ export PATH="/usr/local/opt/bison/bin:$PATH"
$ git clone https://github.com/crosstool-ng/crosstool-ng
$ cp -r ./armv7-chip-linux-gnueabihf ./crosstool-ng/samples

# make APFS case insensitive sparse image called `crosstool-ng`
make -f ct-ng armv7-chip-linux-gnueabihf
make -f ct-ng menuconfig
# ->> change all the paths paths to inside /Volumes/crosstool-ng/
make -f ct-ng build
```

`.cargo/config`
```toml
[target.armv7-unknown-linux-gnueabihf]
linker = "/Volumes/crosstool-ng/x-tools/armv7-chip-linux-gnueabihf/bin/armv7-chip-linux-gnueabihf-gcc"
```

```
$ rustup target install armv7-unknown-linux-gnueabihf
$ cargo build --target armv7-unknown-linux-gnueabihf
```
