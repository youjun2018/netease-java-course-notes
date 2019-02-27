##  第四章 抽象和接口
###  4.1 抽象类
#### 4.1.1 抽象类
前面使用 Shape 类可以话出很多形状。父类源代码如下：  
![abstract](image/part2/abstract.png)  
在 public 和 class 中间多了一个 abstract。类中唯一一个函数在 public 和 draw 中间也有 abstract。这个单词的意思是 **抽象**。为什么要这样？  

##### Shape 是什么形状？
* Shape 类的 draw() 函数应该如何写？
![abstract2](image/part2/abstract2.png)  
我们现在 Shape 类家族如上图所示，从 Shape 类派生出了 Rectangle Ellipse Square Circle 等各种各样的形状。在 Shape 里面我们定义了 draw() 的函数，这个函数定义出来以后，所有的 Shape 子类都有一个 draw() 的函数。假如我们现在来写 Circle，这个 Circle 的 draw() 怎么做？很简单，画个圆；如果做个 Square, Square 的 draw()怎么做呢？很简单，画个矩形。但是如果我和你说现在有个 Shape，让你画个形状，你画什么？也就是说像 Shape 这个类在程序中的作用是什么？它提供了 Rectangle Square Ellipse Circle 等公共的概念，公共的父类。在这个公共概念当中，它提出了所有的 Shapes 不管哪种形状，都应该会 draw()，这是讲多态时提的概念。有公共的父类提出 draw() 这件事情，以至于所有的子类都能够 draw()，这就是这个公共父类存在的意义。如果没有这个 Shape，那么 Circle 和 Rectangle 就没有关系了。因为有 Shape，可以认为 Circle 和 Rectangle 都是 Shape，所以 Shape 类的意义就在这。我们没有想过要产生 Shape 类的一个对象，如果有一个 Shape 类的对象，你就没有办法说我到底要你怎么 draw()。因为它没有任何存在的意义，他只是表达一种概念。在这种情况下，我们最合适的方式是让这个类成为一个 abstract 类，即抽象类。而这个抽象类中的那个 draw() 方法，它在这个类中没有存在的意义，他的意义就是告诉别人说所有的 Shape 类的子类都有一个 draw() 函数。所以这个函数本身也应该是一个抽象的，abstract。  

从语法上来说，由于这个 draw() 是抽象的，所以 draw()函数没有表示函数体的大括号，加上会报错。如果有一个函数是抽象的，那么这个类就是抽象的，要加关键字 abstract。因为抽象类还有另外一层意思，就是抽象类不能产生对象。假如说某个类中有一个抽象函数，但是这个类不是抽象的。类不是抽象的意味着这个类可以产生对象了，如果我们制造了这个类的对象 s，那么 s.draw() 改怎么做呢？这个 draw() 函数没有定义，没有 body，我们只是声明这里有个 draw()，没有给出函数体呀，s.draw() 依然无法执行。所以只要一个类中有一个函数时抽象的，那么这个类就是抽象的。  

##### 抽象函数/抽象类
* 抽象函数 -- 表达概念而无法实现具体代码的函数
* 抽象类 -- 表达概念而无法构造出实体的类

从定义上来说，抽象函数就是表达概念而无法实现具体代码的函数，比如说，Shape 类中的那个 draw()；抽象类就是表达概念而无法构造出实体的类，一旦你这个类中有一个抽象函数了，这个类就是抽象类。

* 带有 abstract 修饰符的函数
* 有抽象函数的类一定是抽象类
* 抽象类不能制造对象
* 但是可以定义变量
    + 任何继承了抽象类的非抽象类的对象可以赋给这个变量

在 Java 使用修饰符即关键字 abstract 单词的本意就是抽象，用这个单词去修饰函数、修饰类去表明它是抽象的。抽象类不能制造对象，但是可以使用抽象类定义变量，当然将来赋给这个类定义的变量的对象一定是这个类的非抽象的子类，才能赋给这个类的抽象变量。这个抽象类的变量的意思就是任何，比如 Shape 类的变量 s，那指的就是任何 Shape 类的子类的对象都可以由这个 s 来管理，指的是管理子类的对象的变量。  

##### 实现抽象函数
* 继承自抽象类的子类必须覆盖父类中的抽象函数
* 否则自己成为抽象类

当我们有一个子类，这个子类继承了抽象类以后呢，那个抽象类里面的所有的抽象函数，都必须要被这个子类实现，即被它覆盖，这种覆盖我们叫做**实现**。否则这个类自己就成为抽象类。如果一个类继承了一个抽象类，但是没有实现所有的抽象方法，那个这个类就是抽象类。  

##### 两种抽象
* 与具体相对
  + 表示一种概念而非实体
* 与细节相对
  + 表示在一定程度上忽略细节而着眼大局

在计算机中，抽象有两种不同的意义，只是很多人没有意识到这一点。我们会在两种不同的语境下用抽象这个词，它们的含义有相似的地方，但也有细微的不同。两种抽象，一种抽象和具体相对，比如 Shape 类的抽象，就和具体相对，因为 Shape 表达的是概念而不是具体的东西，Circle 才有可能是具体的东西，Line 才有可能是具体的东西，所以和具体相对的是一种抽象。但其实还有另外一种抽象，是和细节相对，比方说当我看到一辆汽车的时候，普通人会说是蓝色的轿车，他不会说这个车的发动机是4缸的，是什么样的变速箱，正常人不会想这些事情，人的思维都会在一定程度上掩盖细节，不会看到一定层次上细节下面的东西，这是另外一种抽象，所以在计算机的术语体系当中实际上是存在两种不同的抽象，两种抽象，两种抽象的能力和实现。


###  4.2 接口
####  4.2.1 狐狸和兔子的例子
刚才看到的细胞自动机，它是在网格上面有细胞，这个细胞有两种状态，要么是活的，要么是死的。现在想把这个故事向前推进一步，我们想做一个农场。  
##### 狐狸和兔子
* 狐狸和兔子都有年龄
* 当年龄到了一定的上限就会自然死亡
* 狐狸可以随机决定在周围的兔子中吃一个
* 狐狸和兔子可以随机决定生一个小的，放在旁边的空的格子里
* 如果不吃也不生，狐狸和兔子可以随机决定向旁边空的格子移一步

