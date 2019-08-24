# radiogaga - setup for my RaspDAC

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

The RaspDAC from [Audiophonics](https://www.audiophonics.fr/fr/) is a network audio player build around a Raspberry Pi. There is many software solutions to bring it to life: [Volumeio](https://volumio.org/), [piCorePlayer](https://www.picoreplayer.org/), [RuneAudio](http://www.runeaudio.com/) and others.

**Radiogaga** is my own solution based on [Alpine Linux](https://alpinelinux.org/) and [radiogagad](https://github.com/vinymeuh/radiogagad).

## Installation

1. Clone this repository to your local drive
2. Manually [install Alpine Linux](https://github.com/vinymeuh/radiogaga/blob/master/alpine/README.md) on your SD card
3. Install Ansible

```
~> cd ansible
~> python -m venv venv
~> source venv/bin/activate
~> pip install -r requirements.txt  
```

4. Setup ssh connectivity for Ansible

```
~> cd ansible
~> ansible-playbook install.yml -t ssh -k
```

Avahi is not install by default by Alpine Linux so it should be necessary to adapt **ansible_host** in [inventory](https://github.com/vinymeuh/radiogaga/blob/master/inventory).

5. Run the main playbook

```
~> cd ansible
~> ansible-playbook install.yml
```

Is it possible to run only a specific set of tasks using tags. See ```ansible-playbook install.yml --list-tags``` for availables tags.
