我们来看下 props 和 slot 之间怎么选，才更能提高组件可重用性。

有时候，我们将 props 换成 slot 方式更能提高组件的可重用性，什么意思呢？我们来看下例子。

假设，我们有一个 Buttom 组件，内容如下：

```html
<template>
  <button @click="$emit('click')">{{ text }}</button>
</template>

<script>
  export default {
    name: "Button",
    props: {
      text: {
        type: String,
        required: true,
      },
    },
  };
</script>
```

在 Button 组件中，它接收一个 text 的参数，这里的 text 参数只是单纯为了显示按钮的文本，没有用于其它操作。但有时候我们使用 Buttom 组件时，想 text 外面在加些样式，比如加个 <strong> 标签或者 text 旁边放个图标，显示我们当前的方式满足不了需求。像这种情况，我们用 slot 方式来代替 props 会更合适：

```html
<template>
  <button @click="$emit('click')"><slot /></button>
</template>

<script>
  export default {
    name: "Button",
  };
</script>
```

现在的代码看起来更简洁了，但更重要的是我们能够更灵活地使用 Button 组件的方式了。

比如，使用 props 方式，我们通过 text 参数来传值：

```html
<button>点击我 <strong>领取</strong> 前端资源</button>
```

运行效果如下：

![](./images/11-1.jpg)

但使用 slot 方式，我们能让按钮文本更加的丰富：

运行效果如下：

![](./images/11-2.jpg)

这里，只举例一个很简单的组件事例，大家在封装一些简单或者复杂组件的时候，可以多多思考，到底是 props 更合适，还是 <slot> 更优雅。
