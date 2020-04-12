# radiogaga - an Ansible role to setup my RaspDAC

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

The RaspDAC from [Audiophonics](https://www.audiophonics.fr/fr/) is a network audio player build around a Raspberry Pi. There is many software solutions to bring it to life: [Volumeio](https://volumio.org/), [piCorePlayer](https://www.picoreplayer.org/), [RuneAudio](http://www.runeaudio.com/) and others.

**Radiogaga** is my own solution made with [Ansible](https://www.ansible.com/), [Alpine Linux](https://alpinelinux.org/), [radiogagad](https://github.com/vinymeuh/radiogagad) and :heart:.

See [raspi-ansible](https://github.com/vinymeuh/raspi-ansible/blob/master/deploy-radiogaga.yml) for the playbook used to manage my RaspDAC.

## Requirements

Thanks to Alpine Linux the SD Card is mounted read only. To store MPD database and a large music collection, a USB key can optionaly be used to be mounted read-write.

The USB key format have to be done manually, I choose to use F2FS:

```shell
mkfs.f2fs -l USBKEY /dev/sda
```

## Role Variables

```yaml
dac: "SabreES9023"
```

The type of DAC in the RaspDAC.

```yaml
mpd_rootdir: "/etc/mpd"
```

Directory for mpd database and Playlists & Music directories, overriden when ```usbkey_enabled: true```.

```yaml
playlists: ""
```

List of specifications for playlists in format: ```{file: "...", name: "...", url: "http://..."}```.

```yaml
radiogagad_enabled: true
radiogagad_configuration: ""
```

Controls radiogagad install and setup:

* when set to false, only a init script to start mpd play is installed.
* otherwise installs last published version of [radiogagad](https://github.com/vinymeuh/radiogagad).

```radiogagad_configuration``` can be used to define content of ```/etc/radiogagad.yml``` (see [radiogagad.yml.template](https://github.com/vinymeuh/radiogagad/blob/master/radiogagad.yml.template) for file format).

```yaml
rc_parallel: false
```

Enable OpenRC parallel boot.

```yaml
usbkey_enabled: true
usbkey_label: ""
usbkey_mnt: ""
```

Enables USB key use and defines filesystem label and mount point.

```yaml
wifi_enabled: false
```

Controls wifi activation in firmware.
