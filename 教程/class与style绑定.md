# 绑定HTML Class

#### 对象语法

我们可以传给 v-bind:class 一个对象，以动态地切换 class。

动态的v-bind：class对象还能接受一个计算属性。例如：
```js
<div v-bind:class="classObject"></div>
```


# 绑定内联样式

#### 对象语法

v-bind:style的对象语法十分直观--看着非常像CSS，但其实是一个JavaScript对象。CSS property名可以用驼峰式或短横线分隔来命名。

