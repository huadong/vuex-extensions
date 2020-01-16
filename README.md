# Vuex Extensions
Adding Reset and Mixins funtionanity to Vuex

<hr />

[![CircleCI](https://circleci.com/gh/huybuidac/vuex-extensions.svg?style=svg)](https://circleci.com/gh/huybuidac/vuex-extensions) [![npm version](https://badge.fury.io/js/vuex-extensions.svg)](https://badge.fury.io/js/vuex-extensions)

## Install
You can install it via NPM
```console
npm install vuex-extensions
```

or YARN
```console
yarn add vuex-extensions
```

## Usage
#### Creating Vuex.Store
```js
import Vuex from 'vuex'
import { createStore } from 'vuex-extensions'

export default createStore(Vuex.Store, {
  plugins: []
  modules: {}
})
```

#### Store resets to initial State
```js
// Vue Component
this.$store.reset()
```

```js
// Vuex action
modules: {
  sub: {
    actions: {
      logout() {
        this.reset()
      }
    }
  }
}
```

#### Mixins: adding some default getters/mutations/actions to all modules
```js
    const store = createStore(Vuex.Store, {
      modules: {
        sub: {
          namespaced: true,
          state: {
            count: 0
          },
          actions: {
            test: function({ commit }) {
              commit('changeState', { count: 1 })
            }
          }
        }
      },
      mixins: {
        mutations: {
          changeState: function (state, changed) {
            Object.entries(changed)
              .forEach(([name, value]) => {
                state[name] = value
              })
          }
        }
      }
    })
    store.dispatch('sub/test')
```
