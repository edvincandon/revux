
# Revue2
Based on Revue, use Redux with Vue.js seamlessly
> We were not satisfied with the way the original Revue worked internally.

# Installation
Install via NPM: `npm i --save revue2`

# Getting started
> Work in Progress

**store.js**

Create your redux store:
```js
import {createStore} from 'redux'
import reducer from './reducer'

const store = createStore(reducer)

export default store
```

**index.js**

Instantiate Revue2 in your root's component data function as **store**
```js
import Vue from 'vue'
import Revue from 'revue2'
import store from './store'
import main from './main.vue'

Vue.use(Revue) // !!!


const app = new Vue({
  el: '#app',
  render: h => h(main),
  data: function () {
    return {
      store: new Revue(store)
    }
  }
})
```

**main.vue**

Use the `$connect` method to map state to $data and map actions to dispatch.
Here our state looks something like `{ status: 'foobar' }`

**Be sure to declare your mapped $data properties in your component's data definition for them to be reactive**

```js
<template>{{status}}</template>

<script>
  import * as actions from './actions'

  const mapState = state => {
    const { status } = state // deeply nested state support as well
    return {
      status // must match data property
    }
  })

  const mapDispatch = actions

  export default {
    name: 'playButton',
    data () {
      return {
        status: null // define it to be reactive
      }
    },
    created () {
      this.$connect(mapState, mapDispatch)
    }
  }
</script>
```
