## connect：连接容器组件和展示组件

React-Redux中没有定义CounterContainer这样的容器组件，而是直接导出了一个语句
```
export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```
connect(mapStateToProps,mapDispatchToProps)的返回值是一个函数，将这个返回的函数立即执行。
其中：

- mapStateToProps方法store上的state传递给内层展示组件的prop
```
function mapStateToProps(state, ownProps) {
  return {
    value: state[ownProps.caption]
  }
}
```

- mapDispatchToProps方法将展示组件中的用户动作变为action传给reducer进行逻辑处理
```
function mapDispatchToProps(dispatch, ownProps) {
  return {
    onIncrement: () => {
      dispatch(Actions.increment(ownProps.caption));
    },
    onDecrement: () => {
      dispatch(Actions.decrement(ownProps.caption));
    }
  }
}
```

- Counter是展示组件
```
class Counter extends Component {
  render() {
    const {caption, onIncrement, onDecrement, value} = this.props;
    return (
      <div>
        <button style={buttonStyle} onClick={onIncrement}>+</button>
        <button style={buttonStyle} onClick={onDecrement}>-</button>
        <span>{caption} count: {value}</span>
      </div>
    );
  }
} 
```





## Provider：提供包含store的context
直接在顶层导入react-redux的Provider即可，
```
import React from 'react';
import ReactDOM from 'react-dom';
import {Provider} from 'react-redux';

import ControlPanel from './views/ControlPanel';
import store from './Store.js';

import './index.css';

ReactDOM.render(
  <Provider store={store}>
    <ControlPanel/>
  </Provider>,
  document.getElementById('root')
);
```








## 参考代码

https://github.com/mocheng/react-and-redux/blob/master/chapter-03/react-redux


