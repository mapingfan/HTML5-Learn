# CSS

标签（空格分隔）： css

---

1.块级元素盒子会默认拓展到与父元素同宽。
2.结构化伪类：`:first-child，nth-child(n)`的含义：
当我们写下如下`css`时，意味着什么？
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        ol:first-child{
            border:thin solid red;
        }
    </style>
</head>
<body>
    
    <ol>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ol>
</body>
</html>
```
上面的例子中我们可以看到，我们写下了`ol:first-child`样式，但是具体应用到哪里？是应用到`ol`
元素的的第一个儿子节点吗？实际操作并不是，而是应用到了整个`ol`元素上。那就说明我们先前的理解是有偏差的，`:first-child`并不是意味着元素的第一个孩子会被施加样式表。
下面在看一个例子：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        ol:first-child{
            border:thin solid red;
        }


    </style>
</head>
<body>
    <h1>This is a header .</h1> #此处我们添加了一个标题。
    <ol>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ol>
</body>
</html>
```
此时打开页面，你会发现我们写下的`css`特效没有被运用。这个就有点意思了，值得深究。
结论：
当我们写下`ol:first-child`之类的伪类样式规则时，并不是意味着会对`ol`的第一个孩子施加样式，而是意味着只有当`ol`元素是整个页面的`第一个儿子元素`时才会被施加特性。要注意，特性是施加在`ol`上。

最后来个例子验证下:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        :first-child{
            border:thin solid red;
        }


    </style>
</head>
<body>
    <h1>This is a header .</h1>
    <ol>
        <li id="first">1</li>
        <li>2</li>
        <li>3</li>
    </ol>
</body>
</html>
```
如果你能提前预测出样式表会施加在哪些元素上，那么你已经明白这个点。答案是对页面中所有元素的第一个儿子元素施加。具体到这个例子就是`h1,li`元素。

3.伪类选择器：
分为两类：1.UI伪类选择器 2.结构化伪类选择器.
叫法源自他们与类相似。
1.UI伪类选择器：当元素处于某个状态时，为该元素应用样式。
2.结构化伪类选择器：根据文档的结构来添加样式，比如`:first-child`.

4.伪元素选择器
常见的有`::first-letter,first-line,befor,after`.
叫法问题书中所是相当于替类添加了虚拟元素。看个例子：
```
<p>This is a example .</p>
当我们想为This中的T字母加上特性，常规做法就是：
<p><span>T</span>his is a example .</p>
我们给它添加一个span元素，然后用于制作选择器。
```
毕竟要想施加特效，首先得把元素找到。故而有人称之为伪元素。

5.CSS中三大核心：继承，层叠，特指

继承：并不是所有属性都会被继承。一般能被 继承的是文本相关的属性，比如字体，颜色。但是边框，边距等属性不会被继承，因为继承下来没有任何意义。
考虑如下代码:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Example</title>
    <style>
        nav{
            border: thin solid black;
            font-style: italic;
            font-family: "Sitka Heading" , "Times New Roman";
            font-size: x-large;
        }
    </style>
</head>
<body>
<h1>CSS Test </h1>
<nav>
    <a href="#">Home</a>
    <a href="#">Index</a>
    <a href="#">Others</a>
</nav>
</body>
</html>
```
上面例子中可以看到，`nav`元素是三个`a`元素的父元素。我们给`nav`元素设置了边框样式，但是子元素并未继承。但是文本相关属性确继承了。

层叠：
1.样式表之间安装顺序和权重进行排序
2.样式表内部安装特指度进行排序。
3.同特指度后面的样式规则占优。
4.显示声明的规则高于所有继承的样式规则（忽略特指度比较）.
为什么会有层叠?
对同一元素的同一属性进行设置，导致样式冲突，故而有了决议机制，决定采用哪个规则。如果根本不存在冲突，那么也不会存在层叠。
5.样式规则中出现了`！important`，那么此属性值权重被提升到最高，会让样式应用脱离正常的顺序。
6.特指度计算：`I->C-E`规则。`id,class,element`，每出现一个就加一。看几个实例：
````
p {} #特指度 001
p.name {} #特指度011
P P.name ol.other li #idv #特指度 124 四个元素，两个类，一个id.

```

6. LoVe HA原则:用于设置`a相关`伪类时的顺序。`：link, :visited,:hover,:active`。
7. `em,ex`的使用：其实`em`概念很好理解，但是有的书讲的的确太乱，就说了句相对单位。查理下资料，`em`的值最初可能来源于字体`M`的宽度，但是在`css`中，情形却不是如此。看个具体的例子:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Example</title>
    <style>
        nav{
            border: thin solid black;
            font-style: italic;
            font-family: "Sitka Heading" , "Times New Roman";
            font-size: x-large;
            background: #eeeeee;
        }
        div{
            font-size: 2em;
        }
        p{
            font-size: 2em;
        }
    </style>
</head>
<body>
<h1>CSS Test </h1>
<nav>
    <a href="#">Home</a>
    <a href="#">Index</a>
    <a href="#">Others</a>
</nav>
<div>
    Just a test .
    <p>This is a test .</p>
    <p>Another test .</p>
</div>
</body>
</html>
```
在上面的`div`块中，我们设置了文本里，并用`em`单位设置了字体大小。最初我们很好奇，`em`是相对单位，那么当我写下`font-size：1em`倒是是相对谁？我并没有在`css`表中指定任何绝对大小。此时的`1em`会查找父元素也就是`body`的字体大小。因为`body`存在默认值，所以我们是相对body进行设置。其实只需要知道我们是相对什么进行设置即可。