# X-Template

另一个定义模板的方式是在一个 <script> 元素中，并为其带上 text/x-template 的类型，然后通过一个 id 将模板引用过去。例如：

```js
<script type="text/x-template" id="hello-world-template">
  <p>Hello hello hello</p>
</script>


Vue.component('hello-world', {
  template: '#hello-world-template'
})
```
###### 这些可以用于模板特别大的 demo 或极小型的应用，但是其它情况下请避免使用，因为这会将模板和该组件的其它定义分离开。


# 内联模板

当 inline-template 这个特殊的 attribute 出现在一个子组件上时，这个组件将会使用其里面的内容作为模板，而不是将其作为被分发的内容。这使得模板的撰写工作更加灵活。

```js
<my-component inline-template>
  <div>
    <p>These are compiled as the component's own template.</p>
    <p>Not parent's transclusion content.</p>
  </div>
</my-component>
```

**内联模板需要定义在 Vue 所属的 DOM 元素内。**

###### 不过，inline-template 会让模板的作用域变得更加难以理解。所以作为最佳实践，请在组件内优先选择 template 选项或 .vue 文件里的一个 <template> 元素来定义模板。