有块地，这块地有狐狸和兔子，它们相互之间有关系，或者它们的互动就比较多。细胞只有死的活的两种状态，当然对于兔子和狐狸来说它们也有死的活的状态，但更复杂的是它们都有年龄。随着程序的进行它们的年龄不断增大，它们的年龄有一个上限，到了上限他就死了。另外呢狐狸和兔子是捕食者和被捕食者的关系，所以狐狸会在它的周围、那一圈，九宫格，8个方格里面有没有兔子，一定几率它会吃一个兔子，吃了兔子之后它的年龄上限就会提高。狐狸和兔子都会生产小狐狸小兔子，有一定几率生一个小的放在旁边，然后那个小的也逐渐张起来。如果不吃也不生，狐狸和兔子也可以移动，走开，在一定几率下。  

我们想实现这么一个复杂的仿真程序，这就比原来的细胞，只有活或死的状态复杂的多。我们看做出来的效果怎么样。  
![abstract3](image/part2/abstract3.png)
这里红色的是兔子，黑色的是狐狸。它们颜色会随着年龄的增长逐渐变淡，越来越淡，淡到最后看不见就死了。在这个过程中狐狸会吃兔子，兔子会来回走动，每次一格，走完若干步后就停下来，形成最终的状态。  

这个程序怎么做呢？当然这个程序我们还是看到和刚才的细胞自动机有相似的元素，都有网格，网格里面都有颜色。但是这里增加了两种东西，这里有狐狸，有兔子，每一种东西随着年龄的增长，颜色会发生变化，变淡，一直到没有为止，会有新的元素加进来。整个程序的架构会是什么样的呢？  

![abstract4](image/part2/abstract4.png)  
我们还是维持了 field 包里有 Field 和 View 这种架构，就是数据和表现是分离的。Field 表达数据，View 表达表现。我们的 Cell 还是那个 Cell。我们用 Fox 和 Rabbit 来分别表达狐狸和兔子。但是在这个类中，Cell 类的定位就很尴尬。  

##### Cell 类的地位很尴尬
* 在 Cells 程序中它表达了细胞
* 但是同时它也表达了放在网格中的一个格子
* Fox 和 Rabbit 是否应该从 Cell 继承？

我们在细胞自动机里面，Cell 其实表达的是细胞，细胞有活的有死的，死的细胞是一个白的的框框，活的细胞是一个黑色的框框。Cell 这个单词本意是格子，最开始的意思时候格子，后来用它表达细胞。细胞自动机里面细胞和格子正好是同一种东西。但是到了兔子和狐狸故事当中呢，它的角色就很尴尬。它到底是表达格子呢还是格子里面的东西，因为我们现在的局面是说，在 Field 里面每一个格子其实是三种情况，要么没东西，要么是狐狸，要么是兔子。所以 Cell 到底表达的是什么？也就是说我们的狐狸和兔子这两个类将来做出来后，它们上面的一个父类应该是什么？我们知道从问题本身的角度来说，狐狸和兔子如果有一个共同的父类的话，它们的父类应该是动物，比如 animal，这很合理。因为这这个程序里面，狐狸和兔子有很多相同的动作。比如说每经过一轮它们年龄都要增长，它们都要生小 baby。他们要移动，它们有很多相同的动作。它们相同的动作应该放到相同的父类中去，比如 animal。这是从媒体数据库哪里得到的经验。我们的 CD 和 DVD 有相同的东西应该拿出一个 item 类来，我们 fox 和 robbit 有相同的东西就应该拿出一个 animal 作为他们的父类，可是这时 Cell 怎么办？我们现在的关系如下：  

我们有一个叫 Animal 的类，从它派生出了一个叫 Fox 和 Rabbit 的类。这个关系看着很顺。然后我们有一个 Field 类，然后旁边有一个 View 类，它们按照细胞自动机的关系保持不变。一个表达数据，一个表达表现。在 Field 里面我们放的是 Cell，Field 知道有这种东西，然后它管理 Cell，现在我们希望说，这个 Field 里面能够放 Fox 和 Rabbit。对于 Field 来说，既然我们之前 Field 管着 Cell，那么他应该说，比方说我们有个 place(r,c,) 函数，我们 place row 和 column 一个 cell 进去。当然现在我们想把一个 Rabbit 放进去，通过 place 放进去的话，那么 Rabbit 应该是 cell 的子类。但是我们让 Rabbit 同时从两个类得到继承，那么这就形成一个事实上的多继承，一个类从两个类得到继承，这就是多继承，而**多继承在 Java 是不被允许的**。**事实上所有的 OOP 语言都不支持多继承，只要 C++ 才支持多继承。** 因为多继承从编程角度来说，从语言实现角度来说，有很多不好实现的地方，所有所有 OOP 语言都不支持多继承。我们不能让 Rabbit 一方面作为一个 Animal，一方面多为一个 Cell。  
![jiekou](image/part2/jiekou.png)  

这样不行的话，是不是说 Animal 作为一个 Cell 呢？如果是这样又带来一个问题，就是它在语义上时含糊的。Animal 是动物，动物是一种特殊的细胞？或者说动物是一种，假如这里 Cell 不在表达细胞，而是格子，是 Field 里面的一个格子，是因为 Field 需要有一种类型，Field 只能管它自己认识的类型。我们的问题其实是在这，Field 必须要有一个它认识的累心个，它才能能够管，而现在它的代码已经写好了，它管着就是 cell 这种类型。如果现在我们说 Animal 是一种 Cell 行不行？有一个很多大的问题就在于异常语句，Animal 怎么就是 Cell 了呢？Animal 为什么是个格子，Animal 不是格子。我们不认为从语义上来说 Animal 和 Cell 中间联系是恰当的。这种联系使 Animal 是一个很奇怪的类。使得我们本来，Animal \ Fox \ Rabbit 这些类的家族关系其实和 Cell 没有关系，和 Field 没有关系，和 View 更加没有关系。因为 Animal 派生出了 Fox 和 Rabbit，这是动物自己的继承体系，自己的一个家族体系，在这个体系里面你要做什么事，和你要不要在这块田里面，要不要在 Field 和 View 这个架构里面放进去是没有关系的。那怎么办？Field 说你要给我一个 Cell 我才能管你的东西，Animal 说就是 Animal，Animal 不是 Cell，怎么办？  
![jiekou2](image/part2/jiekou2.png)

####  4.2.2 接口
##### 接口
* 接口是纯抽象类
    * 所有的成员函数都是抽象函数
    * 所有的成员变量都是 public static final

