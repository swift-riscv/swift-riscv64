## Clone the Swift Project Repositories

```sh
# clone swift and checkout version
git clone https://github.com/apple/swift.git
cd swift
git checkout release/5.10
cd -

# clone supporting repositories
./swift/utils/update-checkout --clone --tag swift-5.10-RELEASE

```

## Patches for swift 5.10 release

```sh
# swift
cd swift
wget https://raw.githubusercontent.com/swift-riscv/swift-riscv64/main/patches/swift/5.10/set-lld-linker-as-default-5.10-v2.patch
git apply set-lld-linker-as-default-5.10-v2.patch

# note: apply skip-build-libicu patch before bootstrapping-off patch if needed
wget https://raw.githubusercontent.com/swift-riscv/swift-riscv64/main/patches/swift/5.10/skip-build-libicu-5.10.patch
git apply skip-build-libicu-5.10.patch

wget https://raw.githubusercontent.com/swift-riscv/swift-riscv64/main/patches/swift/5.10/bootstrapping-off-5.10.patch
git apply bootstrapping-off-5.10.patch

wget https://raw.githubusercontent.com/swift-riscv/swift-riscv64/main/patches/swift/5.10/nostart-stop-gc-5.10.patch
git apply nostart-stop-gc-5.10.patch
cd -

# swift-driver
cd swift-driver
wget https://raw.githubusercontent.com/swift-riscv/swift-riscv64/main/patches/swift/5.10/swift-driver-use-lld-riscv64.patch
git apply swift-driver-use-lld-riscv64.patch
cd -
```

## Build Swift

```sh
# $USER = build-user
./swift/utils/build-script --preset buildbot_linux,no_test install_destdir=/home/build-user/swift-install installable_package=/home/build-user/swift-5.10-RELEASE.tar.gz
```
