# OpenJpeg-js test

## Bechmark vs. jpx

### Chrome 49.0.2623.112

| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 110.53 | 301.42 | 0.00|
|lossyhdr.dcm.jp2 | 254.20 | 403.42 | 206.01|
|peppers.10.jp2 | 186.56 | 403.35 | 0.49|
|saturn.jpc | 499.50 | 511.34 | 0.00|

FAILS: 860AE501.dcm.jp2

### FF DEV 47.0a2 (2016-04-07)


| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 425.08 | 20.20 | 0.00|
|lossyhdr.dcm.jp2 | 352.66 | 95.77 | 206.01|
|peppers.10.jp2 | 605.59 | 57.25 | 0.49|
|saturn.jpc | 952.16 | 170.68 | 0.00|

FAILS: 860AE501.dcm.jp2

## Notes

### Fails and diff
#### lossyhdr.dcm.jp2

The output from jpx and opj are different.
However, this may actually fix issue [#5](https://github.com/OHIF/image-JPEG2000/issues/5).
More testing required..

#### 860AE501.dcm.jp2

860AE501 fails with OPJ, however this is maybe because OPJ is not configured to handle truncated files?

### download size
* libopenjpg.js + libopenjpeg.js.mem : 480 kb
* jpx.min.js : 17 kb

libopenjpg.js is 20+ times larger and probably takes 20x time to compile by the JS interpreter.
Maybe WebAssembly can help down the line.
