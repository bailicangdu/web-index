## 自定义事件
组件可通过`dispatchCustomEvent`方法发送自定义事件与外部进行交互。

```js
dispatchCustomEvent(name, [detail], [bubbles], [cancelable])

@param name {String 必填参数} 事件名称
@param detail {Object 可选参数} detail会放在事件参数detail中
@param bubbles {Boolean 可选参数} 是否冒泡，默认false
@param cancelable {Boolean 可选参数} 能否被取消，默认false，为true时可以通过e.preventDefault()阻止其行为
```

**定义方式**
```js
// component-a.js
import zoe, { Component, define } from '@zero/zoe'

class A extends Component {
  static elementName = 'component-a'

  handleClick = () => {
    this.dispatchCustomEvent('myevent', { msg: 'xxxx' })
  }

  render() {
    return <div onClick={this.handleClick}><div>
  }
}

define(A)
```

**使用方式：**

**vue**
```vue
<template>
  <div id="app">
    <component-a v-on:myevent='handleMyEvent'></component-a>
  </div>
</template>

<script>
import 'component-a.js'

export default {
  data() {
    return {}
  },
  name: 'App',
  methods: {
    handleMyEvent (e) {
      console.log(e.detail) // { msg: 'xxxx' }
    }
  }
}
</script>
```

**react**

react不支持使用on开头绑定自定义事件，所以需要我们主动绑定：

```js
import React from 'react'
import 'component-a.js'

class App extends React.Component {
  state = {}

  componentDidMount () {
    this.refs.coma.addEventListener('myevent', (e) => {
      console.log(e.detail) // { msg: 'xxxx' }
    })
  }

  render () {
    return (
      <div>
        <component-a ref='coma'></component-a>
      </div>
    )
  }
}
```
