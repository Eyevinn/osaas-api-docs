## Open Source FAST Engine as a Service API

To create and remove channels a REST API is available and API documentation is [available online](https://api-ce.prod.osaas.io/docs). To access the API you need a Service Access Token that you acquire with your [Personal Access Token](../index.md). To request a personal access token or get more information about the service contact [sales@eyevinn.se](mailto:sales@eyevinn.se). If you want to try it out first we have a test environment available that you can use. See further down below on how to get access to the test environment.

## Create a channel from looping a VOD

Create a channel by looping a VOD with this command. Replace `SAT` with the the Service Access Token you have acquire
.

```bash
curl -X 'POST' \
  'https://api-ce.prod.osaas.io/channel' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "mychannel",
  "type": "Loop",
  "url": "https://testcontent.eyevinn.technology/vinn/cmaf/index.m3u8"
}'
```

In return you will get:

```json
{
  "id": "eyevinn-mychannel",
  "name": "mychannel",
  "type": "Loop",
  "url": "https://testcontent.eyevinn.technology/vinn/cmaf/index.m3u8",
  "playback": "https://eyevinn.ce.prod.osaas.io/channels/mychannel/master.m3u8"
}
```

The channel's playback URL is [https://eyevinn.ce.prod.osaas.io/channels/mychannel/master.m3u8](https://web.player.eyevinn.technology/?manifest=https%3A%2F%2Feyevinn.ce.prod.osaas.io%2Fchannels%2Fmychannel%2Fmaster.m3u8)

## Create a channel with ad insertion opportunity

To demonstrate how to insert an opportunity to place ads in a FAST channel you can place a preroll / ad-slate before each VOD. The FAST channel will be decorated with HLS ad tags that a Server-Side Ad Inserter will utilize to replace with ads from the inventory.

```bash
curl -X 'POST' \
  'https://api-ce.prod.osaas.io/channel' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "houseads",
  "type": "Loop",
  "url": "https://testcontent.eyevinn.technology/vinn/cmaf/index.m3u8",
  "opts": {
    "preroll": {
      "url": "https://testcontent.eyevinn.technology/reel/cmaf/index.m3u8",
      "duration": "127"
    }
  }
}'
```

## Create a channel using a webhook

To create a channel that uses a custom webhook you can run the following command.

```bash
curl -X 'POST' \
  'https://api-ce.prod.osaas.io/channel' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "mychannel",
  "type": "WebHook",
  "url": "https://nextvod.dev.eyevinn.technology"
}'
```

Where you would replace the `https://nextvod.dev.eyevinn.technology` with the URL to your webhook. For more information and example of a webhook read the [webhook-plugin documentation](https://fast.docs.eyevinn.technology/plugins/webhook.html).

## Remove a channel

To remove a channel you run the following and replace the `eyevinn-mychannel` with the channel id of your channel.

```bash
curl -X 'DELETE' \
  'https://api-ce.prod.osaas.io/channel/eyevinn-mychannel' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT'
```

## List all your channels

To list all the channels that you have created run the following command. Replace `SAT` with your token.

```bash
curl -X 'GET' \
  'https://api-ce.prod.osaas.io/channel' \
  -H 'accept: application/json' \
  -H 'x-jwt: Bearer SAT'
```

In return you should get something like this.

```json
[
  {
    "id":"eyevinn-houseads",
    "name":"houseads",
    "type":"Loop",
    "url":"https://eyevinn.ce.prod.osaas.io/channels/houseads/master.m3u8"
  },
  {
    "id":"eyevinn-mychannel",
    "name":"mychannel",
    "type":"Loop",
    "url":"https://eyevinn.ce.prod.osaas.io/channels/mychannel/master.m3u8"
    }
]
```

## Test Environment

The address to the API in the test environment is `https://api-ce.stage.osaas.io/docs` and here you can generate a trial-token to try this out. Replace `api-ce.prod.osaas.io` in the instructions above with `api-ce.stage.osaas.io` in the API calls.

### Create trial-token

Generate a trial-token in our demo environment. The trial-token limits you to maximum of 3 channels and running in our test environment. Replace `YOUR_ORG` and `YOUR_EMAIL` in the command below.

```bash
curl -X 'POST' \
  'https://api-ce.stage.osaas.io/token' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "company": "YOUR_ORG",
  "email": "YOUR_EMAIL"
}'
```

In return you get a trial `SAT` that you will be using to create and remove channels in our demo environment.