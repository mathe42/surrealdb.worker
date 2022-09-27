# SurrealDB in worker!

## Browser support
This needs the Lock API!
See https://caniuse.com/mdn-api_lock for support.


## In worker
```ts
import {setupWorker} from './worker.ts'

export const config = {
  /** */
}

setupWorker(config).then(v => {
  v(/* surrealdb options */)
})
```

## In client to start worker
```ts
import {strartWorker} from './worker.setup.ts'

strartWorker(new URL('./path/to/worker/file', import.meta.url))
```

## in client to setup cliet
```ts
import {config} from './path/to/worker/file'
import {setupClient} from './client.ts'

const client = setupClient<typeof config>()

// For vue
import {vue} from './vue.ts'
const vueClient = vue<typeof config>(client)
```

