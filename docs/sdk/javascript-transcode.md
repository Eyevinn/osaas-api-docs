The Javascript client libraries for Open Source Cloud are implemented in Typescript and for server-side use with Node.

# Transcode Library

The Transcode library contains high-level functions for video transcoding in Open Source Cloud. It is implemented on top of the core library and some functions implies use of multiple services active at the same time, which is not eligable on the free tier.

## Installation

```
npm install @osaas/client-transcode
```

## Getting started

You need to have a valid context first. See [core library](./javascript.md) for information how that works.

Then you create an Encore Queue Pool. A Queue Pool is a collection of Encore instances. In most cases one queue is sufficient but for large volumes you might want to run jobs in parallell.

```javascript
const pool = new QueuePool({ context: ctx });
await pool.init();
```

When the pool is initiated the Encore instances are created and also visible in the web user interface.

To then transcode a file `https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4` with the default transcoding profile and transfer the resulting files to S3 bucket `s3://dest/myfiles/` you can write.

```javascript
await pool.transcode(
  new URL(
    'https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4'
  ),
  new URL('s3://dest/myfiles/'),
  {}
);
```

It will await until the transcoding and the transfer is completed. Once completed you can delete the pool and instances.

```javascript
await pool.destroy();
```

If you also want to package the transcoded files to streaming files and upload to an S3 origin you add the option `packageDestination`, e.g.

```javascript
await pool.transcode(
  new URL(
    'https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4'
  ),
  new URL('s3://dest/myfiles/'),
  { packageDestination: new URL('s3://myorigin/myfiles/) }
);
```
