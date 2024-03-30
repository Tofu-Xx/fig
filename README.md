## fig 属性

### 原子样式

#### 一般写法

```javasrcipt
<div width:100px></div>
```

> 原子样式一般写法与 css 语句写法基本一致.
> fig 写法: width:100px
> css 写法:width: 100px;
> _如果你愿意的话,原子样式也可以在末尾加分号_
> px 单位通常可以省略但是也有个别例外

- 注意一个 html 属性不可有空格

```javasrcipt
<div padding:10_5_20_15></div>
```

> 所以 fig 复合属性用下划线分隔,而 css 的复合属性是用空格分隔的

#### 属性映射

```
    w: "width",
    h: "height",
    p: "padding",
    m: "margin",
    ml: "margin-left",
    mt: "margin-top",
    mr: "margin-right",
    mb: "margin-bottom",
    pl: "padding-left",
    pt: "padding-top",
    pr: "padding-right",
    pb: "padding-bottom",
    t: "top",
    b: "bottom",
    l: "left",
    r: "right",
    w: "width",
    h: "height",
    p: "padding",
    m: "margin",
    ml: "margin-left",
    mt: "margin-top",
    mr: "margin-right",
    mb: "margin-bottom",
    pl: "padding-left",
    pt: "padding-top",
    pr: "padding-right",
    pb: "padding-bottom",
    t: "top",
    b: "bottom",
    l: "left",
    r: "right",
    pos: "position",
    bor: "border",
    bgc: "background-color",
    borr: "border-radius",
    fs:"font-size",
```

> 以上是内置的属性映射,所以上面一般写法的例子也可以这样写

```
<div w:100px></div>
```

> 也可以自定义属性映射,如下

```
<body>
  <div c:red>!!!</div>
</body>

<script>
  setAttrMap({
    c: 'color',
  });
</script>
```

#### 属性值映射

> 同上,不过属性值没有内置的映射,你可以发挥你的想象自行设置,比如

```
<body>
  <div c:red display:\>!!!</div>
</body>

<script>
  setAttrMap({
    c: 'color',
  });
   setValMap({
    '\\': 'none',
  })
</script>
```

- '\\\\'前面的反斜杠是用于转义,所以原子样式中写的是一个反斜杠

#### 简写形式

```
<div w:100px></div>
```

> 我们把映射为 css 属性的部分称为 fig 属性
> 映射为 css 属性值的部分称为 fig 属性值
> 当 fig 属性值以数字开头时,我们可以把冒号省略
> 所以这个例子最简单的写法如下

```
<div w100></div>
```

_px 通常可以省略,上面有提到过_

### fig 函数

> fig 函数的声明其实就是写一个 css 类样式
> 只是在使用类样式的标签上不用写类名,是类似函数调用的写法

#### 空参

```
<style>
  .center {
    display: grid;
    place-content: center;
  }
</style>

<body>
  <div center()> lorem </div>
</body>
```

> 当然,你也可以用 class

```
  <div class="center"> lorem </div>
```

> 但是 fig 函数的写法是可以传参的哦

#### 默认传参

```
.wh {
  --1: 100%;
  --2: transparent;
  width: var(--1);
  height: var(--1);
  background-color: var(--2);
}

  <div wh()></div>
  <div wh(100)></div>
  <div wh(100,red)></div>
```

> 类中写上 css 变量,变量名 1,2 代表传参位置
> 参数根据位置直接传 fig 属性值就可以

1. div 没传值,相当于直接用类名
2. div css 变量--1 被传入的 100px 覆盖,
3. 同理

#### 指定传参

```
.test {
  --width: 100%;
  --height: 100%
  --c:transparent;
  width: var(--width);
  height: var(--height);
  background-color: var(--c);
}

  <div wh()></div>
  <div wh(width100)></div>
  <div wh(height100,c:red)></div>
```

> 这里 fig 函数的参数写法类似于原子样式,前面的是对应的 css 变量,不是 fig 属性,这样就可以选择性传参了.
> 不过传入的是 fig 属性值,也就是说,也可以做属性值映射的

