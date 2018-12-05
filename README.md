# rtlwaterfall

At radio spectrum viewer that displays a FFT waterfall as ascii art.
Useful for checking the performance of a remote rtltcp or soapytcp (see 
github.com/roseengineering/soapytcp) server using ssh.

If no length is given for the FFT then it will use the number of
columns of the terminal as the FFT length - if the terminal is
resized the length will be adjusted accordingly.

The floor option defaults to -50 dBFS as the noise floor for
the waterfall.

If the options freq, rate, gain, and auto are set then the changes
are made over the TCP connection using the RTLTCP protocol.

If the float option is set then the TCP stream will be read as
32-bit complex floats.  32-bit IQ streams are used by GNU Radio.


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

For example, the following works well for a 2048khz RTLTCP stream.

```
$ rtlwaterfall --repeat 2000 --freq 99e6 --gain 40
```

![Screenshot](screenshot.png)
