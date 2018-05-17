## 1、赋值
prop是组件对外的接口，很像HTML元素的属性，支持所有数据类型。

当prop的类型不是字符串类型时，必须用{}把值包住，两层{}则表示——外层是JSX语法，内层代表是一个对象
```
<组件 
id="id" 
bw={2} 
onClick={onButtonClick} 
style={{color:"red",height:"100px"}} 
/>
```


## 2、取值
- 如果一个组件，定义了构造函数，必须在构造函数的第一行通过super(prop)调用父类React.Component的构造函数。否则，无法在成员函数中通过this.props访问到父组件传递过来的props。所以，给this.props赋值是React.Component构造函数的工作之一。
- 在构造函数中通过props获得传入的prop，在其他的成员函数中则通过this.props访问传入的prop。
```
//构造函数
 constructor(props) {
    console.log('enter constructor: ' + props.caption);
    super(props);
    }
    
 //成员函数   
 componentWillMount() {
    console.log('enter componentWillMount ' + this.props.caption);
    }
```


## 3、propType检查
```
Counter.propTypes = {
  caption: PropTypes.string.isRequired,
  initValue: PropTypes.number
};
```
