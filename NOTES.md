# radiogaga - notes & references

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