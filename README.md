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
sudo mkfs.ext4 /dev/mapper/furios-sailfish
sudo mount /dev/mapper/furios-sailfish sfos/
cd sfos
sudo rm -rf *
sudo tar --numeric-owner --strip-components=2 -xvf ../sailfish-release-halium-krypton-<release>.tar.bz2 
```
* Unmount and reboot
```
cd ..
sudo umount /dev/mapper/fusios-sailfish
sudo reboot
```
