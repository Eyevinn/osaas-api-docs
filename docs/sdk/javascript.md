The Javascript client libraries for Open Source Cloud are implemented in Typescript and for server-side use with Node.

- [SDK reference documentation](https://js.docs.osaas.io)

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

More examples can be found in the [GitHub repository with examples](https://github.com/EyevinnOSC/client-ts-examples).