于是我们的解决方案是这样的，我们把那个 Cell 改造一下。它不是一个类吗，我们把它从类改造成一个接口，interface。改造成接口之后它就不在是类了，它不在表达可能是具体的东西，因为**类表达一个东西，而接口表达的是概念，表达的是规范**。在这个里面，Java 的接口其实它是一个纯的抽象类，也就是说在这个接口里面，所有的函数都是 abstract，因此你不用说他是 abstract。所有的变量，如果你有变量，如果一个接口中有变量，他实际上是 public static final。表达的意识是，public static final 表达的是其实这个变量不属于任何对象，它属于整个类。第二，因为它是 final，所以他不会改变，因此它其实就是常量。这是一个编译时就可以知道值的东西，public static final。所以这样的一个东西就成为一个接口。下面看一下代码是什么样子。  
![jiekou3](image/part2/jiekou3.png)  

这就是我们的 Cell，我们这个 Cell 空空的啥也没有，只是说可以 draw。Cell 要起的作用就是，所有实现 Cell 这个接口的类的对象可以被放在 Field 里头去，因为 Filed 对这个 Cell 的所有的管理权限就是放进去拿出来，然后将来 view 要拿这些 Cell 去 draw，就这样一个关系。所以从图来看，我们就变成这样子。  
![jiekou4](image/part2/jiekou4.png)  

我们让 Animal 和 Cell 没有关系，可是呢，Fox 和 Rabbit 都去实现这个 Cell。实现了这个接口以后，Fox 对象就能放到 Field 里面去了，Rabbit 对象也能放到 Field 里面去了。能够放进去是因为 Field 说我要一个 Cell， Rabbit 说我实现了 Cell，Fox 说我也实现了 Cell，于是就可以放进去了。怎么去实现Cell 呢？  

![jiekou5](image/part2/jiekou5.png)  
我们来看 Fox。既然说实现我们就用一个新的关键字，叫 implements。同样的后面有 s，因为第三人称单数。他说 Fox 这个类是 Animal 的子类，同时它也实现了 Cell。Fox 是一种 Animal，同时它实现了 Cell，因此 Fox 可以被放到 Cell 里头去。  

![jiekou6](image/part2/jiekou6.png)
因为对于 Field 来说，Field 里面的 place 函数说我要一个 Cell，这个时候 Cell 的这个 o 是什么意思？Cell 本身是一个接口，接口的所有的函数都是 abstract，因此 Cell 一定不可能有对象，不可能有任何 Cell 的对象被制造出来。可是呢 Cell 标量 o 的意思是，任何实现了 Cell 接口的类的对象，都可以交给 o 这个变量。于是，Fox 也可以，Rabbit 也可以。对于 Field 来说，他不在乎你是 Fox 还是 Rabbit，你是不是继承 animal，跟他无关，他只管说你是不是一个 Cell，只要你是一个 Cell，你就可以给我，我就可以给你管起来，放进去，因为对于后面 View 来说，View 要用 Filed 的地方就在于，View 要去遍历整个 Field，让 Field 去拿到每个 Cell，然后让这个 Cell 去做 draw。我们的 Cell 就规定了这个 draw 的动作而已，其他什么都不管。  

![jiekou7](image/part2/jiekou7.png)
所以，对于 Fox 来说，它实现了 Cell 之后，它就必须去 Override 这个 draw，去实现这个 draw，把这个函数实际去做出来，然后他就能够在 View 和 Field 关系里头被画出来。  

我们回到主程序，我们看到和细胞很像，在主程序中，我们看到两层循环去往里面填东西，然后根据可能性，来放 Fox 或者 Rabbit。放到田里头去，然后把这个窗口给做出来，这和前面的细胞自动机几乎一样的。在 Start 里头，我们做了一定的步数，每一次做一步，然后让整个窗口 repaint()。在每一步里做的事情也是遍历整个 Fiel，拿到每个格子 Cell。其实我们放进去的是 Animal，所以我们可以 cast，造型让它成为一个 Animal，我们让这个 Animal grow()。  

 Animal grow做的事情也是很简单，就是 age++，岁数加1。如果岁数大于 ageLimit，那就 die()。die() 就 isAlive = false。  

 在 animal.grow() 之后，我们就判断，是不是还是活着的，如果不活着，我们就跟 Field 说把这个地方的东西给它 remove 掉。remove 做的事情也是很简单，就是把这个位置变成 null。如果是活的的，那就要做三个动作，移动，吃，生小baby。移动就是让 Field 去枚举出当前这个位置狐狸或兔子它周边空的neighbour，把这个地方交给 Animal 去 move。Animal move函数会拿到一个 Location，表达在 Field 里面的一个数组，在这个数组里面随机的找一个空的位置。当然在一定的几率下找一个随机的位置。然后返回那个位置。所以如果那个 animal 要移动，我们就让田 Field 去帮我们做这个移动的事情。吃比较复杂点，我们得到了所有的邻居，我们在邻居数组里面遍历一下，每个邻居拿出来说，an instanceof Rabbit，你是不是 Rabbit 的一个对象，如果你是 Rabbit，就把你加到 Rabbit 的数组里头去。这个遍历做完之后，得到当前这个邻居的兔子。如果有兔子，就让 animal 去 feed。对于 animal 来说，他的 feed 做的事情是什么也不吃。对于 Rabbit 来说，它的 feed 也是什么都不吃。对于 Fox 函数，它的 feed 函数就吃了。如果达到了一定的几率，就在他的邻居的兔子里挑一个兔子，然后把它吃掉，吃掉以后使用longerLife()，即自己的 agelimit 加2，寿命就边长了。如果决定吃，就返回吃了哪一个。Field 就把这个东西移走，从整个格子里移走。  

 第三件事情，我们来生 baby。每一次就让这个 animal 去 breed。Animal breed() 是一个抽象函数，就是 Animal 不管怎么 breed。对于 Fox 来说，breed 做的事情是说，如果 breedable，为什么呢，因为还有一个年龄问题。我们在 Animal 里面定义了一个 变量叫 breedableAge，可以生 baby 的年龄。isBreedable() 做的事情是，如果当前年龄大于等于 breedableAge，那么就可以生 baby。在 Fox 里面就判断一下如果现在是可以生的，并且符合一定的概率，我们就生一个出来，否则就 null。对 Rabbit 来说，这个也是一样的。对于主程序来说，业务逻辑我们让 animal 做 bread 动作。如果它觉得要 breed，他就给我一个 baby。如果给了一个 baby，就让 Field 随机的把它放在邻居的九宫格的那个八个的里头，找一个空的位置吧它放进去。这就是每一步做的动作，把每一步组合起来，
