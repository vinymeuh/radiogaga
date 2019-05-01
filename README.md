# radiogaga - setup for my RaspDAC

The RaspDAC from [Audiophonics](https://www.audiophonics.fr/fr/) is a network audio player build around a Raspberry Pi. There is many software solutions to bring it to life: [Volumeio](https://volumio.org/), [piCorePlayer](https://www.picoreplayer.org/), [RuneAudio](http://www.runeaudio.com/) and others.

**Radiogaga** is my own solution based on [Alpine Linux](https://alpinelinux.org/) and [radiogagad](https://github.com/vinymeuh/radiogagad).

## Installation

1. Clone this repository to your local drive
2. Manually [install Alpine Linux](https://github.com/vinymeuh/radiogaga/blob/master/alpine/README.md) on your SD card
3. Install Ansible

```
~> python -m venv venv
~> source venv/bin/activate
~> pip install -r requirements.txt  
```

4. Setup ssh connectivity for Ansible with ```ansible-playbook radiogaga.yml -t ssh -k```
5. Run ```ansible-playbook radiogaga.yml``` inside this directory
