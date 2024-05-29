## Synopsis

```
osc list <serviceId>
osc create [options] <serviceId> <name> -o [optionKey1=optionValue2] -o [...]
osc remove <serviceId> <name>
```

## Description

List, create and remove service instances.

### Service Instance Options
The service instance options when creating an instance are provided with the option `-o, --instance-options` and as key value pairs (.e.g. `-o key1=value1 -o key2=value2`). For example to create a FAST Channel Engine channel:

```bash
% osc create channel-engine example -o \
    type=Loop \
    url=https://lab.cdn.eyevinn.technology/stswetvplus-promo-2023-5GBm231Mkz.mov/manifest.m3u8 \
    opts.useDemuxedAudio=false \
    opts.useVttSubtitles=false \
    opts.preroll.url=http://maitv-vod.lab.eyevinn.technology/VINN.mp4/master.m3u8 \
    opts.preroll.duration=10500
```

This will be translated to the following JSON payload when creating the instance:

```json
{
  "name": "example",
  "url": "https://lab.cdn.eyevinn.technology/stswetvplus-promo-2023-5GBm231Mkz.mov/manifest.m3u8",
  "opts": {
    "useDemuxedAudio": false,
    "useVttSubtitles": false,
    "preroll": {
      "url": "http://maitv-vod.lab.eyevinn.technology/VINN.mp4/master.m3u8",
      "duration": 10500
    }
  }
}
```
