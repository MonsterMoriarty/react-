## 1、意义

虽然Redux全局只有一个store，但是每个组件都需要导入store，
而大项目中是不知道store的位置的，直接导入不利于复用。

最好只有一个地方需要导入store，这个位置在调用最顶层React组件的位置。

## 2、创建一个特殊的组件Provider

作为通用的context提供者

```
import {PropTypes, Component} from 'react';
class Provider extends Component {
  render() {
    return this.props.children;
  }
}
export default Provider;
```


## 3、Provider组件宣称自己支持context

```
Provider.childContextTypes = {
  store: PropTypes.object
};
```

## 4、提供函数返回context的对象

```
  getChildContext() {
    return {
      store: this.props.store
    };
  }

```


## 5、Provider组件的所有子孙组件宣称自己需要context

```
CounterContainer.contextTypes = {
  store: PropTypes.object
}
```


## 6、通过this.context.store访问store

```
getOwnState() {
    return {
      value: this.context.store.getState()[this.props.caption]
    };
  }
```

且在构造函数中需要带上context

```
constructor(props, context) {
    super(props, context);
  }
```

















