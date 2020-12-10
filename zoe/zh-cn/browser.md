Web Components本身的兼容要求：
- 移动端：ios 10.3、android 5 
- pc端：edge 79、chrome 54、Firefox 63

如果不能满足你的项目要求，可以使用polyfill进行向下兼容：

使用polyfill可以兼容到：
- 移动端：ios 9、android 4.4
- pc端：IE11 以及现代浏览器

#### polyfill使用方式

1、安装webpack插件
```bash
jnpm i @zero/zoe-polyfill-plugin -D
```

2、使用
```js
// webpack.config.js
const ZoePolyfillPlugin = require('@zero/zoe-polyfill-plugin')

// 放入webpack插件中
plugins: [
  new ZoePolyfillPlugin(),
]
```

> [!NOTE]
> polyfill插件会检测当前浏览器是否支持Web Components，如果不支持才会加载polyfill文件

如非必要，不建议使用polyfill，因它会产生几个问题：

**1、不能给组件名称一致的class定义样式**

HelloWorld组件的名称为hello-world，可以使用hello-world作为class名，但是不能定义样式
```js
const style = '.hello-world { color: red; }' // error 不能给.hello-world定义样式
class HelloWorld extends Component {
  static elementName = 'hello-world'
  static style = style

  render() {
    return (
      <div class='hello-world'>123</div> // 可以使用hello-world作为class名，但是不能定义样式
    )
  }
}
```

**2、设置动态class时需要给元素加上组件名称的class**

```js
class HelloWorld extends Component {
  static elementName = 'hello-world'

  state = {
    show: true,
  }

  render() {
    return (
      // div的样式是动态的，需要加上class名hello-world
      <div class={`hello-world ${this.state.show ? 'class-a' : 'class-b'}`}>123</div>
    )
  }
}
```
