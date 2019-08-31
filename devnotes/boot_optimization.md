# radiogaga devnotes - Alpine Linux boot optimization

## bootchard

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
