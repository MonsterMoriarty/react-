state是组件内部的状态

## 1、初始化
- 通常在组件类的构造函数结尾处初始化state
```
constructor(props) {
    console.log('enter constructor: ' + props.caption);
    super(props);

    this.onClickIncrementButton = this.onClickIncrementButton.bind(this);
    this.onClickDecrementButton = this.onClickDecrementButton.bind(this);

    this.state = {
      count: props.aaaaaa || 0
    }
```
state的count优先使用prop的coutNum，若无，则使用默认值0。

- defaultProps

也可通过defaultProps将默认值从构造函数中分离出来：
```
constructor(props) {
    console.log('enter constructor: ' + props.caption);
    super(props);

    this.onClickIncrementButton = this.onClickIncrementButton.bind(this);
    this.onClickDecrementButton = this.onClickDecrementButton.bind(this);

    this.state = {
      count: props.aaaaaa
}
Counter.defaultProps = {
  aaaaaa: 0
};

```
这两段代码等效

## 2、读取和更新
- 不能直接修改state，而要通过this.setState()，因为直接修改只会修改状态，却不会驱动组件重新渲染，setState函数修改状态之后会驱动组件进行重新渲染。

读取：
```
 this.state.值
```



















