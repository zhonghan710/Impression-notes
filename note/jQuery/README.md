# jQuery

JavaScript技术核心：获取标签， 绑定事件，标签的变化

jQ的获取标签$(".wrap p")，括号内书写类名.wrap，#wrap，

```js
  window.onload = function(){}
```

onload事件：网站资源全部加载完成才执行；执行一次

ready方法：DOM结构加载完毕之后执行；执行多次，不会覆盖。

```js
$(document).ready(function(){
  alert("ready1")
});
// ready简写
$(function(){
  alert("ready2")
})
```

## 绑定事件两种方法

```js
$('.btn').click(function (e) {
  ...
});
$('.btn').on('click', target, function (e){
  ...
})
// target为事件委托的对象，没有实质的变化
```

## 事件移除

```js
$(".btn").off("click");
// 如果不在括号里，则移除所有事件
```

## on、bind、live区别

使用bind()方法是浪费资源的，因为他要匹配选择器中的每一项并且挨个设置相同的时间处理程序。

建议停止使用.live()方法，因为他已经弃用了。

1.在调用live()方法之前，jquery会先获取与指定的选择器匹配的元素，这一点对于大型文档来说很花费时间。
2.不支持链式写法，例如$('a').find('.classA, .classB').live()，不合法的写法。
3.由于所有的live()时间被添加到document元素上，所以在时间被处理之前，可能会通过最长最慢的那条路去触发。
4.在移动端ios(iphone,ipad,ipod)上，对于大多数元素而言，click()事件不会冒泡到文档body上，并且如果不满足如下情况之一，就不能和live()方法使用：使用原生的可被点击的元素，例如a或者Button，因为这两个元素可以冒泡到document。
5.在doucment.body内的元素使用on()或者delegate()进行绑定，因为移动端ios只有在Body内才进行冒泡。
6.需要click冒泡到元素上才能应用的css样式例如cursor。但是依然需要注意，这样会禁止元素上的复制、粘贴功能，当点击元素时，会导致该元素高亮。
7.在事件处理中调用event.stopPropagation()来阻止事件处理被添加到document之后的结点中，是效率最低的。因为事件已经被传播到document上。
8.live()方法与其它事件方法的相互影响是会令人感到惊讶的。例如，$(document).unbind('click')会移除所有通过live()绑定的click事件。

delegate()方法'很划算'用来处理性能和响应动态添加元素。

新的on()方法主要是实现bind()、live()甚至delegate()的功能。