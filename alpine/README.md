# Install Alpine Linux for radiogaga

This has been written while installing Alpine Linux 3.9.3 on a Raspberry Pi 3 from a macOS computer.

## Prepare the SD card

1. [Download Alpine Linux](https://alpinelinux.org/downloads/) image for Rapsberry Pi ARMv7 
2. Insert the SD card in your computer and identify the assigne device using ```diskutil list``` (for me ```disk3```)
3. Format the SD card

```
~> sudo diskutil partitionDisk disk3 MBR "MS-DOS FAT32" RADIOGAGA R
```

4. Extract Alpine Linux image on the SD card

```
~> cd /Volumes/RADIOGAGA
~> tar xzf $HOME/Downloads/alpine-rpi-3.9.3-armv7.tar.gz
```

5. Copy ```alpine.answer``` on the the SD card
6. Eject the SD card

## First Boot

1. Insert the SD card, plug display, keyboard and ethernet cable then boot the Raspberry 
2. Log as root without password
3. Install Alpine Linux

```
cd /media/
setup-alpine -c alpine.anwser
# Accepts all defaults choices
```

4. Add ```PermitRootLogin yes``` in ```/etc/ssh/sshd_config```
5. Save configuration with ```lbu commit -d```
6. Reboot

Now it must be possible to connect remotely as root using ssh.

## Manually install Avahi & Python3

```
radiogaga:~# apk update
radiogaga:~# apk add dbus avahi python3
radiogaga:~# rc-update add avahi-daemon default
radiogaga:~# rc-service avahi-daemon start
radiogaga:~# lbu commit -d
```
