## Synopsis

```
osc transcribe [options] <source>
```

## Description

Transcribe an audio or video file using [Subtitle Generator](https://app.osaas.io/dashboard/service/eyevinn-auto-subtitles) in Open Source Cloud.

## Prerequisites

OpenAI API key

## Example

In this example the OpenAI API key is stored in a secret called `openaikey` which is the recommended way to work with sensitive data in the platform.

```bash
% export OSC_ACCESS_TOKEN=<your-secret-pat>
% export OPENAI_API_KEY="{{secrets.openaikey}}
% osc transcribe https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4
WEBVTT

00:00:00.000 --> 00:00:05.360
Probably the most interesting challenge of the 21st century.

00:00:05.360 --> 00:00:07.200
Streaming tech TV plus.

00:00:07.200 --> 00:00:08.200
Money.

00:00:08.200 --> 00:00:10.420
Money, money, money, money.

00:00:10.420 --> 00:00:13.700
Great streaming tech talks curated from all over the world.

00:00:13.700 --> 00:00:18.280
They said they would prefer blur if I was going like this.
...
```

And in this example we output to format SRT

```bash
% osc transcribe -f srt https://testcontent.eyevinn.technology/mp4/stswe-tvplus-promo.mp4
1
00:00:00,000 --> 00:00:04,480
probably the most interesting challenge of the 21st century.

2
00:00:04,480 --> 00:00:10,100
StreamingTech TV Plus Money, money, money, money, money.

3
00:00:10,100 --> 00:00:13,460
Great streaming tech talks curated from all over the world.
...
```
