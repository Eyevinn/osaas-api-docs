The Javascript client libraries for Open Source Cloud are implemented in Typescript and for server-side use with Node.

# Open Media Web Services

This library provides high-level functions for web services in Eyevinn Open Source Cloud for media services.

## Installation

```
npm install @osaas/client-transcode
```

## Getting started: VOD

In this example we will create a video on-demand package for streaming using available open web services and the `client-transcode` library.

You need to have a valid context first. See [core library](./javascript.md) for information how that works.

```javascript
const ctx = new Context();
```

Then we will create a pipeline of open web services that we will need.

```javascript
const pipeline = await createVodPipeline('sdkexample', ctx);
```

This will create an SVT Encore instance and an Encore Packager instance and connect these using a shared Redis-compatible queue. In addition it will create a storage for the VOD packages. This means you need to be at least on the Business plan as this requires more than two open web services.

Now we can create a VOD package with the help of this pipeline. 

```javascript
const vod = await createVod(pipeline, 'https://testcontent.eyevinn.technology/mp4/VINN.mp4', ctx);
console.log(vod);
```

Putting these all together we have:

```javascript
import { Context } from '@osaas/client-core';
import {
  createVod,
  createVodPipeline
} from '@osaas/client-transcode';

async function main() {
  const ctx = new Context();
  const pipeline = await createVodPipeline('sdkexample', ctx);
  const vod = await createVod(pipeline, 'https://testcontent.eyevinn.technology/mp4/VINN.mp4', ctx);
  console.log(vod);
}

main();
```