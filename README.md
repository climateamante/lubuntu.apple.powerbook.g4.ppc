# Apple PowerBook PPC G4 - Lubuntu #
 > Hardware Tested | PowerBook G4 1.67 17" (Al)

## Install the USB disk image ##

 - Find your USB device
	- ``diskutil list``

 - Unmount the USB device before making the bootable drive
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

```
image=/boot/vmlinux
        label=Linux
        read-only
        initrd=/boot/initrd.img
        append="quiet splash live video=radeonfb:1440x900-32@60"
```

## Optimization ##


``cat /proc/sys/vm/swappiness``
```
#Decrease swap usage to a more reasonable level
vm.swappiness=10
```


## Keyboard Backlight ##

```
sudo modprobe i2c-dev
sudo /etc/init.d/pbbuttonsd restart
```

```
sudo modprobe pmu_battery
sudo nano /etc/modules
 > pmu_battery
```

## Setting Up WiFi ##

```
sudo apt-get install firmware-b43-installer
```


## Setting Up VPN ##

 - Able to import `opvn` config file

```
sudo apt-get install openvpn network-manager-openvpn network-manager-openvpn-gnome network-manager-vpnc
sudo /etc/init.d/networking restart
```



## Notes ##

The ``yaboot.config`` screen dimensions should match your device, the example was for a 17-inch powerbook with an ATI Radeon


There will be times when the screen is off or the ethernet connection may seem slow, be patient.

If the screen stays completely black for longer than five minutes with no response

 - no mouse movement
 - no keyboard activity
 - no network activity

Then it is possible that it was a kernel panic or a setting changed from the ``yaboot.config`` that is incorrect for your device.

All credit goes to the countless hours of the opensource Apple | Lubuntu community for breathing life back into old hardware.
