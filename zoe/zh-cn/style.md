通过静态属性`style`定义组件样式

方式如下：
```js
import style from 'xxx.css'

// 对于class组件
class HelloWorld extends Component {
  static elementName = 'hello-world'
  static style = style

  render() {
    return 123
  }
}

// 对于函数组件
function HelloWorld () {
  return 123
}

HelloWorld.style = style
HelloWorld.elementName = 'hello-world'
```

也可以通过数组的形式可以传入多个样式文件：

```js
import style1 from 'xxx.css'
import style2 from 'xxx.css'

// 对于class组件
class HelloWorld extends Component {
  static elementName = 'hello-world'
  static style = [style1, style2]

  render() {
    return 123
  }
}

// 对于函数组件
function HelloWorld () {
  return 123
}

HelloWorld.style = [style1, style2]
HelloWorld.elementName = 'hello-world'
```

## 样式共享

Web Components本身的样式是和外部完全隔离的，导致样式无法复用。

为了实现样式共享我们提供了4种方式：

### 1、全局样式

全局样式会作为style标签插入每一个组件中，它会影响每一个组件，设置方式如下：

```js
import zoe from '@zero/zoe'
import style from 'xxx.css'
zoe.options.globalStyle = style
```

### 2、全局link样式

所有以下划线开头的样式文件会合并为一个link标签，并插入每一个组件中。

但是样式生效会有延迟，所以适合体积较大但不会影响布局的样式。

设置方式如下：
```js
import '_xxx.css'
```

### 3、共享当前组件样式
设置静态属性shareStyle为true，可以将当前组件的样式下发，后代组件可以通过声明静态属性applyStyle来使用上层传入的样式。

applyStyle 可以是字符串，或字符串数组，字符串内容为共享样式组件的elementName。

```js

class B extends Component {
  static elementName = 'component-b'
  static applyStyle = ['component-a'] // 或者 'component-a'，声明使用上层传入的共享样式

  render() {
    return 123
  }
}

class A extends Component {
  static elementName = 'component-a'
  static shareStyle = true // 声明共享当前组件的样式

  render() {
    return <B />
  }
}

```

如果有多个组件分享了样式，applyStyle可以设置为数组来使用多个共享样式。
```js
static applyStyle = ['component-a', 'component-xxx' ...]
```

> [!NOTE]
> 共享样式只能向下传递给后代组件。

### 4、共享样式文件
我们可以将公共样式提取为一个文件，分别传入每一个需要用到的组件，更加灵活可控。

```js
import styleA from '组件A的样式文件.css'
import styleB from '组件B的样式文件.css'
import publicStyle from '公共样式文件.css'

class A extends Component {
  static elementName = 'component-a'
  static style = [publicStyle, styleA]
  
  render() {
    return 123
  }
}

class B extends Component {
  static elementName = 'component-b'
  static style = [publicStyle, styleB]

  render() {
    return 456
  }
}
```

## 样式渲染顺序
zoe依次渲染传入的样式，如果有重复的样式，则后传入的会覆盖前面的样式。
