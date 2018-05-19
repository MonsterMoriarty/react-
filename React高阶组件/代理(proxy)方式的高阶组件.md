## 原理：
接收被代理的组件作为参数，处理之后，渲染出新的组件

## 应用场景

- 操纵prop
```
function removeUserProp(WrappedComponent) {
  return function newRender(props) {
    const {user, ...otherProps} = props;
    return <WrappedComponent {...otherProps} />
  }
}
```

- 访问ref
```
不推荐使用ref直接操纵DOM元素
```

- 抽取状态
```

```

- 包装组件
```

```

## 参考代码

https://github.com/mocheng/react-and-redux/tree/master/chapter-06/hoc



















