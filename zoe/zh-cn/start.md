
#### 1、安装依赖

```shell
jnpm i @zero/zoe -S
```

#### 2、开始使用
zoe组件和React组件写法几乎一致，但也有不同点：

1、通过静态属性 `elementName` 声明组件名称

2、通过静态属性 `style` 设置组件样式

```js
import zoe, { Component } from '@zero/zoe'
import style from 'xxx.css'

class HelloWorld extends Component {
  static elementName = 'hello-world'
  static style = style

  state = {
    count: 1,
  }

  handleClick = () => {
    this.setState({
      count: this.state.count + 1
    })
  }

  render() {
    return (
      <div class='my-btn' onClick={this.handleClick}>{this.state.count}</div>
    )
  }
}

zoe.render(<HelloWorld />, document.getElementById('app'))
```

渲染结果如下：

![result](https://img12.360buyimg.com/imagetools/jfs/t1/148403/7/9500/42291/5f718b26E649b3042/78445d86e19ff565.png ':size=60%')
