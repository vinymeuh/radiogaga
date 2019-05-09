# radiogaga - notes & references

## Raspberry Pi

### Disable HDMI at boot

By default:

```
radiogaga:/opt/vc/bin# ./tvservice -s
state 0x120006 [DVI DMT (82) RGB full 16:9], 1920x1080 @ 60.00Hz, progressive
```

With ```hdmi_ignore_hotplug=1``` & ```hdmi_ignore_composite=1```

```
radiogaga:/opt/vc/bin# ./tvservice -s
state 0x120001 [TV is off]
```

References:

* [add option in config.txt to disable video out](https://github.com/raspberrypi/firmware/issues/352#issuecomment-169455388)
* [Disable video via tvservice vs vcgencmd](https://github.com/raspberrypi/userland/issues/447)

## Alpine Linux boot optimization

### bootchard

To enable **bootchartd**, add option ```chart``` to ```cmdline.txt```.

After boot, retrieve ```/var/log/bootchart.tgz```. To generate a PNG from this, we need [pythonchartgui](https://github.com/xrmx/bootchart):

```
$ apk add python2 py2-cairo
$ git clone https://github.com/xrmx/bootchart
$ cd bootchart
$ cp pythonchartgui/main.py.in pythonchartgui/main.py
$ ./pythonchartgui.py bootchart.tgz
```

References:

* [Alpine boot process on the Raspberry Pi](https://pi3g.com/2019/01/10/alpine-boot-process-on-the-raspberry-pi/)
* [Debugging the Alpine boot process](https://pi3g.com/2019/01/22/debugging-the-alpine-boot-process/)
* [Bootchart](https://elinux.org/Bootchart)

## Samba

### Disable printing

```
load printers = no
printing = bsd
printcap name = /dev/null
disable spoolss = yes
```

### General Samba optimization and performance tuning

1. Network socket options: ```socket options = TCP_NODELAY IPTOS_LOWDELAY```
2. Enable sendfile: ```use sendfile = true```

References:

* [Optimize Samba](https://calomel.org/samba_optimize.html)
* [Fix Samba read & write performance issues](https://coderwall.com/p/2ufa0g/fix-samba-read-and-write-performance-issues)
* [Make Samba Go Faster - use sendfile](https://wiki.amahi.org/index.php/Make_Samba_Go_Faster#use_sendfile)

### The macOS compatibility nightmare

By default, samba shares are unusables from macOS (10.12.6): Finder is very very slow to display files and connection is very unstable. Enable VFS module **vfs_fruit** resolves the problem.

```
ea support = yes
vfs objects = fruit streams_xattr
```

References:

* [vfs_fruit](https://www.mankier.com/8/vfs_fruit)
* [AFP vs SMB Performance](https://discussions.apple.com/thread/7674819)

## F2FS

* [A presentation of F2FS (in french)](https://korben.info/f2fs-systeme-de-fichiers-pense-raspberry-pi-linstaller.html)