# Vue.extend(options)

使用基础Vue构造器，创建一个“子类”。参数是一个包含组件选项的对象。

需要注意，在`Vue.extend()`中`data`选项必须是函数（因为，`Vue.extend()`出来的是组件的一个子类）

```js
<div id="mount-point"></div>
// 创建构造器
var Profile = Vue.extend({
  template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
  data: function () {
    return {
      firstName: 'Walter',
      lastName: 'White',
      alias: 'Heisenberg'
    }
  }
})
// 创建 Profile 实例，并挂载到一个元素上。
new Profile().$mount('#mount-point')
```

结果如下：

```js
<p>Walter White aka Heisenberg</p>
```

可以看到，extend 创建的是 Vue 构造器，而不是我们平时常写的组件实例，所以不可以通过 new Vue({ components: testExtend }) 来直接使用，需要通过 new Profile().$mount('#mount-point') 来挂载到指定的元素上。


# Vue.component(id,[definition])

* 参数：
```js
{string} id
{Function | Object} [definition]
```

* 用法：
注册或获取全局组件。注册还会自动使用给定的 id 设置组件的名称

```js
// 注册组件，传入一个扩展过的构造器
Vue.component('my-component', Vue.extend({ /* ... */ }))

// 注册组件，传入一个选项对象 (自动调用 Vue.extend)
Vue.component('my-component', { /* ... */ })

// 获取注册的组件 (始终返回构造器)
var MyComponent = Vue.component('my-component')
```

# Vue.compile(template)

* 参数：{ string } template

* 用法：将一个模板字符串编译成render函数。**只在完整版时可用**。

```js
var res = Vue.compile('<div><span>{{ msg }}</span></div>')

new Vue({
  data: {
    msg: 'hello'
  },
  render: res.render,
  staticRenderFns: res.staticRenderFns
})
```

# Vue.nextTick( [callback, context] )

* 参数：
  {Function} [callback]
  {Object} [context]

* 用法：

  在下次DOM更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的DOM。

```js
// 修改数据
vm.msg = 'Hello'
// DOM 还没有更新
Vue.nextTick(function () {
  // DOM 更新了
})

// 作为一个 Promise 使用 (2.1.0 起新增，详见接下来的提示)
Vue.nextTick()
  .then(function () {
    // DOM 更新了
  })
```

###### 2.1.0 起新增：如果没有提供回调且在支持 Promise 的环境中，则返回一个 Promise。请注意 Vue 不自带 Promise 的 polyfill，所以如果你的目标浏览器不原生支持 Promise (IE：你们都看我干嘛)，你得自己提供 polyfill。