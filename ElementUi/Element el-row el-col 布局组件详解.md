**本文目录**

[1、背景](##背景)

[2、分栏布局](##分栏布局)

[3、分栏间隔](##分栏间隔)

[4、分栏偏移](##对其方式)

[5、对齐方式](##对其方式)

[6、响应式布局](##响应式布局)

[7、小结](##小结)

## 1、背景

element的布局方式与bootstrap原理是一样的，将网页划分成若干行，然后每行等分为若干列，基于这样的方式进行布局，形象的成为栅栏布局。

区别是element可将每行划分为24个分栏，而bootstrap是划分为12个分栏，从使用角度，还是24个分栏更加精细。

## 2、分栏布局

首先每行使用`<el-row>`标签标识，然后每行内的列使用`<el-col>`标识，至于每列整行的宽度比例，则使用`:span`属性进行设置。

如下代码，即为将1行等分为2列，为了便于区分列，我们为列添加了不同的样式，另外注意`<el-divider></el-divider>`是分割线，此处用于区分不同的示例。

```html
<template>
  <div>
  	<span>每行24分栏布局</span>
    <el-row>
      <el-col :span="12" class="lightgreen-box">示例1</el-col>
      <el-col :span="12" class="orange-box">示例1</el-col>
    </el-row>
    <el-divider></el-divider>
  </div>
</template>
<style scoped>
	.lightgreen-box {
	  background-color: lightgreen;
	  height: 24px;
	}
	.orange-box {
	  background-color: orange;
	  height: 24px;
	}
</style>
```

## 3、分栏间隔

有时候想为不同分栏之间设定一定的间隔，可以使用<el-row>标签的:gutter属性，注意默认间隔为0。

此时需要注意的是，下面的写法，间隔是不生效的。

```html
<span>分栏间隔 无效</span>
<el-row :gutter="50">
  <el-col :span="8" class="lightgreen-box">示例2</el-col>
  <el-col :span="8" class="orange-box">示例2</el-col>
  <el-col :span="8" class="lightgreen-box">示例2</el-col>
</el-row>
<el-divider></el-divider>
```

需要在分栏里面新增元素，才能实现分栏间隔，代码修改如下则间隔生效。

```html
<span>分栏间隔 有效</span>
<el-row :gutter="24">
  <el-col :span="8">
    <div class="lightgreen-box">示例3</div>
  </el-col>
  <el-col :span="8">
    <div class="orange-box">示例3</div>
  </el-col>
  <el-col :span="8">
    <div class="lightgreen-box">示例3</div>
  </el-col>
</el-row>
<el-divider></el-divider>
```

上面两个示例效果如下：

![image](https://github.com/user-attachments/assets/79bf28f5-4977-420a-aed6-8341a1de9dfe)

## 4、分栏偏移

有时候想让某个分栏不从左边显示，而是直接显示到中间或者右侧，例如右侧导航栏，我们希望它处于右侧且占据页面1/3的宽度。此时可以借助offset属性来实现，表示偏移量。

此时，想占据1/3宽度，则:span应为8，偏移量应为24-8=16，所以代码如下：

```html
<span>分栏偏移</span>
<el-row>
  <el-col :span="8" :offset="16">
    <div class="lightgreen-box">示例4</div>
  </el-col>
</el-row>
<el-divider></el-divider>
```

效果如下：

![image](https://github.com/user-attachments/assets/5b56af38-c874-48dd-ac21-94750d5b720e)

## 5、对齐方式

如果想让整个行居左、居中、居右对齐，则可以直接设置<el-row>的对齐方式。

此时需要先设置type="flex"来启用对齐方式，然后通过justify属性来设置具体的对齐方式，例如下面的例子实现了居中对齐。

```html
<span>对齐方式</span>
<el-row type="flex" justify="center">
  <el-col :span="12">
    <div class="lightgreen-box">示例5</div>
  </el-col>
</el-row>
<el-divider></el-divider>
```

![image](https://github.com/user-attachments/assets/ad91213a-e51e-43d5-8f54-70925520c768)

## 6、响应式布局

element和bootstrap的响应式布局原理相同，都是通过为列设置不同分辨率下的占用宽度比例来实现的。

例如我们想实现在比较大的分辨率（电脑），每分栏占据屏幕宽度的1/4，而在比较小宽度（手机），每分栏占据屏幕全部宽度。这样就能保证在手机上也能完整显示内容，则可以使用如下代码：

```html
<span>响应式布局</span>
<el-row>
  <el-col :lg="6" :xs="24" class="lightgreen-box">示例6</el-col>
  <el-col :lg="6" :xs="24" class="orange-box">示例6</el-col>
  <el-col :lg="6" :xs="24" class="lightgreen-box">示例6</el-col>
  <el-col :lg="6" :xs="24" class="orange-box">示例6</el-col>
</el-row>
```

在电脑上效果如下：

![image](https://github.com/user-attachments/assets/51a6e7d6-8242-4038-a0b9-e9ea313c54cd)

在手机上效果如下：

![image](https://github.com/user-attachments/assets/e4fe42f8-7af7-4228-b5a3-ffb50963d9a2)

注意具体的尺寸属性为：


属性	使用说明

xs	宽度<768px

sm	>=768px

md	>=992px

lg	>=1200px

xl	>=1920px


## 7、小结

element的布局跟bootstrap原理是一样的，使用起来也比较方便，具体的参数其实不需要都记住，只要知道用法，使用时去官网查询即可。
