## Synopsis

```
osc [global-options] compare vmaf <reference> <distorted> <result-bucket>
```

## Description

Compare two video files on an S3 bucket and store the result on another S3 bucket.

## Example using VMAF

Provide AWS credentials as environment variables for the S3 bucket accesses.

```bash
% export OSC_ACCESS_TOKEN=<your-secret-pat>
% export AWS_ACCESS_KEY_ID=<aws-access-key-id>
% export AWS_SECRET_ACCESS_KEY=<aws-secret-access-key>
% osc compare vmaf \
    s3://video/reference.mp4 \
    s3://video/distorted.mp4 \
    s3://result/vmaf/
```
