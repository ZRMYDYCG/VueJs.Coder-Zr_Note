我们知道在 Vue2 中可以通过 Vue.prototype 来扩展全局属性，如下所示 ：

```js
import Vue from "vue";
Vue.prototype.$myGlobal = "全局属性";
```

在 Vue3 中跟 Vue2 不太一样， Vue3 中每个 Vue 应用都会暴露一个包含其配置项的 config 对象，在 config 对象中有一个 globalProperties 属性，该属性就是用来添加一个可以在应用的任何组件实例中访问的全局 property，如下所示：

```js
import { createApp } from "vue";
const app = createApp({});

app.config.globalProperties.$myGlobal = "全局属性";
```

> 建议在任何全局属性前加一个 `$` ，防止与其他变量的命名冲突，而且这也是一个标准的惯例，开发者看到 值 `$`，基本不知道了该变量是全局变量了。

声明了全局属性后，我们在任何组件中都可以访问该属性了，在选项 API 中可以通过 this 来获取，如下所示：

```html
<template>
  <div>获取到全局属性，值为：{{ getGlobalProperty }}</div>
</template>

<script>
  export default {
    name: "Button",
    computed: {
      getGlobalProperty() {
        return this.$myGlobal;
      },
    },
  };
</script>
```

运行，效果如下：

![](./images/12-1.jpg)

但在组合 API 中，我们不能用这种方式获取全局属性，因为访问不到 this 的值。那怎么做了，常见的做法是创建一个简单的可组合函数来获取全局的属性，如下所示：

```js
// useGlobals.js
export default () => ({
  $myGlobal: "全局属性",
});
```

然后通过函数的方式来获取到改全局属性，如下所示：

```html
<template>
  <div>获取到全局属性，值为：{{ $myGlobal }}</div>
</template>

<script setup>
  import useGlobals from "../useGlobals";

  const { $myGlobal } = useGlobals();
</script>
```

我们引入 useGlobals 方法并执行，我们知道执行``useGlobals() 并返回一个对象，接着我们通过对象解构的方式就能拿到我们声明的全局属性了。

运行，效果如下：

![](./images/12-2.jpg)
