# React 基础入门和组件

## demo01 hellow Word 
    1.html文件引入 react-dom.min.js 和 react.min.js包
        1.1 react.js React核心逻辑，且于具体的渲染引擎无关，从而可以跨平台公用。如果应用要迁移到React Native，这一部分逻辑是不需要改变的。
        1.2 react-dom.js 包含了具体的DOM渲染更新逻辑，以及服务端渲染的逻辑，这部分就是与浏览器相关的部分了。
    用React.creatElement创建元素


    ReactDOM.render(虚拟dom，容器)
## demo2 jsx （javascript XML）
    1.babel 作用 es6=>es5 jsx=>JS
    注意此时<script type='text/babel'>、
    2.jsx语法规则：
        2.1 定义虚拟DOM，不要写引号
        2.2 标签中混入js表达式用P{}
        2.3 样式指定类名 要用calssName
        2.4 内联样式要用style={{key:value}}
        2.5 只有一个根标签
        2.6 标签闭合
        2.7 标签首字母
            （1）小写字母开头，将标签转为html中同名元素，找不到久报错
            （2）大写开头，react渲染对应的组件，组件没定义-报错。

## demo3   jsx数组输出
    1.JSX允许直接在模版插入JavaScript变量。如果这个变量是一个数组，则会展开这个数组的所有成员。

## demo4 函数式组件和类式组件 [简单组件]
    1.函数中this指向undefined，babel生成的代码是严格模式，严格模式下函数的this不执行window，是undefined
    2./* 
    执行了render( <Demo />,。。。之后发生了什么？
        2.1. React找到组件标签，找到Demo组件
        2.2. 发现是函数定义的，调用函数，将返回的虚拟DOM转为真实DOM，呈现再页面中
    */

## demo5 类式组件  [复杂组件]
    类知识点复习
    1. 类中constructor构造中的this 指向实例对象，构造器不是必须的，添加指定属性才写，比如人：年龄、属性
    2. 实例方法在哪里？ 类的原型对象上，供实例使用
    3. 继承且父类写了构造器，那么子类的constructor必须调用super()，并且必须在this操作的最前面。
    4. 类中所定义的方法都放在类的原型对象上，供实例使用

    类式组件
    1. 创建的类中 render放在哪里？ - MyComponent的原型对象上，供实例使用，  实例呢？ render中this是谁？MyComponent类的实例对象- MyComponent类的实例对象 , 或者说MyComponent组件实例对象
    2.执行了render( <MyComponent />,。。。之后发生了什么？
        2.1. React找到组件标签，找到MyComponent组件
        2.2. 发现是类定义的，随后new 类的实例，通过该实例，调用原型上的render方法
        2.3. 将返回的虚拟DOM转为真实DOM，呈现再页面中

## 简单组件和复杂组件
    有state状态，复杂组件

## 组件实例3大属性  state
    !!! 里面的this 值得多看多理解 尚硅谷1516节课程

    1.react 状态state 不可直接更改
    2.类继承了 React.Component， 实例对象的对象原型的对象原型，也就是React.Component的原型对象，上面有setState方法

    为什么要写构造函数？
    1.要去里面初始化状态
    2.解决this指向的问题

    demo7 精简demo6代码,state的简写方式

## react中 构造函数仅两种情况 （state中例子）
    1.通过this.state 复制对象来初始化内部state
    2.为事件处理函数绑定实例

## 组件实例3大属性 props
    1.props限制，PropType， proptype.string.isRequired ,限制必填且未string类型，函数类型 func Person.propTypes={}。默认值：Person.defaultProps={}
    2.props限制简写，放入类中，Person换为  static 就是类本身的属性，不加staic是实例的属性
    3.构造器是否接受props，传不传给super 取决于：是否希望在构造器通过this访问props

## 组件实例3大属性 refs
    1.ref当标识使用 类似于id
    2.字符形式的ref，可能被废弃，不推荐。 效率问题。
    回调函数特点：1.自己定义的 2.自己没调用 3.函数执行了
    3.回调函数中ref：
        3.1 第一次渲染，ref中回调函数执行一次
        3.2 内联的回调函数： 更新时，2次，第一次null，第二次才返回node节点。 （更新，调render，状态改变调用render，1+n次，）
            因为在每次渲染的时候，会创建新的函数实例，所以会清空旧的，设置新的
            解决：替换回调函数为类上的方法。（但是上述也不影响）
    4.React.createRef()使用ref

        calss: myRef= React.createRef()，只能存一个，想要多个就要创建多个 myRef1..
         jsx: <input ref ={this.myRef} type="text" placeholder='点击按钮提示数据'/>

    5.不要过度使用Ref：
        当发生事件的元素刚好是要操作的元素，就可以用event事件直接实现操作dom不需要用ref
## 事件处理

    1.通过onXxx属性指定事件处理函数(大小写注意)
        1.1 React使用自定义(合成)事件，而不是使用原生DOM事件
        1.2 React中事件是通过事件委托方式处理的(委托给最外层元素)
    2.通过event.target得到发生事件的DOM元素对象  ----不要过度使用ref，当发生事件的元素刚好是要操作的元素，就可以用event事件
    3.!!必须把一个函数作为事件的回调！！！ （函数柯里化例子）

## react中收集表单数据 
##### **官网：请勿过度使用ref**
    表单提交，默认引发页面跳转、刷新
    非受控：要写ref.  
    受控  优势 省略掉ref：类似于vue双向绑定(v-model=v-bind+@change语法糖)。

## 高阶函数、函数柯里化
    1.高阶函数： 如果函数符合下面2个规范中任何一个，就是高阶函数：
        1.1 若A函数，接受的参数是一个函数
        1.2 若A函数，调用的返回值依然是一个函数
        常见高阶函数： Promise，、setTimeout、Array常见方法（arr.map()）

    2.函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式

## 组件生命周期
    挂载 Mount： 把组件挂载到页面上
    卸载 UnMount： 卸载组件