# radiogaga devnotes - disable Raspberry HDMI at boot

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
