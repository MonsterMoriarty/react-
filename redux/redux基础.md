
## 初始化
1、通过reducer创建store，`store=create(reducer,initValues)`
将store导入view中

2、通过`store.subscribe(listener)`将代表listener注册在store上

3、定义好action以及actionType


## 如何工作
1、在view中，
通过store的`dispatch(action)`方法，
将action传给reducer进行逻辑处理，
并返回一个新的state然后替换掉原store中的state，
（不可直接对原store中的state进行修改——保持状态只读，数据改变只能通过纯函数完成）

2、store中state的改变，会触发开始已经用`subscribe(listener)`注册在store上的listener，
接着在listener中调用`this.setState()`方法对view中的state进行更新。

## 参考代码
https://github.com/mocheng/react-and-redux/tree/master/chapter-03/redux_basic

