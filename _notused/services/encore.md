## Open Source SVT Encore as a Service API

[SVT Encore](https://github.com/svt/encore) is a scalable video transcoding tool, built on Open-Source giants like FFmpeg and Redisson. Encore was created to scale, and abstract the transcoding power of FFmpeg, and to offer a simple solution for Transcoding- as-a-Service. Encore is aimed at the user that needs a scalable video transcoding tool - for example, as a part of their VOD (Video On Demand) transcoding pipeline.

To create and remove Encore queues a REST API is available and API documentation is [available online](https://api-encore.prod.osaas.io/docs). To access the API you need a Service Access Token that you acquire with your [Personal Access Token](../index.md). To request a personal access token or get more information about the service contact [sales@eyevinn.se](mailto:sales@eyevinn.se). If you want to try it out first we have a test environment available that you can use. See further down below on how to get access to the test environment.

## Start an Encore queue

Spin up an Encore queue (instance) called `test`.

```bash
curl -X 'POST' \
  'https://api-encore.prod.osaas.io/encoreinstance' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "test"
}'
```

In return you will get something like this.

```json
[
  {
    "name": "test",
    "url": "https://<tenantId>-test.encore.prod.osaas.io/",
    "profilesUrl": "",
    "resources": {
      "license": {
        "url": "https://api-encore.prod.osaas.io/license"
      },
      "enqueueJob": {
        "url": "https://<tenantId>-test.encore.prod.osaas.io/encoreJobs",
        "method": "POST"
      },
      "listJobs": {
        "url": "https://<tenantId>-test.encore.prod.osaas.io/encoreJobs",
        "method": "GET"
      }
    }
  }
]
```

URL to the created instance in this case is then `https://<tenantId>-test.encore.prod.osaas.io/`. To access the OpenAPI endpoint as json:

```bash
curl -v -H 'x-jwt: Bearer SAT' "https://<tenantId>-test.encore.prod.osaas.io/v3/api-docs/"
```

or as yaml:

```bash
curl -v -H 'x-jwt: Bearer SAT' "https://<tenantId>-test.encore.prod.osaas.io/v3/api-docs.yaml"
```

## Enqueue a job

To put a job on the created queue

```bash
curl -X 'POST' \
  'https://<tenantId>-test.encore.prod.osaas.io/encoreJobs' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT' \
  -H 'Content-Type: application/json' \
  -d '{
  "profile": "program",
  "outputFolder": "/usercontent/demo",
  "baseName": "demo_",
  "inputs": [
    {
      "uri": "https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4",
      "type": "AudioVideo"
    }
  ],
  "duration": 5,
  "priority": 0
}'
```

## Remove an Encore queue

To remove an Encore queue (instance) that you created and named `test`.

```bash
curl -X 'DELETE' \
  'https://api-encore.prod.osaas.io/encoreinstance/test' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT'
```

## Test Environment

The address to the API in the test environment is `https://api-encore.stage.osaas.io/docs` and here you can generate a trial-token to try this out. Replace `api-encore.prod.osaas.io` in the instructions above with `api-encore.stage.osaas.io` in the API calls.

### Create trial-token

Generate a trial-token in our demo environment. The trial-token limits you to maximum of 3 queues and running in our demo environment. Replace `YOUR_ORG` and `YOUR_EMAIL` in the command below.

```bash
curl -X 'POST' \
  'https://api-encore.stage.osaas.io/token' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "company": "YOUR_ORG",
  "email": "YOUR_EMAIL"
}'
```

In return you get a trial `SAT` that you will be using to create and remove queues in our demo environment.