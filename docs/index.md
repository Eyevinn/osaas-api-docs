Welcome to Eyevinn Open Source Cloud API documentation

## Getting Started

To access the APIs for the services running in Eyevinn Open Source Cloud you need a Service Access Token (SAT). The SATs are unique for each type of service. To obtain an SAT you will be using the Personal Access Token (PAT) that you have previously received by your sales representative at Eyevinn.

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