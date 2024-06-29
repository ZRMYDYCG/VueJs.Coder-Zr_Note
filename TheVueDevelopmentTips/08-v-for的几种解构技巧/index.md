我们来看下在 v-for 中的几种解构方式。之所以可以使用 v-for 进行解构，是因为 Vue 将v-for的整个第一部分直接提升到函数的参数部分：

```html
<li v-for="____ in array"> 
</li> 
function (____) { 
  //... 
}
```

## 方式一：对数组进行解构

代码如下：

```html
<template>
  <div>
    <ul>
      <li v-for="(lang, index) in ['vue2', 'vue3', 'JavaScript', 'TypeScript']">
        {{ index }}: {{ lang }}
      </li>
    </ul>
  </div>
</template>
```

运行结果：

```bash
0: vue2

1: vue3

2: JavaScript

3: TypeScript
```


## 方式二：对对象进行解构

对对象进行解构时，我们可以获取对象的键值对。

```html
<template>
  <div>
    <ul>
      <li v-for="(value, key) in {
        name: '王大冶',
        age: 26,
        job: '前端开发'
      }">
        {{ key }}: {{ value }}
      </li>
    </ul>
  </div>
</template>
```

运行结果：

```bash
name: 王大冶

age: 26

job: 前端开发
```

## 方式三：对对象进行解构 + 索引

除了获取对象的键值对外，还可以通过第三个参数，获取当前迭代的索引。

```html
<template>
  <div>
    <ul>
      <li v-for="(value, key, index) in {
        name: '王大冶',
        age: 26,
        job: '前端开发'
      }">
       #{{ index + 1 }} {{ key }}: {{ value }}
      </li>
    </ul>
  </div>
</template>
```

运行结果：

```bash
#1 name: 王大冶

#2 age: 26

#3 job: 前端开发
```

## 方式四：对字符串进行解构

你知道吗，还可以使用v-for遍历字符串?

```html
<template>
  <div>
    <ul>
      <li v-for="character in 'Hello, World'">
        {{ character }}
      </li>
    </ul>
  </div>
</template>
```

运行结果会打印每个字符：

```bash
H

e

l

l

o

,



W

o

r

l

d

```
