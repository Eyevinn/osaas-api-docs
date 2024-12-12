The Javascript client libraries for Open Source Cloud are implemented in Typescript and for server-side use with Node.

# Core Library

The core library includes general functionality to create, list and delete service instances or jobs. They are generic and can be used with any type of service in Open Source Cloud.

## Installation

```
npm install @osaas/client-core
```

## Getting started

Assuming that you already have an account at Open Source Cloud you need your Personal Access Token that you find under `Settings` in the web user interface. This is your secret and should never be added in plain text in code.

Required for all functions is to setup a `Context`. A context contains configuration on which environment to access and the Personal Access Token. In normal cases you don't need to change this and you would use the defaults.

To create a context:

```javascript
const ctx = new Context();
```

It will read the Personal Access Token from the environment variable `OSC_ACCESS_TOKEN`. To override the default configuration and read the token from another environment variable, here called `MY_TOKEN`, and connect to the development environment you setup a context as below.

```javascript
const ctx = new Context({ personalAccessToken: process.env.MY_TOKEN })
```

To create, list or remove a service instance you then need to obtain a temporary Service Access Token (SAT) first. This is achieved with the `getServiceAccessToken()`. For example to get an SAT for the service `eyevinn-chaos-stream-proxy` you write.

```javascript
const serviceAccessToken = await ctx.getServiceAccessToken(
  'eyevinn-chaos-stream-proxy'
);
```

With the Service Access Token you can now create a Chaos Stream Proxy instance.

```javascript
const instance = await createInstance(
  ctx,
  'eyevinn-chaos-stream-proxy',
  serviceAccessToken,
  { name: 'example' }
);
console.log(instance.url);
```

To create for example a `eyevinn-docker-retransfer` job you write.

```javascript
const serviceAccessToken = await ctx.getServiceAccessToken(
  'eyevinn-docker-retransfer'
);
const job = await createJob(
  ctx,
  'eyevinn-docker-retransfer',
  serviceAccessToken,
  {
    name: 'example',
    awsAccessKeyId: process.env.AWS_ACCESS_KEY_ID,
    awsSecretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
    cmdLineArgs: 's3://source/myfile.txt s3://dest/'
  }
);
```

And to wait for that job to be completed

```javascript
await waitForJobToComplete(
  ctx,
  'eyevinn-docker-retransfer',
  job.name,
  serviceAccessToken
);
```

## Examples

### Create a Chaos Stream Proxy in stateful mode

```javascript
import { Context, Log, createInstance } from '@osaas/client-core';

const ctx = new Context();

try {
  const serviceAccessToken = await ctx.getServiceAccessToken(
    'eyevinn-chaos-stream-proxy'
  );
  Log().info(serviceAccessToken);

  const instance = await createInstance(
    ctx,
    'eyevinn-chaos-stream-proxy',
    serviceAccessToken,
    { name: 'example', statefulmode: true }
  );
  console.log(instance.url);
} catch (err) {
  Log().error(err);
} 
```

### Launch an SVT Encore transcode job and wait for it to be completed

```javascript
import { Context, Log, createInstance, createFetch } from '@osaas/client-core';
const ctx = new Context();

try {
  // Launch Encore instance
  const encoreToken = await ctx.getServiceAccessToken('encore');
  const instance = await createInstance(
    ctx,
    'encore',
    'example',
    encoreToken
  );

  // Put a transcode job on the Encore queue
  const jobId = Math.random().toString(36).substring(7);
  const encoreJobUrl = new URL('/encoreJobs', instance.url);
  const source = new URL('https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4');
  const dest = new URL('s3://dest/myplace/');
  const data = await createFetch<any>(encoreJobUrl, {
    method: 'POST',
    body: JSON.stringify({
      profile: 'program',
      outputFolder: `/usercontent/${jobId}`,
      baseName: jobId,
      inputs: [
        {
          type: 'AudioVideo',
          uri: source.toString()
        }
      ]
    }),
    headers: {
      'x-jwt': `Bearer ${encoreToken}`,
      'Content-Type': 'application/json'
    }
  });
  const encoreJob = JSON.parse(data);
  // Poll job resource endpoint until status is completed
  const job = await waitForEncoreJobToComplete(
    new URL(encoreJobUrl.toString() + '/' + encoreJob.id),
    encoreToken
  );

} catch (err) {
  Log().error(err);
}
```