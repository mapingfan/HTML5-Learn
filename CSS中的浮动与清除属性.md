# CSS中的浮动与清除属性

标签（空格分隔）： css

---

这篇文章用于总结`css`中的浮动和清楚属性。

- 浮动的起源
根据我看的这本书，作者说浮动源于想要实现图文混排的版式。要想实现文字围绕图片的浮动效果，必须先写图片，后写文字。
```
img {
            float: left;
        }
        
<section class="clearfix">
    <img src="images.jpg">
    <p>It's fun to float</p>
</section>
```
对某个元素设置`float`属性时，那就意味着尽量把这个元素往上放（左上或者右上）。对于紧随其后的子元素来说，会选择性失明看不见浮动的元素，所以你会发现`p`元素也尝试着往上靠拢。

- 浮动可以用来干什么
浮动可以用来实现图文混排，分栏效果。所谓的实现分栏，就是对待分栏的元素都使用`float`属性。看个例子
```
<style>
    img,p {float: left}
</style>
<img src="images.jpg">
<p>It's fun to float</p>
```
设置了两个`float`属性，两个元素都拼命往左上角靠拢，直到左上角没有多余的空间可用。

- 弊端
设置浮动属性，会让元素脱离正常的文档流，其父元素看不见浮动的子元素。下面介绍三种方法围住浮动的子元素，不让它们溢出。考虑如下例子：
```
<section>
<img src="images.jpg">
<p>It's fun to float</p>
</section>
<footer>This is footer</footer>
#下面，我们想让p段落同图片并排显示，我们这样应用如下属性：
<style>
    section{
            border: 1px solid blue;
            margin:0 0 10px 0;
        }
        img {
            float: left;
        }
        footer{
            border: 1px solid red;
        }
</style>
# 但是意味发生了，footer元素竟然也浮动上来了，这就显得非常尴尬了。下面的解决办法就是为了解决这个问题。
```
最初我根本没以为`footer`元素会浮动到上面。因为我们只是对`img`元素设置了浮动属性，最多会影响到`p`元素，然而现实并不是如此。它还影响力`section`的兄弟元素`footer`。这就非常尴尬了。既然影响到了`footer`元素，那我们对`footer`元素设置清除属性即可。运行下发现是可行的。但这是我自己的方法，下面介绍下书上给的三种方法。
- 方法一：替父元素添加`overflow:hidden`属性
这个属性的真正用途是防止包含元素被超大内容撑大。应用此属性后，包含元素依旧保持其设定宽度，而超大的子内容则会被其剪切掉。除此之外还有一个作用，即它尽可能迫使父元素包含其浮动的子元素。
上面这段描述看完就知道符合我们的需求。缺点就是并不是一直会有父元素可以设置这个属性。
- 方法二：同时浮动父元素
但是仍要替父元素的兄弟元素设置清除属性。不然你会发现`footer`元素的盒子是包含了`section`元素。
- 方法上：添加非浮动清楚元素：
原理很简单，在我们的`p`元素后面添加一个不可见的元素，然后设置清除属性。当我们在这里设置了清除属性，`footer`元素就不会受到影响。常见有两种方法添加不可见的非浮动子元素：
```
<div class=clear></div> #可以设置可见性为hidden.
其次就是通过css进行设置：
section:after{
    content:".";
    display:block;
    visibility:hidden;
    height:0;
    clear:both;
}
```
我感觉我的第一种方法比较粗暴简单。




