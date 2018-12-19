# rtlwaterfall

![](waterfall.gif)

The following is a radio spectrum analyzer that displays a FFT waterfall as ASCII art.
It communicates with a RTLTCP server to listen to the radio.  It
can also issue RTLTCP commands to control the radio.  For example 
it can change the sampling rate or frequency of the networked radio
using the --rate and --freq options.

The rtlwaterfall program is useful for checking the performance of 
a remotely running rtltcp or soapytcp (see 
github.com/roseengineering/soapytcp) program using say ssh.

If no length is given for the FFT then rtlwaterfall will use the number of
columns in the terminal as the FFT length - if the terminal is
resized the length will be adjusted accordingly.

The --floor option defaults to -50 dB as the noise floor of
the waterfall.  The --ceiling options defaults to 0 dB.

If the --float option is set then the TCP stream will be read as
32-bit floats instead of unsigned bytes.  Complex 32-bit IQ 
streams are used by program such as GNU Radio.  The --word option
supports 16-bit sign integer samples as used by standard IQ WAV files.
Use the --stdin option to run the waterfall over standard input rather
than a server stream.

```
$ rtlwaterfall -h
usage: rtlwaterfall [-h] [--floor FLOOR] [--ceil CEIL] [--length LENGTH]
                    [--repeat REPEAT] [--skip SKIP] [--float] [--word]
                    [--hann] [--host HOST] [--port PORT] [--freq FREQ]
                    [--rate RATE] [--gain GAIN] [--auto] [--quit] [--stdin]
                    [--meter]

optional arguments:
  -h, --help       show this help message and exit
  --floor FLOOR    set the waterfall floor (dB), default -50
  --ceil CEIL      set the waterfall ceiling (dB), default 0
  --length LENGTH  FFT length (bin BW = rate / length)
  --repeat REPEAT  FFT computations to average, default 1
  --skip SKIP      FFT computations to skip, default 0
  --float          read 32-bit float samples
  --word           read 16-bit integer samples
  --hann           use a hann window
  --host HOST      host address of server
  --port PORT      port address of server
  --freq FREQ      set center frequency (Hz)
  --rate RATE      set sample rate (Hz)
  --gain GAIN      set gain (dB)
  --auto           turn on automatic gain
  --quit           issue commands to server, then quit
  --stdin          read samples from standard input
  --meter          add a peak meter to waterfall (-dBFS)
```

For example, the following works well for a 2048KHz RTLTCP stream if you stand back.

```
$ rtlwaterfall --repeat 2000 --freq 99e6 --gain 40
```

Or you can view files.

```
$ rtlwaterfall --repeat 10 --stdin --word --ceiling -55 --floor -80 < Winrad_20090913_202519Z_7020kHz.wav
```

