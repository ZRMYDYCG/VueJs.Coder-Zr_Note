## 前言

> 在 Vue3 中封装一些组合方法时，有时候想用 ref，有时候又不想使用。这节课，我们来介绍一种模式，可以让我们即可以使用 ref，又可以不使用，从而让组合函数更具有灵活性。

## 使用 ref 和 unref 获得更灵活的参数

通常，封装一些公共方法时，需要接收参数，参数一般是非响应式的，即非 reactive 或 ref 类型的数据，但是呢，有时候参数如果具有响应式的时候，该方法会更加的有用且灵性。

所以编写更加灵活的组合方法时，不仅要接收 ref 类型的参数也可以接收原始类型参数，然后我们将参数转换为我们需要参数。如下所示：

```js
// 传递一个 ref
const countRef = ref(2);
useCount(countRef);

// 或者直接一个数字
const countRef = useCount(2);
```

VueUse 中的 useTitle 也是采用这种模式，当我们传入一个 ref 时，网页标题就可以通过 .value 的方式来动态更改:

```js
const title = ref("Vue2 小技巧");
useTitle(title);
title.value = "Vue3 小技巧";
```

如果传入的是一个字符串，useTitle 内部会创建一个 ref，值为我们所传入的字符，最后返回一个 ref 变量，然后 .value 的方式来动态更改。

```js
const title = useTitle("Vue2 小技巧");
title.value = "Vue3 小技巧";
```

## 在组合函数中实现灵活的参数

为了让灵活的参数模式能工作，我们需要对得到的参数使用 ref 或 unref 进行包装：

```js
export default useMyComposable(input) {
  const ref = ref(input);
}

export default useMyComposable(input) {
  const rawValue = unref(input);
}
```

ref 函数将为我们创建一个新的 ref。但如果我们传给它一个 ref，它只是把这个 ref 返回给我们:

```js
// 创建一个 ref
const myRef = ref(0);
// 结果是相等的
allert(myRef === ref(myRef));
```

unref 函数的工作原理是一样的，但是它要么解开一个 ref，要么把我们的原始值返回给我们：

```js
const value = unref(myRef);
// 结果是相等的
assert(value === unref(value));
```

我们来 看看 VueUse 中的 useTitle 是如何实现这个模式的.

在 useTitle 中,我们即可以传入一个字符串还可以传入 ref，它并不关心我们提供的是哪一个：

```js
// 传入一个字符串
const titleRef = useTitle("Vue2 小技巧");

// 传入 `ref`
const titleRef = ref("Vue3 小技巧");
useTitle(titleRef);
```

在源代码中，可以看到，这里使用了 ref 函数，它允许我们使用一个 ref 或一个字符串来创建 title 的 ref:

```js
// ...
const title = ref(newTitle ?? document?.title ?? null);
// ...
```

这里的意思是先取 newTitle 作为初始化值，如果没有在取 document?.title，还是没有就取 null。

最后

我们可以通过在组合函数中巧妙地使用 ref 和 unref 来搭配地使用参数，让我们的方法更加具有灵活性。
