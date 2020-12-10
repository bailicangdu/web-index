
### 测试页面

```jsx
/*react*/
<desc>
Hello `world`
* a
* b
</desc>
<style>
  .author {
    color: #ff0000cc;
  }
</style>
<script>
  export default class Application extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        color: 'blue'
      }
      this.globalVariable = globalVariable
    }
    render() {
      return (
        <div>
          <div className='wrapper' ref={el => this.el = el}>
            <div>
            <p className='author'>author: {this.globalVariable}</p>
            <button style={{color: this.state.color}} className='test' onClick={e => {alert('author: ' + this.globalVariable); this.setState({color: 'red'})}}>test</button>
            </div>
          </div>
        </div>
      )
    }
  }
</script>
```

> [!NOTE]
> An alert of type 'note' using global style 'callout'.

> [!NOTE|style:flat]
> An alert of type 'note' using alert specific style 'flat' which overrides global style 'callout'.

> [!TIP]
> An alert of type 'note' using global style 'callout'.

> [!TIP|style:flat]
> An alert of type 'note' using alert specific style 'flat' which overrides global style 'callout'.


> [!WARNING]
> An alert of type 'note' using global style 'callout'.

> [!WARNING|style:flat]
> An alert of type 'note' using alert specific style 'flat' which overrides global style 'callout'.


> [!DANGER]
> An alert of type 'note' using global style 'callout'.

> [!DANGER|style:flat]
> An alert of type 'note' using alert specific style 'flat' which overrides global style 'callout'.

<!-- [filename](http://cangdu.org/index.html ':include') -->

<div class='iframe-container'>
  <iframe src="https://cangdu.org/elm" width="100%" height="100%"></iframe>
</div>