就得到了我们的视觉效果。  

代码在 网易云课堂 Java基础入门：面向对象程序设计 第四章 抽象和接口 4.2接口 2接口这一节。


###  4.3 内部类
####  4.3.1 内部类
```java
//: Parcle1.java
// Creating inner classes

public class Parcel1 {
  class Contents {
    private int i = 11;
    public int value() { return i; }
  }
  class Destination {
    private String label;
    Destination(String whereTo) {
      label = whereTo;
    }
    String readLabel() { return label; }
  }

  // Using inner classes looks just like using any other class, within Parcel1:
  public void ship(String dest) {
    Contents c = new Contents();
    Destination d = new Destination(dest);
  }
  public static void main(String[] args) {
    Parcel1 p = new Parcel1();
    p.ship("Tanzania");
  }

}

```


这个类叫做 Parcel1。在这个 class 里面出现了一个 class，叫做 Contents。这是定义在 类内部的类，这叫做内部类。Contents 是 Parcel1 的内部类，我们要解决很多问题，而且我们还有理解的一件事情是，现在的大多数编程设计语言都会遵循的一个原则，叫正交。正交的意思是说，这个语言当中出现了语言成分，这些语言成分应该是能够相互充分组合的。我们先来看内部类，然后再来体验正交是什么事情。这个 Contents 是 Parcel1 的内部类，它是 Parcel1 的成员，因此，现在我们又扩展了类的成员的种类。原来我们说类的成员可以有成员变量，成员函数，现在可以有成员类，它是成员。既然它是成员，他就遵循这个成员所有的东西。成员有什么，比如所它有访问属性，它可以有 static 和 非 static。所以这些事我们要展开去看。我们要解决的第一件事情是说，这样的一个程序，你看它有 Contents 类，还有 Destination 类，编译完成后会形成几个.class 文件？Parcel1 一定会有的，问题是 Contents 和 Destination 会不会有.class 文件。使用一下命令编译文件：  
```java
$ javac Parcel1.java
```
![innerClass](image/part2/innerClass.png)  

我们看到 Parcel1.class，Parcel$Contents.class,Parcel1$Destination.class。所以它仍然给每个类单独的生成一个.class 文件。单独的 .class 文件意味着什么？他们尽管是内部类，是成员，但是在类格上时独立的。或者换句话说，我们提到过一件事情，我们的类是动态被装载的。也就意味着当装载 Parcel1.class 的时候，那两个类要不要被装载其实是动态的。它们不一定被装载，或者至少不一定和这个它外围的那个类同时被装载。因为它们被分开，它们就可能这样，我说的是可能，不说说一定不会，或者一定要会，有可能被分开。我们做了这两个类，我们怎么去用它呢？  

在我们的 ship() 函数里头，这是它的外围类的函数，它可以去 new 一个 Contents，去 new 一个 Destination，可以用来做事情。但是我们这两个例子没有很充分的去用这两个类。我们的 main 函数去做一个 Parcel1 出来，然后去让这个 Parcel1 去做了一些事情。好像从这个地方看不出来到底发生了什么事情，但至少我们可以看到说，在外部类的某个函数里面可以直接的使用 Contents 那个内部类的名字，不需要用到什么 Parcel1.Contents 或者 Parcel1$Destination 的符号，直接用那个类的名字，因为我在那个成员里头。那我们先来做一件事情，验证刚才提到过得有可能不在同时装载。所以我们想验证一下说什么时候装载什么东西，还记得我们怎么去 trace，去跟踪类的装载这件事情。可以使用 static 静态初始化块对不对。所以我们放一些静态初始化块。改动后的代码如下：  
```java
//: Parcle1.java
// Creating inner classes

public class Parcel1 {
  static {
    System.out.println("Parcel1.class loading");
  }
  class Contents {
    static {
      System.out.println("Contents.class loading");
    }
    private int i = 11;
    public int value() { return i; }
  }
  class Destination {
    static {
      System.out.println("Destination.class loading");
    }
    private String label;
    Destination(String whereTo) {
      label = whereTo;
    }
    String readLabel() { return label; }
  }

  // Using inner classes looks just like using any other class, within Parcel1:
  public void ship(String dest) {
    Contents c = new Contents();
    Destination d = new Destination(dest);
  }
  public static void main(String[] args) {
    System.out.println("main()");
    Parcel1 p = new Parcel1();
    System.out.println("after new");
    p.ship("Tanzania");
  }

}
```
运行出现如下错误：  
![innerClass2](image/part2/innerClass2.png)  
为什么显示内部类 Parcel1.Contents 中的静态类声明非法吗？刚才提到一个词叫做正交。它是内部类，它是成员，它要符合成员所能加上去的所有的修饰符规则。现在我们没有给他加上 static，没有给他加上 static，意味着它不是 static。比如说如果成员变量加上 static 意味着什么？意味着他在所有的对象当中都是一样的值，从本质上来说意味着它的位置在哪里，在类对象里面，他什么时候被装载，那个静态的成员变量什么时候被初始化，类装载进来的时候就初始化了。现在这两个类，Contents 和 Destination 不是 static，没有 static 关键字，也没有 private 和 public，从访问属性上来说它是 frendly。它不是 static 意味着你没有直接的这个类存在，是要到制造出 Parcel1 对象之后这两个类才存在。它本身就不是静态的，不会被静态的装载，所以不能在里面用静态的东西，它本身不可能是静态的。为什么 Parcel1 为什么可以有 static 的初始化？因为它可以是静态的。而 Contents 和 Destination 一定是动态的，不可能有 static 在里头。至少刚才的编译告诉我们意见事情，他的 static 和 非 static 是有区别的。因为它不是 static，也就意味着你不可能在这个类的外部去使用它，你只能通过这个类的对象去使用它。而实际上你又不可能通过对象，因为它的对象没有给出任何的手段去使用它。所以，这个 inner class 是在外部类的内部的。只能在 Parcel1 的内部才能使用它。这两个 inner class 没有办法从外面去使用它。  

