Welcome to Eyevinn Open Source Cloud API documentation

[Eyevinn Open Source Cloud](https://www.osaas.io) (OSC) reduces the barrier to get start with open source by reducing the barrier for an open source creator to offer their software as a service. Generated revenue is shared with the open source creator.

Our goal is to not be evil and to provide the creators with an additional income stream for their projects. Read [Our Pledge to the community](https://docs.osaas.io/osaas.wiki/Our-Pledge.html).

## Getting Started

To access the APIs for the services running in Eyevinn Open Source Cloud you need a Service Access Token (SAT). The SATs are unique for each type of service. To obtain an SAT you will be using the Personal Access Token (PAT) that you have available in the [web console](https://app.osaas.io).

### Example: Acquire an SAT for FAST Engine as a Service (using HTTP)

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

### Example: Acquire an SAT for FAST Engine as a Service (using OSC command line tool)

You can also use the OSC command line tool to obtain a service access token (SAT) for a service, in this example we are requesting a token for the FAST Engine as a Service (channel-engine)
```bash
% export OSC_ACCESS_TOKEN=<PAT>
% npx -y @osaas/cli service-access-token channel-engine
<SAT>
```

## Client Libraries

To call the Open Source Cloud API from a programming language you use client libraries. These are officially supported open source client libraries:

### Javascript

- [@osaas/client-core](https://www.npmjs.com/package/@osaas/client-core)
- [@osaas/client-services](https://www.npmjs.com/package/@osaas/client-services)
- [@osaas/client-transcode](https://www.npmjs.com/package/@osaas/client-transcode)

### Golang

- [EyevinnOSC/client-go](https://github.com/EyevinnOSC/client-go)

## CLI

Eyevinn Open Source Cloud provides a command line tool for communicating with Open Source Cloud. Prerequisite is to have Node installed and then you can install it with NPM (Node package manager).

```
% npm install -g @osaas/cli
```

For help

```
% osc -h
```

If you don't want to install it and just run it you can use `npx` given that you have Node and NPM installed.

```
% npx @osaas/cli -v
4.3.1
```