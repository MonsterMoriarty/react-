## 原理
采用组件继承的方式实现高阶组件



## 应用场景

- 操纵props

不安全的方式：
```
function removeUserProp(WrappedComponent) {
  return class NewComponent extends WrappedComponent {
    render() {
      const {user, ...otherProps} = this.props;
      this.props = otherProps;
      return super.render();
    }
  };
}
```
安全的方式：
```
const modifyPropsHOC = (WrappedComponent) => {
  return class NewComponent extends WrappedComponent {
    render() {
      const elements = super.render();

      const newStyle = {
        color: (elements && elements.type === 'div') ? 'red' : 'green'
      }
      const newProps = {...this.props, style: newStyle};

      return React.cloneElement(elements, newProps, elements.props.children);
    }
  };
};
```
除非高阶组件需要根据参数组件渲染结果来决定如何修改props。

否则使用代理方式实现操纵prop的功能更加清晰。

- 操纵生命周期函数

如：控制render
```
const onlyForLoggedinHOC = (WrappedComponent) => {
  return class NewComponent extends WrappedComponent {
    render() {
      if (this.props.loggedIn) {
        return super.render();
      } else {
        return null;
      }
    }
  }
}

```
或者控制shouldComponentUpdate：
```
const cacheHOC = (WrappedComponent) => {
  return class NewComponent extends WrappedComponent {
    shouldComponentUpdate(nextProps, nextState) {
      return nextProps.useCache;
    }
  }
}
```

## 参考代码

https://github.com/mocheng/react-and-redux/blob/master/chapter-06/hoc/src/inheritance
