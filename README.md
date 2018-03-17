# ct-ng-nextthing-chip
crosstool-ng config for Next Thing [CHIP](https://en.wikipedia.org/wiki/CHIP_(computer)#CHIP)

This is intended for linking cross-compiled Rust `armv7-unknown-linux-gnueabihf` on macOS. Add it to your [crosstool-ng](https://github.com/crosstool-ng/crosstool-ng) samples folder.


### For Next Thing CHIP v1

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


### For original Raspberry Pi or Zero

```
$ rustup target install arm-unknown-linux-gnueabi
$ make -f ct-ng armv6-rpi-linux-gnueabi
$ make -f ct-ng menuconfig
$ make -f ct-ng build
$ 

### Rust


`.cargo/config`
```toml
[target.armv7-unknown-linux-gnueabihf]
linker = "/Volumes/crosstool-ng/x-tools/armv7-chip-linux-gnueabihf/bin/armv7-chip-linux-gnueabihf-gcc"
[target.arm-unknown-linux-gnueabi]
linker = "/Volumes/crosstool-ng/x-tools/armv6-rpi-linux-gnueabi/bin/armv6-rpi-linux-gnueabi-gcc"
```

```
$ rustup target install armv7-unknown-linux-gnueabihf
$ rustup target install arm-unknown-linux-gnueabi
$ cargo build --target armv7-unknown-linux-gnueabihf
$ cargo build --target arm-unknown-linux-gnueabi
```
