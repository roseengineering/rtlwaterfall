# rtlwaterfall

![](screenshot.png)

A radio spectrum viewer that displays a FFT waterfall as ASCII art.
It communicates with a RTLTCP server to read the radio signal over TCP.  It
can also issue RTLTCP commands to control the radio.  For example 
it can change the sampling rate or frequency of the networked radio
using the rate and freq options.
The rtlwaterfall program is useful for checking the performance of 
a remotely running rtltcp or soapytcp (see 
github.com/roseengineering/soapytcp) program using say ssh.

If no length is given for the FFT then rtlwaterfall will use the number of
columns in the terminal as the FFT length - if the terminal is
resized the length will be adjusted accordingly.
The floor option defaults to -50 dBFS as the noise floor of
the waterfall.  0 dBFS is considered the max value.
If the float option is set then the TCP stream will be read as
32-bit floats instead of unsigned bytes.  Complex 32-bit IQ 
streams are used by program such as GNU Radio.

```
$ rtlwaterfall -h
usage: rtlwaterfall [-h] [--floor FLOOR] [--length LENGTH] [--repeat REPEAT]
                    [--skip SKIP] [--float] [--host HOST] [--port PORT]
                    [--freq FREQ] [--rate RATE] [--gain GAIN] [--auto]
                    [--quit]

optional arguments:
  -h, --help       show this help message and exit
  --floor FLOOR    set the waterfall floor (dBFS)
  --length LENGTH  FFT length (bin BW = rate / length)
  --repeat REPEAT  FFT computations to average
  --skip SKIP      FFT computations to skip
  --float          read 32-bit float samples
  --host HOST      host address of server
  --port PORT      port address of server
  --freq FREQ      set center frequency (Hz)
  --rate RATE      set sample rate (Hz)
  --gain GAIN      set gain (dB)
  --auto           turn on automatic gain
  --quit           quit, no waterfall
```

For example, the following works well for a 2048KHz RTLTCP stream if you stand back.

```
$ rtlwaterfall --repeat 2000 --freq 99e6 --gain 40
```

