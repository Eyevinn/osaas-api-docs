## Synopsis

```
osc packager [options] <source> <dest>
```

## Description

Create streaming package from ABR bundle on S3 source bucket and store on an S3 destination bucket.

## Example

Create an HLS and MPEG-DASH streaming package from video `snaxax_x264*.mp4` and audio `snaxax_STEREO.mp4` on `s3://lab-testcontent-store/birme` and store it in `s3://lab-testcontent-store/birme/vod`

```bash
% export OSC_ACCESS_TOKEN=<your-secret-pat>
% export AWS_ACCESS_KEY_ID=<aws-access-key-id>
% export AWS_SECRET_ACCESS_KEY=<aws-secret-access-key>
% osc packager s3://lab-testcontent-store/birme s3://lab-testcontent-store/birme/vod \
-a snaxax_STEREO.mp4 \
-v snaxax_x264_324.mp4 \
-v snaxax_x264_1312.mp4 \
-v snaxax_x264_2069.mp4 \
-v snaxax_x264_3100.mp4
```
