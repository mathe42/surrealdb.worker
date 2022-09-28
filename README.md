# SurrealDB in worker!

## WHY?
The main thread is full of stuff that don't need to be there. Also when you have an Application where each client connects via WebSocket to SurrealDB that will be a lot of 
open connections.

This package enables you to use 1 Connection per browser (NOT per tab). All Connection related stuff (basicly most querys) has to be moved into a single config object that lives in the Worker.

> NOTE: If the browser of the user supports SharedWorker it is a good idea to use it!

## Live Querys
This is build with live querys in mind so as soon as they are available they are added here.

## Browser support
This needs the Lock API!
See https://caniuse.com/mdn-api_lock for support.

## Size
Uncompressed (but minified) you add arround 5KB to your page. With gzip or brotli you get that to 1-2KB!

## In worker
```ts
import {setupWorker} from 'surrealdb.worker/worker'

export const config = {
  /** */
}

setupWorker(config).then(v => {
  v(/* surrealdb options */)
})
```

## In client to start worker
```ts
import {strartWorker} from 'surrealdb.worker/worker.setup'

strartWorker(new URL('./path/to/worker/file', import.meta.url))
```

## in client to setup cliet
```ts
import {config} from './path/to/worker/file'
import {setupClient} from 'surrealdb.worker/client'

const client = setupClient<typeof config>()

// For vue
import {vue} from 'surrealdb.worker/framework/vue'
const vueClient = vue<typeof config>(client)
```

## Frameworks
As I will use this with Vue I added a wrapper for that.
I also added a react wrapper but I don't know if that works / what the best practices for that are.

You want to add other frameworks? Feel free to create a PR for this!
