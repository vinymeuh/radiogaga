# radiogaga - setup for my RaspDAC

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

The RaspDAC from [Audiophonics](https://www.audiophonics.fr/fr/) is a network audio player build around a Raspberry Pi. There is many software solutions to bring it to life: [Volumeio](https://volumio.org/), [piCorePlayer](https://www.picoreplayer.org/), [RuneAudio](http://www.runeaudio.com/) and others.

**Radiogaga** is my own solution based made with :heart:, [Ansible](https://www.ansible.com/), [Alpine Linux](https://alpinelinux.org/) and [radiogagad](https://github.com/vinymeuh/radiogagad).

**Table of Contents**

- [Install Ansible](#Install-Ansible)
- [Configuration](#Configuration)
- [Installation](#Installation)
  - [Bootstrap Alpine Linux](#Bootstrap-Alpine-Linux)
  - [Finish installation](#Finish-installation)
- [Backup & Restore](#Backup-&-restore)

## Install Ansible

First of all, clone this repository to your local drive.

Then assuming you already have a working Python interpreter:

```
~> cd ansible
~> python -m venv venv
~> source venv/bin/activate
~> pip install -r requirements.txt  
```

## Playbooks configuration

By default, playbooks are run using configuration defined in ```environments/radiogaga```:

* ```hosts``` file which defined Ansible connectivity to Raspberry Pi
* ```group_vars/all``` file for playbooks's configuration

You can use a different configuration using the ```-i``` flag of the ```ansible-playbook``` command line.

```
~> ansible-playbook -i environments/radiotest ...
```

## Installation

### Bootstrap Alpine Linux

The playbook **bootstrap.yml** download the Alpine Linux distribution, extracts it on the SD Card and performs minimal setup to be able to connect remotely to the Raspberry Pi just after the first boot.

Network configuration is defined by following parameters

| Parameter | Description |
| --- | --- |
| bootstrap.use_dhcp | note that it is better to use static IP to speed up boot time |
| boostrap.ip | mandatory if bootstrap.use_dhcp is set to False |
| boostrap.netmask | mandatory if bootstrap.use_dhcp is set to False |
| boostrap.gateway | mandatory if bootstrap.use_dhcp is set to False |

Moreoever to be able to connect as root using ssh we add a ```TrustedUserCAKeys``` in ```sshd_config```.

Insert the SD card and check that parameter ```boostrap.mount_point``` point to its mount point.

```
~> ansible-playbook bootstrap.yml -t initialize
```

Eject the media and use it to boot the Raspberry Pi.

We should be able to connect remotely as root using ssh to finish the Alpine setup.

```
radiogaga:~# cd /media/mmcblk0p1
radiogaga:~# setup-alpine -f setup.answer
# Accepts all defaults choices
radiogaga:~# rm /etc/runlevels/default/bootstrap-sshd
radiogaga:~# apk update
radiogaga:~# apk add python3
radiogaga:~# lbu commit -d
radiogaga:~# reboot
```

After reboot we should be able to ping the Raspberry Pi with ansible.

```
~> ansible -m ping '*' --one-line
radiogaga | SUCCESS => {"changed": false,"ping": "pong"}
```

If everything is fine the harder is done :champagne:.

### Finish installation

All remaining tasks are handled by the playbook **install.yml**.

```
~> ansible-playbook install.yml
```

If no errors, enjoy your new [:radio:](https://www.youtube.com/watch?v=azdwsXLmrHE)

## Backup & Restore

