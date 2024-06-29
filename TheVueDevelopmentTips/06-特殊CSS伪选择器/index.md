## 插槽选择器

默认情况下，作用域样式不会影响到渲染出来的内容，因为它们被认为是父组件所持有并传递进来的。但使用`:slotted`伪类可以确切地将插槽内容作为选择器的目标。

假设，我们有一个 User 组件，内容如下：

```html
// User.vue
<template>
  <div class="user">
    <slot />
  </div>
</template>

<style scoped>
.user .userInfo{
  color: red;
}
</style>
```

在 User 组件中，我们声明一个默认 插槽`<slot />`。然后我们在父组件中引入：

```html
<template>
  <User>
    <div class="userInfo">小明</div>
  </User>
</template>

<script setup>
import User from './components/User.vue'
</script>
```

运行:

![](./images/6-1.jpg)

发现，我们在 User 组件中样式中，让.userInfo 类的颜色为红色，效果并没有生效，这里因为作用域样式不会影响到 `<slot/>` 渲染出来的内容。

我们要想改变插槽的内容，可以使用 :slotted  伪类：

```css
<style scoped>
:slotted(.userInfo){
  color: red;
}
</style>
```

运行：

![](./images/6-2.jpg)

## 全局选择器

如果想让其中一个样式规则应用到全局，比起另外创建一个 `<style>`，可以使用 :global 伪类来实现 。

我们改下 User 组件中的内容：

```html
<template>
  <div class="user">
    <slot />
  </div>
</template>

<style scoped>
:global(.red) {
  color: red;
}
</style>
```

这里，我们声明了一个全局选择器，将 .red 的样式中应用到全局。这样，在引入 User 组件时，只要有声明 .red 的类，字体都会变成红色。

在父组件中调用：

```html
<template>
  <User />
  <div class="red">小明</div>
</template>

<script setup>
import User from './components/User.vue'
</script>
```

运行：

![](./images/6-3.png)

可以看出，我们不用把 `<div>` 里面放在 User 组件中，也能通过添加一个 .red 类，来改变字体颜色了。