```java
//: Parcel3.java
// Returning a handle to an inner class

abstract class Contents {
  abstract public int value();
}

interface Destination {
  String readLabel();
}

public class Parcel3 {
  private class PContents extends Contents {
    private int i = 11;
    public int value() { return i; }
  }

  protected class PDestination implements Destination {
    private String label;
    private PDestination(String whereTo) {
      label = whereTo;
    }
    public String readLabel() { return label; }
  }

  public Destination dest(String s) {
    return new PDestination(s);
  }

  public Contents cont() {
    return new PContents();
  }
}

```
这个例子是我们更为常见的怎么去使用内部类的例子。它的做法是说我有一个抽象的类 Contents 定义在外面，它定义了一个函数叫 value()。有一个接口叫 Destination 定义在外面，这两个是对外面的。然后，在 Parcel3 里面我们定义了两个内部类，这两个内部类，一个是继承了外面那个公开的类，一个是实现了外面公开的接口。然后我们有两个函数，一个叫 dest，返回一个 Destination，你仔细看它返回的是 Destination，而不是里面的那个 PDestination。所以有一天你做了一个 Parcel3 的对象，你得到了一个 Parcel3 的对象，你调用它的 dest 函数，你就会得到一个 Destination 的对象。你知道 Destination 对象有 readLabel，你就可以去调用它的 readLabel。你不需要知道实际上它不是 Destination，而是 PDestination。这是内部类最初的用处。**我在内部去实现一个外部公开的接口，这个内部的实现对你是隐藏的**。凭什么叫隐藏，什么叫隐藏？你会说我们从来也不知道内部怎么实现的呀。比如说我们去用 String 类的函数，一般情况下也不会去看 String 类的源码，虽然源码是开放的。我正常使用的时候，我不会去看 String 的源码对不对，那个也是隐藏的。为什么这个也是隐藏的？因为你不可能去直接制造 PDestination 的对象出来。你想这是两件事情，所以你可以拿到 PDestination 这个类的对象，所以其实 PDestination 那个类的 class 类的对象是在你的运行时内存里面的。你记得我们说过每个类被装载进来以后，它会有一个 class 的对象来代表那个装载的类，我们以后会在 ittr 时在看待这件事情，我们已经讲过很多遍了，但是我一直不给你们看，到 ittr 在来看，所以 PDestination 这个对象要在你的运行时候能被你用到，一定会有一个 PDestination 的 class 对象在你的内存里面，但是你虽然有那个类的描述，有那个类的定义，但是你不能用它来制造你的对象。只有在那个内部类的外部类里头可以去制造它的对象。一切都是很绕口的。  

```java
//: Parcel4.java
// Nesting a class within a method

public class Parcel4 {
  public Destination dest(String s) {
    class PDestination implements Destination {
      private String label;
      private PDestination(String whereTo) {
        label = whereTo;
      }
      public String readLabel() { return label; }
    }
    return new PDestination(s);
  }
  public static void main(String[] args) {

  }
}

```
这个例子是这样的，我们有一个函数 dest 会返回 Destination 对象。在这个函数里面我们看到了一个类的定义，最后我们制造了这个类的对象走了。这个类的定义可以出现在一个函数的内部，它编译以后也会有一个 Parcel4$xxx 的名字，但是编译的结果如下图：
![innerClass3](image/part2/innerClass3.png)  
仔细看就会发现，中间有个1。因为你把它放在一个更小的 scope 里面，不是类的成员了。Destination 不是 PDestination，不是类的成员。和刚才那两个的例子不一样，它是一个函数里面的东西，我们知道在函数里面你放的所有的东西，除非你加 static，否则它都是 local 的，都是 outto的。也就是说你进这个函数的时候它才有，离开这个函数它就不存在了。就像本地变量一样，离开了以后就没了。所以它也遵循这些法则，进来以后才有，出来以后就没有了。为什么要加上1，是因为你完全可以有重名的，你在这个类的很多地方都可以有 PDestination 的类，当然和变量的法则是一样的，一个函数里面只能有一个。不同的函数里面可以有同名的变量。它也一样在不同的函数里面它也可以有不同的 PDestination。所以出现这样的情况，1,2，3...就是用来做区分的。它会给你加上一个序号。  

```java
//: Parcel5.java
// Nesting a class within a scope

public class Parcel5 {
  private void internalTracking(boolean b) {
    if(b) {
      class TrackingSlip {
        private String id;
        TrackingSlip(String s) {
          id = s;
        }
        String getSlip() { return id; }
      }
      TrackingSlip ts = new TrackingSlip("slip");
      String s = ts.getSlip();
    }
    // can't use it here! Out of scope:
  }
}
```
这是一个函数 internalTracking，里面有 if 语句，条件满足的时候，我们来定义一个类，但其实更准确的是当条件满足的时候，这个类被装载。如果你要问我什么时候它被卸载，可能有的 JVM 不一样，但我知道的是它会在一个情况下被卸载，就是这个类没有任何对象存在了。所以你可以把它想象成，但是我必须说你把它想象成，不是完全 exactly 这个样子。我们每个类被装载进来以后就会有一个 class 对象去描述它，所以你可以把它想象成就是有那么一个对象，它也是对象，所以既然是对象它也和别的对象一样遵循那个垃圾回收机制的法则。然后这个类的每一个对象都会有一个个指针指着那个类，我们讲ittr 的时候会讲那个指针。每个类里面都有一个静态成员变量，那个静态成员变量就叫做 class。那个成员变量就指向他自己的那个 class 类的对象的。当然这里面 JVM 给你转了一道，它不一定完全是那个东西。然后你就可以把它想象成说，当这个类的所有的对象都不存在，都被垃圾回收机制收集掉以后，这个类的那个class 类对象就没有任何指针指着了，于是它就和普通的对象一样成为垃圾，于是它就被卸载掉。所以即使我们定义在这个地方，如果是本地变量的话，我们知道离开了这个 scope，这个本地变量就不存在了。但是对于这个类来说离开了这个 scope，这个类其实仍然是存在于你的内存里头，但是同样的原则，你不能再用那个类了，因为它不在它的 scope 里头了。所以 TrackingSlip 在这个大括号里可以有，但出了这个 if 后面的大括号，在这里 can't use it here! Out of scope。在这里就不能用了。这就是我前面讲的正交的意思。你不能把它当成一种特殊的东西来看，他出现在这里，他就要遵循在这里出现过的其他东西的法则，他出现在函数内部，它就要遵循本地变量的法则。这就叫做正交。

