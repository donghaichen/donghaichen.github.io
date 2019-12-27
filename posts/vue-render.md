# ( 转载 ) Vue 中的 render 函数学习

> 简介：对于不了解 slot 的用法（参考：大白话 vue-slot 的用法）又刚接触 render 函数的同学来说，官网的解释无疑一脸懵逼，这里就整理下个人对  render 函数的理解

问题：

　　1. render 函数是什么

　　2. render 函数怎么用

###   render 函数是什么

　　简单的说，在 vue 中我们使用模板 HTML语法组建页面的，
使用  render 函数我们可以用js语言来构建 DOM 

　　因为 vue 是虚拟 DOM ，所以在拿到 template 模板时也要转译成VNode的函数，
而用  render 函数构建 DOM ， vue 就免去了转译的过程。

　　当使用  render 函数描述虚拟 DOM 时， vue 提供一个函数，
这个函数是就构建虚拟 DOM 所需要的工具。官网上给他起了个名字叫 createElement 
还有约定的简写叫 h,

　　vm 中有一个方法 _c ,也是这个函数的别名

　　先看官网对 createElement 的介绍

```javascript
// @returns {VNode}
createElement(
  // {String | Object | Function}
  // 一个  HTML 标签字符串，组件选项对象，或者
  // 解析上述任何一种的一个 async 异步函数，必要参数。
  'div',

  // {Object}
  // 一个包含模板相关属性的数据对象
  // 这样，您可以在  template  中使用这些属性。可选参数。
  {
    // (详情见下一节)
  },

  // {String | Array}
  // 子节点 (VNodes)，由 `createElement()` 构建而成，
  // 或使用字符串来生成“文本节点”。可选参数。
  [
    '先写一些文字',
    createElement('h1', '一则头条'),
    createElement(MyComponent, {
      props: {
        someProp: 'foobar'
      }
    })
  ]
)

```
就是说 createElement（params1，params2，params3） 接受三个参数，
每个参数的类型官方介绍已经说明

###   render 函数怎么用

示例：
```javascript
  render : (h) => {
  return h('div', {
    //给div绑定value属性
    props: {
      value: ''
    },
    //给div绑定样式
    style: {
      width: '30px'
    },
    //给div绑定点击事件　　
    on: {
      click: () => {
        console.log('点击事件')
      }
    },

  })
}
```

### 深入 data 对象

　　有一件事要注意：正如在模板语法中，v-bind:class 和 v-bind:style ，
会被特别对待一样，在 VNode 数据对象中，下列属性名是级别最高的字段
。该对象也允许你绑定普通的  HTML 特性，
就像  DOM  属性一样，比如 inner HTML (这会取代 v- HTML 指令)。
```javascript
{
  // 和`v-bind:class`一样的 API
  'class': {
    foo: true,
    bar: false
  },
  // 和`v-bind:style`一样的 API
  style: {
    color: 'red',
    fontSize: '14px'
  },
  // 正常的  HTML 特性
  attrs: {
    id: 'foo'
  },
  // 组件 props
  props: {
    myProp: 'bar'
  },
  //  DOM  属性
   DOM Props: {
    inner HTML: 'baz'
  },
  // 事件监听器基于 `on`
  // 所以不再支持如 `v-on:keyup.enter` 修饰器
  // 需要手动匹配 keyCode。
  on: {
    click: this.clickHandler
  },
  // 仅对于组件，用于监听原生事件，而不是组件内部使用
  // `vm.$emit` 触发的事件。
  nativeOn: {
    click: this.nativeClickHandler
  },
  // 自定义指令。注意，你无法对 `binding` 中的 `oldValue`
  // 赋值，因为  vue  已经自动为你进行了同步。
  directives: [{
    name: 'my-custom-directive',
    value: '2',
    expression: '1 + 1',
    arg: 'foo',
    modifiers: {
      bar: true
    }
  }],
  // Scoped slots in the form of
  // { name: props => VNode | Array<VNode> }
  scopedSlots: {
    default: props => createElement('span', props.text)
  },
  // 如果组件是其他组件的子组件，需为插槽指定名称
  slot: 'name-of-slot',
  // 其他特殊顶层属性
  key: 'myKey',
  ref: 'myRef'
}
```