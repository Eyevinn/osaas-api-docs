The Javascript client libraries for Open Source Cloud are implemented in Typescript and for server-side use with Node.

# Open Database Web Services

This library provides high-level functions for web services in Eyevinn Open Source Cloud for database services.

## Installation

```
npm install @osaas/client-services
```

## Getting started: Redis database

You need to have a valid context first. See [core library](./javascript.md) for information how that works.

In this example we will create a Valkey database that provides a high-performance key-value data store with a Redis compatible interface. We will create the database and then obtain the Redis URL and connect with it using the `ioredis` client library.

```javascript
import { Context } from '@osaas/client-core';
import { ValkeyDb } from '@osaas/client-db';
import Redis from 'ioredis';

async function main() {
  const context = new Context();
  try {
    const db = new ValkeyDb({ context, name: 'mydb' });
    await db.init();
    const redisUrl = await db.getRedisUrl();

    const client = new Redis({ host: redisUrl.hostname, port: redisUrl.port });
  } catch (err) {
    Log().error(err);
  }
}

main();
```