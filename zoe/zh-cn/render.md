自定义渲染方式分两种：函数式组件、html标签

正常情况下默认渲染函数式组件，比如：

```js
import zoe, { Component } from '@zero/zoe'
import styleA from '组件A的样式文件.css'
import styleB from '组件B的样式文件.css'

// 组件A
class A extends Component {
  static elementName = 'component-a'
  static style = styleA
  
  render() {
    return <span>123</span>
  }
}

// 组件B
function B () {
  return <span>456</span>
}

B.style = styleB
B.elementName = 'component-b'

class Home extends Component {
  render () {
    return (
      <div>
        <A /> // 组件A、B通过函数的形式使用
        <B />
      </div>
    )
  }
}
```

上述A、B两个组件的使用方式和我们平常开发时一样，props传递方式也相同。

当我们希望将组件提供给第三方使用时，需要将组件转换为html标签，以便在任何框架中都可以正常使用。

我们首先需要对组件进行声明，方式如下：
```js
import zoe, { Component, define } from '@zero/zoe'

class A extends Component {
  static elementName = 'component-a'

  render() {
    return 123
  }
}

define(A) // 声明组件A

function B () {
  return 456
}

B.elementName = 'component-b'

define(B) // 声明组件B

class C extends Component {
  static elementName = 'component-c'

  render() {
    return (
      <div>
        // 在任何框架中都可以通过标签名称来使用组件
        <component-a></component-a>
        <component-b></component-b>
      </div>
    )
  }
}

zoe.render(<C />, document.getElementById('app'))
```
