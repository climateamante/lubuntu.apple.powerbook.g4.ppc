# Apple PowerBook PPC G4 - Lubuntu #


## Install the USB disk image ##

 - ```diskutil unmountDisk /dev/disk2```

#### if ``pv`` is installed via ``brew`` to monitor progress ####

 > ```sudo dd if=lubuntu-12.04-desktop-powerpc.iso | pv | sudo dd of=/dev/disk2 bs=16m && sync```
 
 - if ``pv`` is __not__ installed...

 > ``sudo dd if=lubuntu-12.04-desktop-powerpc.iso of=/dev/disk2 bs=16m && sync``

## Boot In Recovery Mode ##

 - When at the boot login
 
 > ``Linux single``

 - Confirm that AMD graphics card is installed

 > ``lspci -k | grep -EA2 'VGA|3D``

 - Edit the default ``yaboot.config``

 > ``sudo nano /etc/yaboot.config``

 - Add the following line to the append config file

 >
```
image=/boot/vmlinux
        label=Linux
        read-only
        initrd=/boot/initrd.img
        append="quiet splash live video=radeonfb:1440x900-32@60"
```
