# Boot From NVME SSD

Note: This method currently only works with the `starfive visionfive2` images.

### Update to 3.0.4 Firmware

[VF2_v3.0.4](https://github.com/starfive-tech/VisionFive2/releases/tag/VF2_v3.0.4)  
[Instructions Here](https://doc-en.rvspace.org/VisionFive2/Quick_Start_Guide/VisionFive2_SDK_QSG/updating_spl_and_u_boot%20-%20vf2.html)

### Load img to SD Card and Boot Board

Use Etcher or similar software to load `starfive-jh7110-VF2-SD-wayland.img` to an sd card.

After board has booted from sd card run the following commands.

```sh
sudo dd if=starfive-jh7110-VF2-SD-wayland.img of=/dev/nvme0n1 bs=4M status=progress conv=fdatasync
```

```sh
sudo mkdir nvme-boot && sudo mount /dev/nvme0n1p3 nvme-boot
sudo sed -i 's/mmcblk1p3/nvme0n1p3/g' nvme-boot/extlinux/extlinux.conf
sudo sed -i 's/mmcblk1p4/nvme0n1p4/g' nvme-boot/extlinux/extlinux.conf
sudo umount nvme-boot
sudo mkdir nvme-root && sudo mount /dev/nvme0n1p4 nvme-root
sudo sed -i 's/mmcblk1p3/nvme0n1p3/g' nvme-root/etc/fstab
sudo sed -i 's/mmcblk1p4/nvme0n1p4/g' nvme-root/etc/fstab
sudo umount nvme-root
sudo shutdown now
```

Reboot and [Resize nvme Partition](https://doc-en.rvspace.org/VisionFive2/Quick_Start_Guide/VisionFive2_QSG/extend_partition.html)

```sh
# fix sources.list
sudo nano /etc/apt/sources.list
# add - deb https://deb.debian.org/debian/ unstable main contrib non-free
# update keys
wget https://deb.debian.org/debian/pool/main/d/debian-ports-archive-keyring/debian-ports-archive-keyring_2023.02.01_all.deb
dpkg -i debian-ports-archive-keyring_2023.02.01_all.deb
sudo apt update
sudo apt upgrade
```
