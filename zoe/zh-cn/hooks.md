zoe实现了React的Hooks语法，写法一致，但也有不同点：

1、通过函数静态属性 `elementName` 声明组件名称

2、通过函数静态属性 `style` 设置组件样式

例子：
```js
import zoe, { useState } from '@zero/zoe'
import style from 'xxx.css'

function HelloWorld () {
  const [count, setCount] = useState(1)

  return (
    <div class='my-btn' onClick={() => setCount(count + 1)}>{count}</div>
  )
}

HelloWorld.elementName = 'hello-world'
HelloWorld.style = style

zoe.render(<HelloWorld />, document.getElementById('app'))

```

渲染结果如下：

![result](https://img12.360buyimg.com/imagetools/jfs/t1/148403/7/9500/42291/5f718b26E649b3042/78445d86e19ff565.png ':size=60%')