####  4.3.2 匿名类
```java
//: Parcel6.java
// A method that return an anonymous inner class

public class Parcel6 {
  public Contents cont() {
    return new Contents() {
      private int i = 11;
      public int value() { return i; }
    };  // Semicolon reauired in this case
  }
  public static void main(String[] args) {
    Parcel6 p = new Parcel6();
    Contents c = p.count();
  }
}
```
cont() 函数要返回一个 Contents 的对象，然后你看他 return new Contents()，如果在这句括号后有一个分号，一切都很正常。但是在这里不是，在其后面有一个大括号，并且后面还有分号，分号是谁的？是 return 语句的分号，不能省略。这里的大括号表示要在这制造出一个新的类出来，然后这个类去 new 它的对象，这个类是 Contents 的子类或者实现了 Contents 接口的类。取决于 Contents 是什么，Contents 是类的话就继承 Contents 的接口去实现。这个类里面有成员，有函数，这是一个 **匿名类**，他没有名字，对于外界来说它就认为这是一个 Contents 的对象，他不在乎到底是什么类，那个类的名字是什么。Contents 的对象会做 Contents 规定的动作，于是让它做那些动作就可以。这个才是 java 费力气要引入内部类的真正原因，它要实现匿名类。因为在 JDK 1.2 以后，在 Swing 的消息机制里面你会发现有时不得不做很多小的类出来，而那些类很难起名字。与其很难起名字不如不要起名字，要不你起的名字要么是 my1,my2,my3... 这样的名字，还不如不起。我给你提供机制你可以不起名字，起名字是很难的事情。当起错名字，写代码会越来越不舒服。这个东西编译会生成什么？会生成 Parcel6$1.class。反正是匿名，就用数字编号。  

```Java
// An anonymous inner class that calls the base-class constructor

public class Parcel7 {
  public wrapping wrap(int x) {
    // base constructor call:
    return new Wrapping(x) {
      public int value() {
        return super.value() * 47;
      }
    };
  }

  public static void main(String[] args) {
    Parcel7 p = new Parcel7();
    Wrapping w = p.wrap(10);
  }
}
```
这是如何向匿名类传递参数，向它的父类传递参数，它的 Wrapping 类的父类是要有参数的，我们把 x 写到这里，就可以把参数传递给它的父类。  

```java
//: Parcel8.java
// An anonymous inner class that performs initialization. A briefer version of Parcel5.java.

public class Parcel8 {
  // Argument must be final to use inside anonymous inner class:
  public Destination dest(final String dest) {
    return new Destination() {
      private String label = dest;
      public String readLabel() { return label; }
    };
  }
  public static void main(String[] args) {
    Parcel8 p = new Parcel8();
    Destination d = p.dest("Tanzania");
  }
}
```
在这里我们看到的是，我们在这个内部类实现了 Destination 接口的内部类里面用到了 dest，而 dest 就是它外面那个函数的参数。因为你的内部类既然在这个函数的里头，那么你的类里面的函数和变量的初始化是可以自由的去使用它外面的那些东西的，外面的那些东西包括函数里面的本地变量，包括这个函数所在的那个类的成员变量都是它可以自由使用的，因为如果不是这样的，你在这个函数中本来就是可以自由使用的东西，所以作为你这个函数里面的也可以自由使用的东西。但是现实条件是，这个本地变量，因为参数也是本地变量的一种，它们的内存是一样的，所以本地变量或参数必须是 fianl。本来这个 final 没有任何意义，因为 final 只是说明 dest 变量不能指向另一个 String 对象了，没有任何意义，并不保护 String 本身，但是这是对于内部类的要求。内部类要能访问外部类的本地变量必须是 final。  

```java
//: Parcel9.java
// Using "instance initialization" to perform construction on an anonymous inner class

public class Parcel9 {
  public Destination dest(final String dest, final float price) {
    return new Destination() {
      private int cost;
      // Instance initialization for each object:
      {
        cost = Math.round(price);
        if(cost > 100)
          System.out.println("Over budget!");
      }
      private String label = dest;
      public String readLabel() { return label; }
    };
  }
}
```
这是一个匿名类。类 Destination 中的大括号里面是什么？这是定义初始化块，它会在这个类的构造函数初始化之前被执行，而匿名类是没法写出构造函数出来的，因为他没有名字，构造函数一定要有一个和类相同的名字。所以这个东西就起到它的构造函数的作用，而且这个东西是和匿名类一起进入到 java 的，之前没有。

####  4.3.3 外部类关系
```Java
//: Sequence.java
// Holds a sequence of Objects

interface Selector {
  boolean end();
  Object current();
  void next();
}

public class Sequence {
  private Object[] o;
  private int next = 0;
  public Sequence(int size) {
    o = new Object[size];
  }
  public void add(Object x) {
    if(next < o.length) {
      o[next] = x;
      ++ next;
    }
  }
  private class SSelector implements Selector {
    int i = 0;
    public boolean end() {
      return i == o.length;
    }
    public Object current() {
      return o[i];
    }
    public void next() {
      if(i < o.length)
        ++i;
    }
  }
}
```
这个例子里面我们有一个类叫 Sequence，它有一个 private 的数组 o，它有一个内部类 SSelector，注意这个内部类是 private，意味着外面根本不可能接触到这个类。然后在这个内部类里头我们看到它可以自由的使用外部类的成员变量 o。所以这就是内部类存在的意义，它是外部类的一个有机成员，它可以作为成员享受外部类的所有的福利，可以使用外部类的所有的东西。Java 的内部类要做的就是自如的内部类去访问外部类的东西。

