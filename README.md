# 大众美男典范霍小强的笔记

## javascript赋值

>赋值就是把某一个值赋给变量。

### 我凭什么要把值赋给变量？

变量相当于名字。

拿我举例，如果我没有名字，当别人叫我帮忙的时候，就只能说：

“那个个头不高、颜值爆表、头发很硬、坐在角落的小哥哥，过来帮我一下呗！”

而有名字的情况是：

“小强快来！”

可见变量赋值的意义在于**便于使唤**。

### 基本类型的赋值

基本类型的赋值，好比在每个盒子里放东西。

#### 直接赋值

例如，

```$xslt
var a = '手机'
console.log(a)  // '手机'
```

相当于，给一个盒子起名为a，并放进去一个字符串‘手机’。

#### 将变量赋值给变量

例如，

```$xslt
var a = '苹果'
var b = a
a = ''
console.log(a)  // '' 
console.log(b)  // '苹果' 
```

当`var b = a`时，相当于：

给一个盒子起名为b，并偷看一下盒子a里面放的什么，然后自己里面放同样的东西。

当`a = ''`时，相当于：

盒子a里面原来的东西不要了，改放一个`''`进去。

但是，这并不会影响盒子b中的值。

因为，在盒子a里面发生变化的时候，盒子b并不关心。

只有将变量a赋值给变量b，即`b = a`时，

b才会出现偷看行为，进而使自身的值和a的值一样。

可见，**赋值就是复制**，特点是**赋值过后互不影响**。

好比我把感冒复制给朋友，我吃完药好了，并不能代表他也好了。

### 引用类型的赋值

引用类型的赋值，看上去是共享，实际还是复制。

#### 栈和堆

首先，基本类型采用栈存储，一个萝卜一个坑。

前面也说到，基本类型的赋值，就像在每个盒子里放东西，比如，

我在a盒子里放个香蕉、

我在b盒子里放个手机、

我在c盒子里放个老鼠、

**我在d盒子里放个房子**...

问题出现了，

之前，我们在盒子里放一些很傻很天真的东西，基本没问题，

但是，盒子里可以放房子吗？

这时候，我们进一步认识一下我们的盒子（栈存储）有什么特点？

* 盒子按顺序排列
* 每个盒子只能存放一件物品
* 每个盒子都不是很大

显然，我们的盒子不足以装下房子。

而且常识告诉你：

房子里倒是能**堆**很多的盒子，因此房子就是堆存储。

堆存储就像找了一片空地，然后在上面尽情放盒子（*请不要想到《我的世界》*）。

特点就是存的多、存的乱。

理解堆和栈的区别，也可以参照公交车，

每个座位，

有序、只能坐一人、大小有限...

好比栈；

其它地方，

能挤下一堆人，很乱...

好比堆。

对象采用的就是堆存储。

#### 什么是引用类型

我们知道，javascript引用类型包括对象。

先随便来一个对象:

```$xslt
var a = {}  // 堆存储，相当于建了个房子，名为a
```

再随便来一个数字:

```$xslt
var b = 10  // 栈存储，相当于选了个盒子，名为b
```

再随便来一下：

```$xslt
b = a
console.log(b)  // {}
```

太随便就容易出问题：

原本b是一个正经盒子，a是一个正经房子，

执行`b = a`之后，b变成了`{}`，

根据上面说的基本类型的赋值，这是不是在说

盒子b虽然之前只是一个小盒子、

但是偷看了一眼房子a之后、

自己发奋图强变成像房子a一样大的盒子、

并复制了房子a里面的东西？

不是的。

盒子b并没有为了复制房子a里面的东西而变大，

实际上，a其实**从头到尾都只是一个盒子**、而不是房子，仅管我们看到是a被赋值了一个堆存储的对象。

为什么呢？

因为引用类型只暴露一个地址给我们，

操作引用类型的数据时（比如赋值），我们也只是在操作这个地址、引用、指针...爱叫啥叫啥。

