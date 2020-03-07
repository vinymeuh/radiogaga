# radiogaga - setup for my RaspDAC

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

The RaspDAC from [Audiophonics](https://www.audiophonics.fr/fr/) is a network audio player build around a Raspberry Pi. There is many software solutions to bring it to life: [Volumeio](https://volumio.org/), [piCorePlayer](https://www.picoreplayer.org/), [RuneAudio](http://www.runeaudio.com/) and others.

**Radiogaga** is my own solution made with :heart:, [Ansible](https://www.ansible.com/), [Alpine Linux](https://alpinelinux.org/) and [radiogagad](https://github.com/vinymeuh/radiogagad).

**Table of Contents**

- [Installation](#Installation)
  - [Bootstrap Alpine Linux](#Bootstrap-Alpine-Linux)
  - [USB Key](#USB-Key)
  - [Finish installation](#Finish-installation)

## Installation

### Bootstrap Alpine Linux

See [raspi-ansible](https://github.com/vinymeuh/raspi-ansible)

### USB Key

Thanks to Alpine Linux the SD Card is mounted read only. To store MPD database and a large music collection, a USB key is used to be mounted read-write.

The USB key preparation is not integrated in playbooks and have to be done manually.

I choose to format the key with F2FS, see [a presentation of F2FS (in french)](https://korben.info/f2fs-systeme-de-fichiers-pense-raspberry-pi-linstaller.html).

```shell
mkfs.f2fs -l USBKEY /dev/sda
```

### Finish installation

```shell
ansible-playbook setup-radiogaga.yml -e target=radiogaga
```

If no errors, enjoy your new [:radio:](https://www.youtube.com/watch?v=azdwsXLmrHE)
