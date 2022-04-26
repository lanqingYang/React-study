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

## 组件实例3大属性 props
