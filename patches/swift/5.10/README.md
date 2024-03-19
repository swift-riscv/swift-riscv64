## Patches for swift 5.10 release

```sh
# swift
cd swift
wget https://raw.githubusercontent.com/futurejones/swift-arm64/master/swift-5.10-patches/set-lld-linker-as-default-5.10-v2.patch
git apply set-lld-linker-as-default-5.10-v2.patch

wget https://raw.githubusercontent.com/futurejones/swift-arm64/master/swift-5.10-patches/bootstrapping-off-5.10.patch
git apply bootstrapping-off-5.10.patch

wget https://raw.githubusercontent.com/futurejones/swift-arm64/master/swift-5.10-patches/nostart-stop-gc-5.10.patch
git apply nostart-stop-gc-5.10.patch
cd -

# swift-driver
cd swift-driver
wget https://github.com/apple/swift-driver/pull/1545.patch
git apply 1545.patch
```