这就好比，你送女朋友戒指，可以直接放到她手里，这是基本类型；

你送女朋友法拉利，并非把法拉利直接放到她手里，而是把车钥匙放到她手里，这就是引用类型；

你送女朋友房子，并非把房子直接交给她（除非你们是蜗牛），而是把房钥匙交给她，这也是引用类型。

从赋值上来进一步认识引用类型：

#### 直接赋值

开始说过，

>变量相当于名字。

另一个事实是，

我们**只能给盒子起名字，不能给房子起名字，但是我们能拿到房子的钥匙**。

这就是为什么说，a其实从头到尾都只是一个盒子。

`var b = 10`相当于取一个盒子叫b，然后里面放啥啥啥，这没有问题；

由于我们不能给房子起名字，

所以`var a = {}`肯定不是说：取了一个房子叫a，然后里面放啥啥啥。

其实，和`var b = 10`的解释一模一样，`var a = {}`也相当于

取了一个盒子叫a，然后里面放啥啥啥。

只不过是，b盒子里面放很傻很天真的东西，

a盒子里面放很傻很天真的钥匙，这把钥匙对应一个大房子。

引用类型的直接赋值就是把钥匙放到对应盒子里。

##### 为什么只给盒子起名字？

代码中，会出现很频繁的变量赋值行为，

为了保证运行速度，这些行为被优先安排在一批有序的盒子中，偷看、复制、再偷看...

可以说，我们大部分时间在玩盒子。

可想而知，如果换成玩房子的话，要费多大的力气。

但是呢，房子在我们的程序中也有着不可或缺的作用，

这时候它就暴露出一个可以找到它的钥匙，相当于它的**联系方式**，

然后放进相应的盒子里，并说：

当你需要我的时候，我会在你身边。

正是因为这样，我们既便于使唤房子，又便于操作房子里的东西。

#### 将变量赋值给变量

```$xslt
var obj = {name: '小强'}
var obj2 = obj
console.log(obj2)   // {name: '小强'}
```

首先，`var obj = {name: '小强'}`是引用类型的直接赋值，

相当于找到一个盒子名obj，把`{name: '小强'}`这个房子的钥匙放进盒子obj里面。

而`obj2 = obj`可以说和基本类型的变量赋值给变量一样，

盒子obj2偷看一眼盒子obj中放的东西，复制一下，自己里面放同样的东西。

喜出望外的是，竟然是一把对应某个房间的钥匙！

这时，obj2就和obj一样，都能访问这把钥匙对应的房间了。

所以引用对象的赋值都是操作钥匙。

#### 引用类型赋值面试题

例一、

```$xslt
var a = {n: 1}
var b = a
a.x = a = {n: 2}
console.log(a.x)    // undefined
console.log(b.x)    // {n: 2}
```

逐句翻译吧：

1. `var a = {n: 1}`

取一个盒子名a，建一个房子，钥匙放到盒子a里面；

房子里有个盒子n，放着1。

2. `var b = a`

取一个盒子名b，盒子b偷看一下盒子a，哇哦，一把钥匙，

盒子b里面也有了这把钥匙，也能去访问这个房间了。

3. `a.x = a = {n: 2}`

* 变量赋值是从右向左的
* 对象用.赋值的时候，就是操作对象的某个属性，如果没有该属性就添加一个

我们通过盒子a中的钥匙，来到了这把钥匙对应的房间，

然后，我们在这个房间取一个盒子名x，并企图在里面放东西。

执行到`a.x = a`的时候，我们还以为：

是把盒子a里面的钥匙，放进我们所处房间的盒子X里面吗？

差点就是了，但是后面又有`=`赋值。

根据变量赋值从右向左，

我们**暂时**先不在这个房间里的盒子x放东西，而是优先执行`a = {n: 2}`，

这条语句显然是引用类型的直接赋值，

