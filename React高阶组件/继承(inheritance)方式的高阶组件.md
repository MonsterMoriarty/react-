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
function removeUserProp(WrappedComponent) {
  return class NewComponent extends WrappedComponent {
    render() {
      const elements = super.render();
      const {user, ...otherProps} = this.props;
      console.log('##', elements);
      return React.cloneElement(elements, otherProps, elements.props.children);
    }
  };
}
```

- 操纵生命周期函数



## 参考代码















