当我们的组件需要提供给第三方使用时，我们需要使用`define`函数将其转换为Web Components。此时定义和使用的方式和平常开发JSX组件不同。

### 定义方式如下：

```js
// component-a.js
import zoe, { Component, define } from '@zero/zoe'

function B () {
  return 456
}

class A extends Component {
  static elementName = 'component-a'

  render() {
    return <B />
  }
}

define(A)
```

> [!NOTE]
> 只有最外层组件需要使用define定义，内部组件(如：B)可以正常使用。

### 对于使用方：

**vue**
```vue
<template>
  <div id="app">
    <component-a></component-a>
  </div>
</template>

<script>
import 'component-a.js'

export default {
  data() {
    return {}
  },
  name: 'App',
}
</script>
```

**react**
```js
import React from 'react'
import 'component-a.js'

class App extends React.Component {
  state = {}

  render () {
    return (
      <div>
        <component-a></component-a>
      </div>
    )
  }
}
```

对外使用的Web Components只支持字符串属性，对于非字符串类型会进行类型转换

```html
<component-a type='字符串'></component-a>
```

Web Components通过`attributeChangedCallback`监听属性的变化，需要注意的是你必须监听这个属性，以通过定义静态函数`observedAttributes()`的get函数来实现。

`observedAttributes()`函数体内包含一个return语句，返回一个数组，包含了需要监听的属性

> [!NOTE]
> 1、attributeChangedCallback 会在组件初始化之前执行一次
>
> 2、Web Components的属性直接通过标签传入，所以无法通过this.props获取，推荐放入state中使用

```js
import zoe, { define, Component } from '@zero/zoe'

class HelloWorld extends Component {
  static elementName = 'hello-world'
  static get observedAttributes () {
    return ['type'] // 返回需要监听的属性
  }

  state = {
    type: '',
  }

  attributeChangedCallback (name, oldVal, newVal) {
    // 在组件初始化之前和每次属性变化时都会执行一次
    this.setState({
      [name]: newVal, // 拿到新的属性值后放入state中使用
    })
  }

  render () {
    const { type } = this.state
    return (
      <i>{type}</i>
    )
  }
}

define(HelloWorld)
```

使用方式
```html
<hello-world type='red'></hello-world>
```

### 自定义事件
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
