# Apple PowerBook PPC G4 - Lubuntu #

- ```diskutil unmountDisk /dev/disk2```

> if ``pv`` is installed via ``brew`` to monitor progress

- ```sudo dd if=lubuntu-12.04-desktop-powerpc.iso | pv | sudo dd of=/dev/disk2 bs=16m && sync```

