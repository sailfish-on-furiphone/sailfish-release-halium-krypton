# Sailfish on krypton

Release build CI

## Installation
* Download latest .tar.bz2 from https://github.com/sailfish-on-furiphone/sailfish-release-halium-krypton/releases
* Boot phone into FuriOS
* 'scp' the release to the phone
```
scp sailfish-releae-halium-krypton-<release>-<version>.tar.bz2 furios@furiphoneflx1:
```
* 'ssh' to the phone
```
ssh furios@furiphoneflx1
```
* mount and enter the sailfish root partition
```
mkdir sfos
sudo mount /dev/mapper/droidian-sailfish sfos/
cd sfos
sudo rm -rf *
sudo tar --numeric-owner -xvf ../sailfish-releae-halium-krypton-<release>-<version>.tar.bz2
```
* (TEMP) Rename boot.img
```
sudo mv boot/boot.img boot/boot.img-sfos
```
* Unmount and reboot
```
cd ..
sudo umount /dev/droidian/droidian-sailfish
sudo reboot
```
