## 通过代理跨域访问
package.json中添加"proxy": "http://localhost:8080/",

## redux-thunk中间件

- 安装
```
npm install --save redux-thunk
```

- 引入
```
import thunkMiddleware from 'redux-thunk'

const middlewares = [thunkMiddleware];
```

- 异步action对象

不是一个普通的对象，而是一个函数

redux-thunk检查action对象是不是函数，如果不是就放行，如果是，就执行这个函数，并把dispatch和getState函数作为参数传递到函数中去。

在这个函数中可以通过fetch发起一个对服务器的异步请求，得到服务器的结果之后再派发一个action对象到reducer上，最终引起store的改变。

- 异步操作的终止

给一个变量，通过自增的方式记录最新的请求序号，如果不是最新的就丢弃此次请求的结果

## 参考代码

https://github.com/mocheng/react-and-redux/tree/master/chapter-07/weather_redux