```Java
//: BigEgg.java
// An inner class cannot be overriden like a method

class Egg {
  protected class Yolk {
    public Yolk() {
      System.out.println("Egg.Yolk()");
    }
  }
  private Yolk y;
  pbulic Egg() {
    System.out.println("New egg()");
    y = new Yolk();
  }
}

public class BigEgg extends Egg {
  Public class Yolk {
    Public Yolk() {
      System.out.println(“BigEgg.Yokl()”);
    }
  }
  Public static void main(String[] args) {

  }
}
```
我们在 Egg 类里面有一个 protected 的内部类叫 Yolk，在它的子类 BigEgg 里面我们又做了一个 class Yolk。也就是说在父类和子类里面都有相同名字的内部类，这两个内部类有没有关系。这就要牵着内部类到底怎么去理解。如果排除掉内部类，在之前我们知道的，成员变量和成员函数它们的表现是不一样的，成员函数它们构成了 override 的关系，子类会覆盖掉父类；而对于成员变量来说，它们没有关系，子类的成员变量和父类的成员变量，如果重名的话，它们是独立存在的。在子类里面只能是子类的成员变量，在父类里面只能是父类的成员变量。所以变量和函数是不一样的。对于成员类呢？它是更像变量还是更像函数。我们会感觉到说这是一个东西，函数时一段代码，是要顺序执行的代码，而变量是东西，而成员类呢？我们觉得他的属性更像是东西，所以在这件事情上它的表现和成员变量是一样的。在这两个类里面同名的内部类之间它们没有任何关系。当然你可以让你的子类的内部类也继承父类的内部类，super.Yolk 是他的父类的内部类，当然要改一改名字，不能也叫 Yolk，这是有可能的。但是普通的这样写，它们俩是没有关系的。


###  4.4 枚举类
####  4.4.1 枚举类
##### Enums
* enum Season {WINTER, SPRING, SUMMER, FALL}
* Sample: Deal.java
Java 很有趣的东西叫枚举。枚举在 C 和 C++ 都有，都很简单。形式就是 enum 然后是一堆大写的名字（可以使用小写，通常使用大写）这些名字会等于一个整数值，在枚举的定义里面还可以改某个值，这是在C和C++ 常用的东西。但是在 java 呢？这个枚举变得复杂，事实上一开始会让人看不懂。  

当然如果你不想怎么样的话，Java 的枚举也可以被当做 C 和 C++ 那样的枚举来用。比如上面的例子，Season 里面有四个季节，你可以把它当做那个来用，实际上它能做更多。  

```java
import java.util.*;

public class Card {
    public enum Rank { DEUCE, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE, TEN, JACK, QUEEN, KING, ACE }

    public enum Suit { CLUBS, DIAMONDS, HEARTS, SPADES }

    private final Rank rank;
    private final Suit suit;
    private Card(Rank rank, Suit suit) {
        this.rank = rank;
        this.suit = suit;
    }
    public Rank rank() { return rank; }
    public Suit suit() { return suit; }
    public String toString() { return rank + " of " + suit; }

    private static final List<Card> protoDeck = new ArrayList<Card>();

    // Initialize prototype deck
    static {
        for (Suit suit : Suit.values())
            for (Rank rank : Rank.values())
                protoDeck.add(new Card(rank, suit));
    }

    public static ArrayList<Card> newDeck() {
        return new ArrayList<Card>(protoDeck);  // Return copy of prototype deck
    }
}

public class Deal {
    public static void main(String args[]) {
        int numHands = Integer.parseInt(args[0]);
        int cardsPerHand = Integer.parseInt(args[1]);
        List<Card> deck = Card.newDeck();
        Collections.shuffle(deck);
        for(int i=0; i<numHands; i++)
            System.out.println(deal(deck, cardsPerHand));
    }

    public static ArrayList<Card> deal(List<Card> deck, int n) {
        int deckSize = deck.size();
        List<Card> handView = deck.subList(deckSize-n, deckSize);
        ArrayList<Card> hand = new ArrayList<Card>(handView);
        handView.clear();
        return hand;
    }
}
```
结果如下图：
![num](image/part2/num.png)

我们能做更多，我们做了两个枚举，一个 Rank, 一个 Suit。Rank 表示扑克牌的点数。我们定义了枚举类型以后做了两个变量，一个是 Rank 的变量，一个是 Suit 的变量。
我们有一个函数 Card，它会让这张牌的 rank 等于 rank，suit 等于 suit。然后我们会返回一个 Rank，一个 Suit。有一件事要知道的是在 Java 中枚举的名字不在是整数，
它和整数之间不能直接去赋值。C 和 C++ 是可以直接赋值的，Java 不能，它就是一个新的类型。枚举量就是一个类型。我们在这里做了一个 list of Card，list 是等会要讲的。
我们做了foreach 循环。等会会讲这些事情。然后，我们在这里还是基本上把它当做一个普通的变量来用。你说我要 list of card，然后就可以往里面放一些 card对象进去，放一些枚举的
量进去，等等。如果这么看我们的枚举和 C/C++ 差别不大，唯一的区别就是在 Java 中不能把枚举当成整数来看。来看比较疯狂的例子。  

##### Enum with operations
* Example: Planet.java  
结果如下：  
![num2](image/part2/num2.png)  

```java
public enum Planet {
    MERCURY (3.303e+23, 2.4397e6),
    VENUS      (4.869e+24, 6.0518e6),
    EARTH       (5.976e+24, 6.37814e6),
    MARS        (6.421e+23, 3.3972e6),
    JUPITER     (1.9e+27,     7.1492e7),
    SATURN     (5.688e+26, 6.0268e7),
    URANUS    (8.686e+25,  2.5559e7),
    NEPTUNE   (1.024e+26,  2.4746e7),
    PLUTO        (1.27e+22,    1.137e6),

    private final double mass;  // in kilograms
    private final double radius;  // in meters
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }
    public double mass()  { return mass; }
    public double radius() { return radius; }

    // universal gravitational constant (m3 kg-1 s-2)
    public static final double G = 6.67300E-11;

    public double surfaceGravity() {
        return G * mass / (radius * radius);
    }
    public double surfaceWeight(double otherMass) {
        return otherMass * surfaceGravity();
    }
    public static void main(String[] args) {
        double earthWeight = Double.parseDouble(args[0]);
        double mass earthWeight/EARTH.surfaceGravity();
        for(Planet p : Planet.values())
            System.out.printf("Your weight on %s is %f%n", p, p.surfaceWeight(mass));
    }
}
```

