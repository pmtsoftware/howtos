- download latest 64-bit Windows 10 ISO into ~/Downloads directory (ex. Win10_20H2_English_x64.iso)
- install necessary tools:
  ```
    sudo pkg install 7-zip wimlib
  ```
 - create ```windows``` directory with extracted content of iso file:
  ```
    mkdir ~/windows
    cd ~/windows; 7z x ~/Downloads/Win10_20H2_English_x64.iso
  ```
- after extraction, compress the size by running:
  ```
    cd sources; doas wimlib-imagex optimize install.wim --solid
  ```
- prepare USB drive
  ```
    sudo gpart destroy -F da0
    sudo gpart create -s GTP da0
    sudo gpart add -a 4k -t ms-basic-data da0
    sudo newfs_msdos -F 32 -L Windows10 /dev/da0p1
    sudo mount -t msdosfs /dev/da0p1 /mnt
    sudo cp -R ~/windows/ /mnt/
    sudo umount /mnt
    sudo sync
  ```
  
  instruction based on this [post](https://forums.freebsd.org/threads/creating-a-windows-10-bootable-usb-stick-using-freebsd.77429/)
  
