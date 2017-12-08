# hydux-react
React enhancer for hydux.

## Install
```sh
yarn add hydux-react hydux # or npm i hydux-react hydux
```

## Usage


```js
import _app from 'hydux'
import withPersist from 'hydux/lib/enhancers/persist'
import withReact, { React } from 'hydux-react'

// let app = withPersist<State, Actions>({
//   key: 'my-counter-app/v1'
// })(_app)

// use built-in 1kb picodom to render the view.
let app = withReact()(_app)

if (process.env.NODE_ENV === 'development') {
  // built-in dev tools, without pain.
  const devTools = require('hydux/lib/enhancers/devtools').default
  const logger = require('hydux/lib/enhancers/logger').default
  const hmr = require('hydux/lib/enhancers/hmr').default
  app = logger()(app)
  app = devTools()(app)
  app = hmr()(app)
}

export default app({
  init: () => { count: 1 },
  actions: {
    down: () => state => ({ count: state.count - 1 }),
    up: () => state => ({ count: state.count + 1 })
  },
  view: (state: State) => (actions: Actions) =>
    <div>
      <h1>{state.count}</h1>
      <button onclick={actions.down}>–</button>
      <button onclick={actions.up}>+</button>
    </div>
})
```

## Counter App

```sh
git clone https://github.com/hydux/hydux-react.git
cd examples/counter
yarn # or npm i
npm start
```

Now open http://localhost:8080 and hack!

##` License

MIT