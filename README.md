# OpenJpeg-js test

## Bechmark vs. jpx
When compiles with
```
emcc bin/libopenjpeg-js.bc -o dist/libopenjpeg.js \
     --post-js bin/JSOpenJPEGDecoder_post-js.js \
     --memory-init-file 0 \
     -s TOTAL_MEMORY=500000000 \
     -s NO_FILESYSTEM=1 \
     -O3
```

### Chrome 49.0.2623.112 - Linux VM

| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 83.87 | 275.00 | 0.00|
|lossyhdr.dcm.jp2 | 245.88 | 409.00 | 206.01|
|peppers.10.jp2 | 178.30 | 439.00 | 0.50|
|saturn.jpc | 482.78 | 506.00 | 0.00|
|860AE501.dcm.jp2 | 1849.93 | 1297.00 | 0.00|

#### with "-s ASM_JS=2"

| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 83.29 | 176.00 | 0.00|
|lossyhdr.dcm.jp2 | 268.40 | 348.00 | 206.01|
|peppers.10.jp2 | 168.16 | 369.00 | 0.50|
|saturn.jpc | 479.16 | 687.00 | 0.00|
|860AE501.dcm.jp2 | 1849.80 | 2129.00 | 0.00|


### FF DEV 47.0a2 (2016-04-07) - Linux VM

| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 139.85 | 18.00 | 0.00|
|lossyhdr.dcm.jp2 | 252.31 | 94.00 | 206.01|
|peppers.10.jp2 | 283.37 | 51.00 | 0.50|
|saturn.jpc | 464.31 | 171.00 | 0.00|
|860AE501.dcm.jp2 | 1282.50 | 810.00 | 0.00|

### IE 11.162 - WIN10

| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 398.76 | 175.00 | 0.00|
|lossyhdr.dcm.jp2 | 1241.58 | 869.00 | 206.01|
|peppers.10.jp2 | 1168.25 | 286.00 | 0.50|
|saturn.jpc | 2072.94 | 1080.00 | 0.00|
|860AE501.dcm.jp2 | 17152.18 | 3455.00 | 0.00|

### Edge 25 - WIN10

| file | jpx time (ms) | opj time (ms) | diff per pixel |
|----------|-------------:|------:|------:|
|cameraman.lossless.jp2 | 52.50 | 50.00 | 0.00|
|lossyhdr.dcm.jp2 | 158.94 | 236.00 | 206.01|
|peppers.10.jp2 | 121.42 | 196.00 | 0.50|
|saturn.jpc | 347.09 | 362.00 | 0.00|
|860AE501.dcm.jp2 | 1776.97 | 1293.00 | 0.00|

## Notes

### diff
#### lossyhdr.dcm.jp2

The output from jpx and opj are different.
However, this may actually fix issue [#5](https://github.com/OHIF/image-JPEG2000/issues/5).
More testing required..

### download size
* libopenjpg.js : 480 kb
* jpx.min.js : 17 kb

libopenjpg.js is 20+ times larger and probably takes 20x time to compile by the JS interpreter.
Maybe WebAssembly can help down the line.
