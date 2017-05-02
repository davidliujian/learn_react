### React 的 JSX 使用大、小写的约定来区分本地组件的类和 HTML 标签。 
> React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)  
> 要渲染 HTML 标签，只需在 JSX 里使用小写字母的标签名。
```jsx
var myDivElement = <div className="foo" />;
ReactDOM.render(myDivElement, document.getElementById('example'));
```
> 要渲染 React 组件，只需创建一个大写字母开头的本地变量。

```jsx
var MyComponent = React.createClass({/*...*/});
var myElement = <MyComponent someProperty={true} />;
ReactDOM.render(myElement, document.getElementById('example'));
```

> 由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。

### 转换
> JSX 把类 XML 的语法转成原生 JavaScript，XML 元素、属性和子节点被转换成 React.createElement 的参数。

```jsx
var Nav, Profile;
// 输入 (JSX):
var app = <Nav color="blue"><Profile>click</Profile></Nav>;
// 输出 (JS):
var app = React.createElement(
  Nav,
  {color:"blue"},
  React.createElement(Profile, null, "click")
);
```

### 命名组件
> 令你使用包含其他组件作为属性的单一的组件,**只需要把你的"子组件"创建为主组件的属性。**

```jsx
var MyFormComponent = React.createClass({ ... });
MyFormComponent.Row = React.createClass({ ... });
MyFormComponent.Label = React.createClass({ ... });
MyFormComponent.Input = React.createClass({ ... });
```

### 属性表达式 
> 要使用 JavaScript 表达式作为属性值，只需把这个表达式用一对大括号 ({}) 包起来，不要用引号 ("")。

### Boolean 属性
> 省略一个属性的值会导致JSX把它当做 true。要传值 false必须使用属性表达式。这常出现于使用HTML表单元素，含有属性如disabled, required, checked 和 readOnly。

### 子节点表达式
```jsx
// 输入 (JSX):
var content = <Container>{window.isLoggedIn ? <Nav /> : <Login />}</Container>;
// 输出 (JS):
var content = React.createElement(
  Container,
  null,
  window.isLoggedIn ? React.createElement(Nav) : React.createElement(Login)
);
```
### 注释
> JSX 里添加注释很容易；它们只是 JS 表达式而已。你仅仅需要小心的是当你在一个标签的子节点块时，要用 {} 包围要注释的部分。

```jsx
var content = (
  <Nav>
    {/* child comment, 用 {} 包围 */}
    <Person
      /* 多
         行
         注释 */
      name={window.isLoggedIn ? window.name : ''} // 行尾注释
    />
  </Nav>
);
```
### 展开属性(...操作符)
```jsx
  var props = {};
  props.foo = x;
  props.bar = y;
  var component = <Component {...props} />;
  
// 它能被多次使用，也可以和其它属性一起用。注意顺序很重要，后面的会覆盖掉前面的。
  var props = { foo: 'default' };
  var component = <Component {...props} foo={'override'} />;
  console.log(component.props.foo); // 'override'
  ```
  
### HTML 实体
> html实体可以插入到jsx的文本中，如果想在 JSX 表达式中显示 HTML 实体，可以会遇到二次转义的问题，因为 React 默认会转义所有字符串，为了防止各种 XSS 攻击。
```jsx
// 错误: 会显示 “First &middot; Second”
<div>{'First &middot; Second'}</div>
```
1.直接用Unicode字符，这时要确保文件是 UTF-8 编码且网页也指定为 UTF-8 编码。         
```jsx
<div>{'First · Second'}</div>   
```    
2.安全的做法是先找到 实体的 Unicode 编号 ，然后在 JavaScript 字符串里使用。
```jsx
<div>{'First \u00b7 Second'}</div>
<div>{'First ' + String.fromCharCode(183) + ' Second'}</div>
```
3.可以在数组里混合使用字符串和 JSX 元素。
 ```jsx
 <div>{['First ', <span>&middot;</span>, ' Second']}</div>
 ```
4.万不得已，可以直接插入原始HTML。
```jsx
<div dangerouslySetInnerHTML={{__html: 'First &middot; Second'}} />
```

### 自定义 HTML 属性
> 如果往原生 HTML 元素里传入 HTML 规范里不存在的属性，React 不会显示它们。如果需要使用自定义属性，要加 data- 前缀。
```jsx
<div data-custom-attribute="foo" />
```
> 然而，在自定义元素中任意的属性都是被支持的 
```jsx
<x-my-component custom-attribute="foo" />
```