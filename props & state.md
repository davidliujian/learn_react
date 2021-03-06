## props
> 从父级传来的数据在子组件里作为 '属性' 可供使用。 这些 '属性' 可以通过 this.props 访问。   
> 在 JSX 中,通过将 JavaScript 表达式放在大括号中（作为属性或者子节点）,你可以把文本或者 React 组件放置到树中。我们以 this.props 的 keys 访问传递给组件的命名属性，以 this.props.children 访问任何嵌套的元素。

## state
> props 是不可变的：它们从父级传来并被父级“拥有”。为了实现交互，我们给组件引进了可变的 state。this.state 是组件私有的，可以通过调用 this.setState() 改变它。每当state更新，组件就重新渲染自己。

> render() 方法被声明为一个带有 this.props 和 this.state 的函数。框架保证了 UI 总是与输入一致。

> getInitialState() 在生命周期里只执行一次，并设置组件的初始状态。

> componentDidMount 是一个当组件被渲染时被Ｒeact自动调用的方法。动态更新的关键是对 this.setState() 的调用。

> React使用小驼峰命名规范(camelCase)给组件绑定事件处理器。如：handleAuthorChange、handleTextChange

## 组件其实是状态机
> React 把用户界面当作简单状态机。把用户界面想像成拥有不同状态然后渲染这些状态，可以轻松让用户界面和数据保持一致。

> React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。React 来决定如何最高效地更新 DOM。

## State 工作原理 
> 常用的通知 React 数据变化的方法是调用 setState(data, callback)。这个方法会合并（merge） data 到 this.state，并重新渲染组件。重新渲染完成后，调用可选的 callback 回调。大部分情况下不需要提供 callback，因为 React 会负责把界面更新到最新状态。

## 哪些组件应该有 State？
> 尝试把尽可能多的组件无状态化。 这样做能隔离 state，把它放到最合理的地方，也能减少冗余，同时易于解释程序运作过程。

> 常用的模式是创建多个只负责渲染数据的无状态（stateless）组件，在它们的上层创建一个有状态（stateful）组件并把它的状态通过 props 传给子级。这个有状态的组件封装了所有用户的交互逻辑，而这些无状态组件则负责声明式地渲染数据。

## 哪些 应该 作为 State？
> **State 应该包括那些可能被组件的事件处理器改变并触发用户界面更新的数据。** 真实的应用中这种数据一般都很小且能被 JSON 序列化。当创建一个状态化的组件时，思考一下表示它的状态最少需要哪些数据，并只把这些数据存入 this.state。在 render() 里再根据 state 来计算你需要的其它数据。你会发现以这种方式思考和开发程序最终往往是正确的，因为如果在 state 里添加冗余数据或计算所得数据，那么你就需要经常手动保持数据同步，而不能让 React 来帮你处理。

## 哪些不应该作为 State？
> this.state 应该仅包括能表示用户界面状态所需的最少数据。因此，它不应该包括：

>> - 计算所得数据： 不要担心根据 state 来预先计算数据 —— 把所有的计算都放到 render() 里更容易保证用户界面和数据的一致性。例如，在 state 里有一个数组（listItems），我们要把数组长度渲染成字符串， 直接在 render() 里使用 this.state.listItems.length + ' list items' 比把它放到 state 里好的多。
>> - React 组件： 在 render() 里使用当前 props 和 state 来创建它。
>> - 基于 props 的重复数据： 尽可能使用 props 来作为实际状态的源。把 props 保存到 state 的一个有效的场景是需要知道它以前值的时候，因为 props 可能因为父组件的重绘而变化。
