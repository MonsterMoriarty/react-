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

在容器组件和展示组件的关系中，通常展示组件为无状态组件，所有的状态管理都交给外部的容器组件，这个模式就叫做“抽取状态”。
```
import React from 'react';

const doNothing = () => ({});

function connect(mapStateToProps=doNothing, mapDispatchToProps=doNothing) {

  function getDisplayName(WrappedComponent) {
    return WrappedComponent.displayName ||
      WrappedComponent.name ||
      'Component';
  }

  return function(WrappedComponent) {
    class HOCComponent extends React.Component {
      constructor() {
        super(...arguments);

        this.onChange = this.onChange.bind(this);

        this.store = {};
      }

      /*
      //TODO: make a workable shouldComponentUpdate
      shouldComponentUpdate(nextProps, nextState) {
        for (const propType in nextProps) {
          if (nextProps.hasOwnProperty(propType)) {
            if (nextProps[propType] === this.props[propType]) {
              return true;
            }
          }
        }
        for (const propType in this.props) {
          if (this.props.hasOwnProperty(propType)) {
            if (nextProps[propType] === this.props[propType]) {
              return true;
            }
          }
        }
        return false;
      }
      */

      componentDidMount() {
        this.context.store.subscribe(this.onChange);
      }

      componentWillUnmount() {
        this.context.store.unsubscribe(this.onChange);
      }

      onChange() {
        this.setState({});
      }

      render() {
        const store = this.context.store;
        const newProps = {
          ...this.props,
          ...mapStateToProps(store.getState(), this.props),
          ...mapDispatchToProps(store.dispatch, this.props)
        }

        return <WrappedComponent {...newProps} />;
      }
    };

    HOCComponent.contextTypes = {
      store: React.PropTypes.object
    }

    HOCComponent.displayName = `Connect(${getDisplayName(WrappedComponent)})`;

    return HOCComponent;
  };
}

export default connect;

```

- 包装组件

render的JSX中完全可以引入其他元素或者组合多个React组件。
```

import React from 'react';

const styleHOC = (WrappedComponent, style) => {
  return class HOCComponent extends React.Component {
    render() {
      return (
        <div style={style}>
          <WrappedComponent {...this.props}/>
        </div>
      );
    }
  };
};

export default styleHOC;

```

## 参考代码

https://github.com/mocheng/react-and-redux/tree/master/chapter-06/hoc



