即建了一个是`{n: 2}`这种样子的房子，然后把钥匙放到盒子a里面。

在栈和堆里面我们提到过：

> 每个盒子只能存放一件物品。

因此，盒子a首先会抛掉之前的钥匙，然后存下这把新的钥匙。

刚才我们拿着盒子a之前的钥匙，进到对应的房间，企图在房间的盒子x里放东西；

然后，发现后面还有赋值行为，所以优先执行后面的赋值行为。

但是，当时我们只是暂停，而不是放弃。

换句话说，是不忘初心，有始有终。

当初我们进的哪个房子，想在哪个盒子放东西，

现在我们就回到哪个房子，然后给哪个盒子放东西，

从`a.x = a`可以看出，我们在盒子x里放的是盒子a的钥匙，

在这个例子中，盒子a中现在的钥匙就是能打开`{n: 2}`这间房子的钥匙。

虽然说，

> 变量赋值是从右向左的。

但是，**代码执行是从左向右的**。

无论后面发生了多大变化，`a.x`都是最先执行的，它的作用就是：

通过钥匙来到一个房间，取盒子x，然后等着在里面放东西。

后面的代码，只能影响这个盒子里放什么东西。

于是，时过境迁：

盒子a里，抛弃旧房子钥匙，放进了一把新房子钥匙，等价于

```$xslt
a = {n: 2}
```

盒子b里，还是旧房子的钥匙。

同时，因为在盒子a换钥匙之前，我们通过盒子a拿到旧钥匙来到旧房子，

并将盒子a换钥匙之后的新钥匙，放进了旧房子的盒子x里面，那盒子b等价于

```$xslt
b = {
    n: 1,
    x: {n: 2}
}
```

也可以将这个例子稍加处理：

```$xslt
var xiaoMing = {moneyBox: 1}
var xiaoQiang = xiaoMing
xiaoMing.keyBox = xiaoMing = {moneyBox: 200}
console.log(xiaoMing.keyBox)    // undefined
console.log(xiaoQiang.keyBox)    // {moneyBox: 200}
```

再逐句翻译：

1. `var xiaoMing = {moneyBox: 1}`

小明有一把房钥匙，这个房子里有个钱柜，里面放着1元钱。

2. `var xiaoQiang = xiaoMing`

小强偷偷复制了一把小明的房钥匙，从此他也可以进出小明的房子。

3. `xiaoMing.keyBox = xiaoMing = {moneyBox: 200}`

小明在此房子里做了一个钥匙柜，这个钥匙柜能自动生成一把小明口袋里的钥匙（**`xiaoMing.keyBox = xiaoMing`的作用，可能有点超现实**），

但是小明想，我口袋里的钥匙现在就是这个房子的钥匙，放在我的钥匙柜里也没什么意义，

不如这样吧，我再买一套房子，**把口袋里的钥匙替换成新房子的钥匙**，那这个钥匙柜里不就存下新房子的钥匙了吗。

于是，小明果断又买了一套房子，这个房子里也有个钱柜，里面放200元钱。

小明正准备回旧房子呢，突然想起来，自己口袋里的钥匙已经替换成新房子的钥匙了，

现在他只能进新房子，而进不去旧房子了，郁闷...

再说小强，

小强当初复制的是小明旧房子的钥匙，所以小强依然能来到这个旧房子，

进来后发现，多了一个钥匙柜，并且里面放着一把钥匙，

没错，这就是小明新房子的钥匙。

所以现在的局势很明朗了：

小明只有新房子的钥匙，只能进新房子（*而且他应该觉得旧房子已经没人能进去了*）。

而小强有小明旧房子的钥匙，

同时这个房间里还有小明的新房子的钥匙，所以小强也能进小明的新房子。

用代码表示，就相当于

```$xslt
xiaoMing = {moneyBox: 200}
xiaoQiang = {
    moneyBox: 1,
    keyBox: {moneyBox: 200}
}
```