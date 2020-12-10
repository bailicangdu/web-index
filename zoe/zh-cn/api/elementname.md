`elementName`是组件的静态属性，用于定义组件的名称。
```js
import zoe, { Component } from '@zero/zoe'

// class组件
class HelloWorld extends Component {
  static elementName = 'hello-world'

  render() {
    return 123
  }
}

// 函数组件
function HelloWorld2 () {
  return 456
}

HelloWorld2.elementName = 'hello-world2'
```