#### 内置函数

```
.center {
  display: grid;
  place-content: center;
}
.wh {
  --1: 100%;
  --2: transparent;
  width: var(--1);
  height: var(--1);
  background-color: var(--2);
}
.innerRow {
  display: flex;
  flex-direction: column;
}

.innerCol {
  display: flex;
  flex-direction: row;
}
```

### 行内选择器

- 原子化的弊端就是当有相同样式的时候需要写相同的原子样式
- fig 选择器就是来解决这个问题的

#### 选择器

> css 选择器能做的,fig 选择器基本都可以
> 由于 fig 选择器是以 html 属性的形式书写的
> 所以它在一个固定的标签上
> 所以它一定是一个联合选择器
> fig 选择器以所在的标签为参考系,这是他的魅力所在...
> 嗯么,那么..

```
  <div +.box{}> lorem </div>
```

> 例如上面这个例子就类似于下面这个 css 选择器

```
div+.box
```

> 效果是一样的,但如果你看一下控制台,就会看到实际解析出的选择器长的十分复杂且怪异

- css 会选择所有 div,而 fig 只是所在的 div
- 或许应该这样表示

```
所在标签+.box
```

- fig 选择器也支持伪类和伪元素选择器后面再作解释

#### 选中后设置样式

> 直接在大括号中写就好,用分号作分隔
> 原子样式或者 fig 函数都可以

```
  <div +.box{bgc:rgb(225,0,0);h100;center()}> lorem </div>
```

- 虽然整体很长,但本质还是一个 html 属性,所以不能有空格,否则会视为多个 html 属性
- 注意 rgb 是 css 函数,center 是 fig 函数,都是可以使用的,css 函数可以看做是 css 属性值的一部分

### 子级选择器

- 由于 css 的子级选择器的连接符是>,所以如果写在 html 属性中的话

```
<div >test > lorem </div>
```

> 看出问题了吗
> 所以 fig 选择器的子级分隔符做了修改,改为了反斜杠

```
<div \.box{w100%}> ... </div>
```
> 等于

```
所在标签>.box{
  width:100%
}
```

### 后代选择器
- 后代选择器与子级选择器有同样的问题,css的后代选择器分隔符是空格,在html属性中无法使用
> 所以 fig 选择器的后代分隔符做了修改,改为了两个反斜杠
> *挺合理的吧 哈哈哈*
```
<div \\span{color:#6af}> ... </div>
```

### 其他选择器
> 其他的与css一样,下面举一些栗子

```
<div  ::after{content:"你好呀"}
      \:nth-child(2){bgc:#fab}
      \#foo,\.bar,\\span{fs2em}      
> ... </div>
```
> 哈哈哈,还习惯嘛,这是div标签中有三个属性哦
- 第三个是并集选择器,每个都是相对于所在标签的
- 也可以写交集,对于自身的交集,比如
```
<div .active{bgc:red}> </div>
```
> 当自身有active类时,背景色变红
## fig 标签

> 弹性盒可以解决百分之八十的布局
> 而弹性盒无非就是横着布局或竖着布局
> 所以...

### 行标签 <f-row\></f-row\>

```
  <div wh(100) \f-row{h100%}>
    <f-row></f-row>
    <f-row></f-row>
    <f-row></f-row>
  </div>
```

> div 中有三行
> f-row 会使父盒子纵向弹性布局

### 列标签 <f-col\></f-col\>

```
  <div wh(100) \f-col{w100%}>
    <f-col></f-col>
    <f-col></f-col>
    <f-col></f-col>
  </div>
```

> div 中有三列
> f-col 会使父盒子横向弹性布局

### 标签注意事项

> 行标签和列标签是可以嵌套使用的
> 行标签和列标签做兄弟节点时,列标签是不起效的
> 当然你可以选择不用这两个标签
> 用内置fig函数 innerRow()和 innerCol()一样方便
