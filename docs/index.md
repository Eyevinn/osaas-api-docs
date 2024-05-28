Welcome to Open Source Cloud API documentation

[Open Source Cloud](https://www.osaas.io) is a cost- effective way to utilize the benefits of open-source software without the upfront costs of hardware or cloud licenses or technical personal. A share of the revenue is shared with the open source creators. With Open Source Cloud, you don't need to worry about installing and configuring software on your own machines, as the software is delivered and managed in the cloud by the Eyevinn experts.

The Open Source Cloud can be scaled up or down as per your needs, providing greater flexibility and adaptability, and at any point the services could be moved to your own control as the software is open and free.

## Getting Started

To access the APIs for the services running in Open Source Cloud you need a Service Access Token (SAT). The SATs are unique for each type of service. To obtain an SAT you will be using the Personal Access Token (PAT) that you have available in the [web console](https://app.osaas.io).

### Example: Acquire an SAT for FAST Engine as a Service

In this example we are using `curl` to show you how to get an SAT for FAST Engine as a Service.

```
curl -X 'POST' \
  'https://token.svc.prod.osaas.io/servicetoken' \
  -H 'accept: application/json' \
  -H 'x-pat-jwt: Bearer <PAT>' \
  -H 'Content-Type: application/json' \
  -d '{
  "serviceId": "channel-engine"
}'
```

The service identifier for the FAST Engine as a Service is `channel-engine`. In response you will get something like this:

```json
{
  "serviceId": "channel-engine",
  "token": "<SAT>",
  "expiry": 1699462522
}
```

The SAT is the value of the `token` in the JSON response above and what you will be using when creating and removing FAST Engine channels.

## Client Libraries

To call the Open Source Cloud API from a programming language you use client libraries. These are officially supported open source client libraries:

### Javascript

- [@osaas/client-core](https://www.npmjs.com/package/@osaas/client-core)
- [@osaas/client-transcode](https://www.npmjs.com/package/@osaas/client-transcode)

## CLI

Open Source Cloud provides a command line tool for communicating with Open Source Cloud. Prerequisite is to have Node installed and then you can install it with NPM (Node package manager).

```
npm install -g @osaas/cli
```

For help

```
osc -h
```