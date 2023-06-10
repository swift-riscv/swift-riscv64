# Fix for only showing 4GB memory

### Recompile DTB

- Recompile .dtb file (run as root user)

```bash
# go to boot directory
cd /boot/dtb/starfive/

# backup original dtb file
cp jh7110-visionfive-v2.dtb jh7110-visionfive-v2.dtb.old

# decompile jh7110-visionfive-v2.dtb into temp file
dtc -I dtb -O dts jh7110-visionfive-v2.dtb -o temp-vf2.dts

# edit temp-vf2.dts
nano temp-vf2.dts
# find the line - device_type = "memory" and edit the line below it.
# replace - reg = <0x00 0x40000000 0x01 0x00>;
# with    - reg = <0x00 0x40000000 0x02 0x00>;
# save and exit nano

# recompile file
dtc -I dts -O dtb -o temp-vf2.dtb temp-vf2.dts

# replace jh7110-visionfive-v2.dtb with temp-vf2.dtb
mv temp-vf2.dtb jh7110-visionfive-v2.dtb

# remove temp-vf2.dts file
rm temp-vf2.dts

# restart device
```

### Quick Fix

- Quick fix with patched .dtb file

```bash
# go to boot directory
cd /boot/dtb/starfive

# backup original dtb file
sudo mv jh7110-visionfive-v2.dtb jh7110-visionfive-v2.dtb.old

# download new .dtb file
sudo wget https://github.com/swift-riscv/swift-riscv64/raw/main/visionfive-2/patch-files/jh7110-visionfive-v2.dtb

# restart device
```