我们有一个枚举叫做 Planet，进了大括号以后出现 MERCURY 什么什么，如果没有后面的圆括号我们能理解的，我们定义了一个名字叫 MERCURY，所以火星，VENUS 金星；
EARTH 地球等等一系列的星球，可是后面有圆括号，圆括号什么意思。如果一下看不懂，可以先看 Planet(double mass, double radius) 这一行。这个枚举有一个构造函数，如果
一个东西有构造函数说明它是类。我们前面看到过类有构造函数，interface 还不能有构造函数，因为 interface 是纯虚的。枚举可以有构造函数，它的构造函数那两个值 mass 质量，radius 半径 然后
赋给她的成员变量。枚举类有两个成员变量，一个 mass 一个 radius，它还有两个成员函数，还是 public 类型，可以返回它的 mass 和 radius。这是做的非常好的封装例子。我们有私有的成员变量，
公有的成员函数得到它，但是没有任何的函数去 set 它，对不对？还有一件事情，**在 Java 里面 mass，成员函数和成员变量可以同名**。C 不可以，C++ 不可以，因为对于 C++ 来说函数和成员变量
它们的名字在同一个空间里面，在 Java 中它们处在不同的空间里面，所以它们可以同名。如果 C++ 我们就要写 get_mass, get_radius。对于 java 来说，也流行写成 get_mass，get_radius，因为这会使
它成为 java bean。成为一个豆子。它还有一个 public static final 的常量，还有一个函数做计算。所以写在最前面的这些事 Planet 的量。这样去理解，Planet 是枚举类，这个枚举类可以有成员变量，
可以有构造函数，可以有成员函数，我们可以去定义这个枚举类的一些静态对象，作为枚举类，你可以把枚举类的静态对象写到这个类的定义里面。这些类的静态对象可以通过调用构造函数去构造出来。
所以原口号里面的那两个数是调用构造函数用的，用来调用构造函数，把这个对象构造出来。  

然后 main 函数是这样去用它的。这里有遇到了我们没见过的事情，我们之前一直在说 String[] args，这是 String 类的数组，这是命令行参数。命令行参数的第 0 项是那个命令本身。对于 java 来说没这回事了，
根本不在乎这件事情，所以 Java 的命令行参数第 0 项就是 0 ，输入的第一个参数。所以，它拿你第一个输入的参数。Double 是系统内部里面的类，我们见过 Integer，每一个基本类型，integer, float，double
char 都有对应的第一个字母大写的类型。这种类型叫做 wrap type(包裹类型)，它用来在类的系统里面，对象的系统里面来代表一个 printf data，printf 的一个值。Double是那个。Double 这个类有一个静态的
parseDouble，它会扫描识别字符串中的 double，产生出一个 double 来。所以我们用这种方法得到了一个你输入的 Double，这是你在地球上的重量。然后用这个重量去除以 EARTH.surfaceGravity()，意味 main
函数在这个类里面，所以可以直接用 EARTH。如果在外面，我们要用 Planet.EARTH 来表明这个枚举量。然后我们做了一个 foreach 循环。这是一个 for 循环，但是这个循环没有分号。我们说这不是数组，是枚举类型，
枚举的类型.values()。所以你想枚举的类型，如果 Planet 是一个对象的话，它应该是什么类？Planet 是 Class 的一个对象，values() 是它的一个静态函数，但是我们没有在我们写的代码中看到 values()，它应该是
继承了某个东西，作为 enum 它应该默认继承了什么东西，那个东西会有一个 values()，那个 values() 能给出枚举类型中所有的值，也就是前面写的 MERCURY~PLUTO。这些东西是静态的，因为可以写 Planet.EARTH。
这个东西给出了一个集合，集合里面有 Planet 的所有量。对于这个集合里面 Planet 中的任何一个 p，如果写成这个样子，那么是 Planet 的对象。人们在批评 Java 的 enum 的地方，确实 enum 给懂它的程序员带来便利，
为了代码的可扩展型，常常需要 enum。对于for each循环来说，这个 Planet 的 values() 的所有的类，这个类里面所有的值，每一个拿出来做 Planet 的对象，然后让这个 p 去 surfaceWeight(mass)，去算一下这个质量。
你的体重除以地球表面的重力就是你的质量。然后你的质量在别的星球上面会有多大的重力。Java 在 1.5 以后有 printf，和 C 的 printf 完全一样。但没有 scanf。printf 里面有 %s，这里需要一个 String，而给它的是 p。因为
Object 里面有 toString()，因此所有的 Java 类都有一个 toString()，如果不定义它，它会打印出你的十六进制地址。对于这个 p 来说，它是 Planet 的对象，它会给出你在前面的名字，例如 MERCURY等。你想要它的名字，拿过来用就好了，
它会 toString。但是在某些场合需要直接去写 p.toString() 这些事情。所以枚举可以做这些事情。  

```java
public enum Operation {
    PLUS     { double eval(double x, double y) { return x + y; } },
    MINUS  { double eval(double x, double y) { return x - y; } },
    TIMES   { double eval(double x, double y) { return x * y; } },
    DIVIDE  { double eval(double x, double y) { return x / y; } };

    // Do arithmetic op represented by this constant
    abstract double eval(double x, double y);

    public static void main(String args[]) {
        double x = Double.parseDouble(args[0]);
        double y = Double.parseDouble(args[1]);
        for (Operation op : Operation.values())
            System.out.printf("%f %s %f = %f%n", x, op, y, op.eval(x, y));
    }
}
```
我们定义了一个枚举叫 Operation，它里面有四个量 PLUS, MINUS, TIMES, DIVIDE。到底这个量是什么？它定义了一个抽象的函数叫 eval 用做计算，给两个 double 计算结果。我们前面的例子，每个量是圆括号，现在每个量后面是大括号。大括号意味着匿名类。
我们写匿名类的时候是这样写的，一个什么什么类的名字，圆括号，后面一个大括号，于是就是匿名类了。只要在 new 的时候后面加上这个东西就是匿名类了。所以现在在这个名字的后面加上这个东西于是他成了匿名类。这个类继承了 Operation 类，所以它可以
override 那个 eval 函数。每个子类有它自己的 eval 函数。我们可以读入两个 double  值，对应于它的每一个 Operation，那个 op 拿出来做它的 op.eval(x,y)。它的每一个量还可以有自己的函数。批评他的人批评的是什么呢？就是你实现的太丰富了，你让别人很难理解
这个量到底是什么，不是整数，ok我们能接受，你可能是一个强制类型的东西，你不愿把一个整数值拿出来。你可以是它的一个对象，你甚至可以是它的一个匿名类的对象，匿名类子类的对象。个人还是倾向说他是对象，但是你在构造这个对象的同事还可以构造它的匿名子类。喜欢它的人
说它非常灵活，不喜欢他的人说会让初学者真的看不懂。



























endOfPart24
