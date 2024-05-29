## Synopsis

```
osc transcode [options] <source> <dest>
```

## Description

Transcode a media file to an ABR fileset and store on an S3 bucket. Requires the capability of running 2 active services in Open Source Cloud at the same time which implies that you need to be on a paid tier.

## Example

Provide AWS credentials as environment variables for the S3 bucket accesses.

```bash
% export OSC_ACCESS_TOKEN=<your-secret-pat>
% export AWS_ACCESS_KEY_ID=<aws-access-key-id>
% export AWS_SECRET_ACCESS_KEY=<aws-secret-access-key>
% osc transcode \
  https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4 \
  s3://lab-testcontent-store/birme/
```
