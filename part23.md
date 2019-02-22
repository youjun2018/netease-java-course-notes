##  第三章 继承与多态
###  3.1 继承
####  3.1.1 媒体资料库的例子
创建CD类，使用容器保存这些 CD 类。  
<img src="http://yuml.me/diagram/nofunky/class/[CD|title;artist;numofTracks;playingtime;gotit;comment]" >  
也应该有一个表示资料库的类，这个类中有容器，用来放这些 CD 类。

```java
package demo;

public class CD {
	private String title;
	private String artist;
	private int numofTracks;
	private int playingTime;
	private boolean gotIt = false;
	private String comment;

	public CD(String title, String artist, int numofTracks, int playingTime, String comment) {
//		super();
		this.title = title;
		this.artist = artist;
		this.numofTracks = numofTracks;
		this.playingTime = playingTime;
		this.comment = comment;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub

	}

	public void print() {
		System.out.println(title+":"+artist);

	}

}
```

```java
package demo;

public class DVD {
	private String title;
	private String director;
	private int playingTime;
	private boolean gotIt = false;
	private String comment;

	public DVD(String title, String director, int playingTime, String comment) {
		super();
		this.title = title;
		this.director = director;
		this.playingTime = playingTime;
		this.comment = comment;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub

	}

	public void print() {
		System.out.println("DVD"+title+":"+director);

	}

}
```

```java
package demo;

import java.util.ArrayList;

public class Database {
	private ArrayList<CD> listCD = new ArrayList<CD>();

	public void add(CD cd)
	{
		listCD.add(cd);
	}

	public void list()
	{
		for(CD cd : listCD)
		{
			cd.print();
		}
	}

	public static void main(String[] args) {
		Database db = new Database();
		db.add(new CD("abc", "abc", 4, 60,"..."));
		db.add(new CD("def", "def", 4, 60,"..."));
		db.list();


	}

}
```

CD 类中成员变量如何初始化？  
在成员变量都做好以后，在 Ecplise 里面选择 Source --> Generate Constructor using Fields... --> 然后在弹出的窗口中勾选需要创建的字段（这里gotIt不选，直接默认就好）  
![autoGenerator](image/part2/autoGenerator.png)  
在 Insertion point 选项中可以选择插入的位置。  
这样，Ecplise 帮组创建一个构造函数，这个构造函数有很多参数，帮我我们把成员变量都初始话好了。创建的构造函数中，有函数 super()，在这个构造函数中，super()函数可以没有，以后再说。

####  3.1.2 继承
上述代码有一个问题，CD类和DVD类有很多相似的地方，在 DataBase 类中，对两个类的操作也有很多相似的地方。**出现了大量的代码复制。** 是代码质量不良的一种表现。  

从 CD 或者 DVD 中提取一些公共的东西，这个公共的东西可以表达 CD 或者 DVD，然后让 DataBase 管这个公共的东西而不是 CD 或者是 DVD。  

在原来的代码中新建 Item 类（不加main函数），让 CD 继承 Item和 DVD 继承 Item(public class CD extends Item)。然后添加代码。如下：  

```java
package demo;

import java.util.ArrayList;

public class Database {
//	private ArrayList<CD> listCD = new ArrayList<CD>();
//	private ArrayList<DVD> listDVD = new ArrayList<DVD>();
	private ArrayList<Item> listItem = new ArrayList<Item>();

//	public void add(CD cd)
//	{
//		listCD.add(cd);
//	}
//
//	public void add(DVD dvd)
//	{
//		listDVD.add(dvd);
//	}

	public void add(Item item)
	{
		listItem.add(item);
	}

//	public void list()
//	{
//		for(CD cd : listCD)
//		{
//			cd.print();
//		}
//		for(DVD dvd: listDVD)
//		{
//			dvd.print();
//		}
//	}
	public void list()
	{
		for(Item item : listItem)
		{
			item.print();
		}
	}
	public static void main(String[] args) {
		Database db = new Database();
		db.add(new CD("abc", "abc", 4, 60,"..."));
		db.add(new CD("def", "def", 4, 60,"..."));
		db.add(new DVD("xxx", "aaa", 60,"..."));
		db.list();		
	}
}

```
```java
package demo;

public class Item {
	public void print() {
		System.out.println("Item");
	}
}
```
```java
package demo;

public class CD extends Item{
	private String title;
	private String artist;
	private int numofTracks;
	private int playingTime;
	private boolean gotIt = false;
	private String comment;

	public CD(String title, String artist, int numofTracks, int playingTime, String comment) {
//		super();
		this.title = title;
		this.artist = artist;
		this.numofTracks = numofTracks;
		this.playingTime = playingTime;
		this.comment = comment;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
	}

	public void print() {
		System.out.println("CD"+title+":"+artist);
	}
}

```
```java
package demo;

public class DVD extends Item{
	private String title;
	private String director;
	private int playingTime;
	private boolean gotIt = false;
	private String comment;

	public DVD(String title, String director, int playingTime, String comment) {
		super();
		this.title = title;
		this.director = director;
		this.playingTime = playingTime;
		this.comment = comment;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
	}

	public void print() {
		System.out.println("DVD"+title+":"+director);
	}

}

```



我们做了一个新的类叫 Item。这个类中只定义了一个空的 print()，在 CD 类中增加 extends Item，即扩展了 Item，这个 CD 就是 Item 的子类。这就叫继承。我有了 Item 类了，然后我说 CD 是 Item 的一个子类。同样，DVD 也是 Item 的子类。DataBase/CD/DVD/Item类的关系是什么样的呢？  

Item 派生了两个子类 CD 和 DVD。以前 Database 管 CD 和 DVD，现在只认识 Item 的类。Database 里面有 ArrayList，ArrayList 里面放 Item。Database没有直接管 CD 或 DVD，它直接管 Item，里面有放 Item 的容器，让后它的 list 函数遍历 Item，他的 add 函数会把东西往 Item 中加。  

当 CD 是 Item 的子类后，我们在 Database 类中能做一件事情，当我们在 add 一件东西的时候，Database 的 add 函数说它要的是 Item，但我们给他的是刚刚 new 出来的 CD，没任何问题，它能接收的。为什么能接收？为什么 new 出来的 CD 能当 Item 呢？刚才我们说，CD 是 Item 的子类，光这么说台太牵强，还不够。对于 Database 来说，他对 Item 的全部认识是什么？它对 Item 的认识是说，他应该有一个 print 函数，因为这是在 Database 中唯一用到的 Item 的地方。在 Database 中，我们会把一个 Item 东西 add 进去，但在这个过程中我们不会去用这个 Item，他说自己是 Item 就可以了。但是在 list 函数中，它会让 item 去做 print 这个事情，那个 item 必须要具有 print 函数才行。然后在 Item 类中要有一个 print 函数。因此它就有 print 函数。在 CD 类中，它也是有 print 函数，所以 Item 的 print 和 CD 的 print 构成这样一个关系，对于 Database 要 print 的时候，只要你这个 item 是有 print 的，我就认为你是一个 item，至于具体你是那个 item，我不关系，因为我要的是只要你有那个 print 就可以了。  

回过来说，假如 CD 没有 print，把 CD 的 print 注释掉后，我们没有看到任何地方有红叉叉，为什么？因为 Item 中有 print，不妨让 Item 做些事情，如下：
```java
package demo;

public class Item {

	public void print() {
		System.out.println("Item");

	}

}
```
结果如下：
```
Item
Item
DVDxxx:aaa
```
然后运行 Database，原本显示 CD 的地方现在是 Item。这发生了什么？我们的 CD 从 Item 得到继承了，它继承得到了什么？你要说你家祖宗留下来什么，一座老宅子，大家看得见摸得着，这是我们家的遗产。现在 CD 从 Item 得到继承了，它 通过 extends Item 来表明继承的关系，它得到什么了呢？所有 Item 的东西他都得到了，包括 Item 中的 print 函数。即使 CD 没有 print 函数，那它也有 Item 的 print 函数。就是说在父类中定义了一个函数后，子类就天然得到了这个函数。继承就是父类有什么他就得到什么，父类所有的东西在子类中都是存在的，在子类中都是可能可以用的，说可能是因为还涉及到访问权限的问题。继承从语法上来说就是某个类宣称 extends 某个类了，它就从那个父类得到继承了，他会继承父类的所有的东西，然后它还可以增加新的东西，当然这个程序不是完美的，还需要做些东西。


###  3.2 子类父类关系
####  3.2.1 子类父类关系Ⅰ
我们用继承把原先代码进行改造，从 Database 角度看还不错，Database 只有一个容器，只有一个add 函数，list 里面只有一个循环。但是我们看 CD 和 DVD，里面仍然有 title, playingTime等。还存在一些代码复制的情况。我们要把所有相同的东西都去掉，怎么做呢？在子类 CD 和 DVD 类中相同的东西提取出来放到它们的父类中去。  

虽然子类继承父类，但是父类中 private 的东西子类不能直接拿来用。解决方法一，就是把父类中的 private 修饰符改为 protected 修饰。  

**protected 意思是说自己可以访问，同一个包里的其他类可以访问，子类可以访问。**  

在我们这个代码中，子类和父类在同一个包里面，protect 没问题。但是现实中，父类和子类往往不在同一个包中，一般父类在别人的包里，子类是在自己的包里面，子类父类在不同的包里面。所以 protected 可以让子类访问父类中标示为 protected 的成员，又能保证和它们没关系的那些类不能访问标示 protected 的成员。  

方法二，现在的问题是是不是要在 CD 里面用这个 title，在 CD 中用到 titel 的地方只有一个，就是在构造里面要对这个 title 做赋值。可是既然 title 是 item 的，不是应该让 Item 做初始化吗？所以本来应该做的事情是，为 Item 做一个构造器，它会去做 title 的初始化，然后在 CD 的构造器中的第一句话把 title 传过去（即在构造其中使用 super(title)），现在就正常了。  

现在又出现了很多新东西，我们为 Item 创造了一个构造器，这个构造器使用 String 来对 title 进行初始化。既然 title 是 Item，就应该由 Item 对其进行初始化，不应该由它的子类来做。在 Item 的子类里面呢，我们实际去构造的时候要给它一个 title。我们要构造 CD 的对象，这个对象有 title 在里面，我们 CD 的构造器要拿到那个 title，完了以后它自己不做对 title 的赋值，使用 super(title) 来调用 Item 的构造器来把 title 传递给它。  

注意子类初始化顺序：  
**CD 构造进来以后，先去做父类的那个构造，或者说父类的初始化，然后才来做自己的定义初始化，然后才进构造函数去做剩下的事情。**  

我们通过在 CD 的构造器的第一行写了一个 super，把 title 的参数传给了 Item，使 title 在 Item 构造器中初始化了 Item 的 title，而这个 title 将来其他地方会用的。  

再看 DVD 类中的问题。刚在在自动生成 DVD 的构造器时，它自动给我们加了 super()，不带任何参数。这句话的意思是它会去调用父类的没有参数的构造器，可是经过刚才的修改，父类 Item 的构造函数是要参数的，出现问题，找不到不要参数的父类的构造器。如果我们把 DVD 构造器中的 super 去掉行不行呢？不行。如果去掉了，错误提示告诉你说它认为 Item 是有一个不带参数的构造器的。也就是 Ecplise 帮我们自动生成的构造其中的 super(); 是没有用的，为什么？假如我们给 Item 增加一个不带参数的构造器，这叫重载，什么也不做。DVD 类就不报错。在 DVD 的 main 函数中增加一些东西，让 DVD 类能跑起来。然后设置断点进行测试。会发现，虽然注释掉了子类 DVD 构造器中的 super，但仍然会跳转到父类无参构造器。我们在 DVD 中并没有写 super(); 这一行，不需要。在构造子类的对象过程当中，它会自动的先去调用父类的那个构造器，如果没有通过 super 给父类传递参数，那么他回去寻找父类中不带参数的构造器；如果给参数了，它会去父类中去寻找带参数的适合的构造器来执行。  

所以我们的原则是，当我们去构造一个子类的对象的时候，它首先要确保它的父类的那些成员变量得到恰当的初始化。恰当的初始化包含两件事情，第一是定义初始化和构造器。我们知道，如果你又有定义初始化又有构造器，定义初始化会先做，然后构造器。如果有子类有父类时，它一定会保证父类的定义初始化和构造器先做，做完之后再回轮到子类的定义初始化和构造器，这样的一个执行顺序是永远存在的。不管你是不是主动的使用 super 去传递参数，去指定调用父类的那个构造器，这个事情是一定会做的。如果没有super，它就会去找父类那个没有参数的构造器，如果有 super，那就会根据 super 去寻找恰当的构造器。

####  3.2.2 子类父类关系Ⅱ
根据上述规则，来把相同的变量放到 Item 类中。  

在修改 DVD 的时候，我们发现一件事情，就是子类 DVD 有自己的 title。我们知道他从 Item 继承的也有 title，这个 title 和 Item 的 title 有什么关系？在子类 DVD 的构造函数中说 this.title = title; 是可以的，为什么？在计算机中有一个基本的准则，就是离我最近的就是我的。  

子类和父类的另一个关系，如果子类中有父类有过的完全相同的名字的成员变量，在子类里面父类的那个变量就会被隐藏起来了。在子类里面我们说的是子类自己的，父类那个看不见了。当时当你回到父类那边去后，对变量进行操作，它用的是谁的呢，是父类自己的。  

总结一下子类和父类的关系。父类的东西都继承给子类，子类都得到。但是当父类的那个东西是 private，子类不能碰，但是可以通过父类的函数去碰。在谁的函数里面，指的成员变量就是谁的。如果子类和父类里出现同名的成员变量后，在子类的函数里面指的成员变量就是子类自己的，在父类的函数里面指的成员变量就是父类自己的。它们之间没有任何联系。  

现在把 DVD 的东西全部搬到父类 Item 中。现在发现 DVD 的 print 出错了，是因为 DVD 的 print 是要打印 title，而 title 现在是父类的 private，子类不知道 title，怎么办？可能谁说，把父类的 title 做成 protected 就好了。但是把父类的成员变量做成 protected 是没办法的办法，尽量不要这样做。解决办法是，Item 不是有 print 吗，那个 print 啥事都没做，能不能让 Item 的 print 去 print title。然后修改 DVD 的 print，让它 print 信息 "DVD" 和 "director"，然后调用父类的那个 print 去 print title，该如何做？如果只写 print(); 这只会调用子类自己的 print。要调用父类的 print，要使用 super.print();。达到最初的效果。

```java
package demo;

import java.util.ArrayList;

public class Database {
//	private ArrayList<CD> listCD = new ArrayList<CD>();
//	private ArrayList<DVD> listDVD = new ArrayList<DVD>();
	private ArrayList<Item> listItem = new ArrayList<Item>();

//	public void add(CD cd)
//	{
//		listCD.add(cd);
//	}
//
//	public void add(DVD dvd)
//	{
//		listDVD.add(dvd);
//	}

	public void add(Item item)
	{
		listItem.add(item);
	}
//	public void list()
//	{
//		for(CD cd : listCD)
//		{
//			cd.print();
//		}
//		for(DVD dvd: listDVD)
//		{
//			dvd.print();
//		}
//	}
	public void list()
	{
		for(Item item : listItem)
		{
			item.print();
		}
	}

	public static void main(String[] args) {
		Database db = new Database();
		db.add(new CD("abc", "abc", 4, 60,"..."));
		db.add(new CD("def", "def", 4, 60,"..."));
		db.add(new DVD("xxx", "aaa", 60,"..."));
		db.list();
	}
}
```
```java
package demo;

public class Item {
	private String title;
	private int playingTime;
	private boolean gotIt = false;
	private String comment;

	public Item(String title, int playingTime, boolean gotIt, String comment) {
		super();
		this.title = title;
		this.playingTime = playingTime;
		this.gotIt = gotIt;
		this.comment = comment;
	}
	public void print() {
		System.out.print(this.title);		
	}
}
```
```java
package demo;

public class CD extends Item{
	private String artist;
	private int numofTracks;

	public CD(String title, String artist, int numofTracks, int playingTime, String comment) {
		super(title,playingTime,false,comment);
		this.artist = artist;
		this.numofTracks = numofTracks;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
	}

	public void print() {
		System.out.print("CD");
		super.print();
		System.out.println(":"+artist);
	}
}
```
```java
package demo;

public class DVD extends Item{
	private String director;

	public DVD(String title, String director, int playingTime, String comment) {
		super(title, playingTime, false, comment);
		this.director = director;
	}
	public void print() {
		System.out.print("DVD");
		super.print();
		System.out.println(":"+director);
	}

	public static void main(String[] args) {
		DVD dvd = new DVD("123","234",4,"...");
		dvd.print();
	}
}
```


###  3.3 多态
####  3.3.1 多态变量
在面向对象的这个世界里面，类 class 它的本意就是类型 type。所以我们定义了一个类出来就是定义了一个新的类型。这个新的类型可以用来定义变量，可以制造这个类的对象来定义变量，当然对象的变量是一个管理者。所以类就是类型，子类呢？当我们用了 extends ，我们说 CD extends Item，表明 CD 是 Item 的一个子类，在这个关系当中，我们可以说 CD 是 Item 的子类，CD 是 Item 的一种子类型。子类和父类的关系也可以表达为子类型和父类型的关系。所以子类的对象可以被当做父类的对象来使用，比如说子类的对象可以赋给父类的变量，子类的对象可以传递给需要父类对象的函数，子类的对象也可以放在用来存放父类对象的容器里面。

##### 子类和子类型
* 类定义了类型
* 子类定义了子类型
* **子类的对象可以被当作父类的对象来使用**
    + 赋值给父类的变量
		+ 传递给需要父类对象的函数
		+ 放进存放父类对象的容器里

例如：
##### 子类型与赋值
子类的对象可以赋值给父类的变量  
<img src="http://yuml.me/diagram/nofunky/class/[Vehicle|]^-[Car|], [Vehicle|]^-[Bicycle|]" >
```java
Vehicle v1 = new Vehicle();
Vehicle v2 = new Car();
Vehicle v3 = new Bicycle();
```
子类对象可以安全的交给父类。  

##### 子类和参数传递
```java
public class DataBase
{
	public void add(Item theItem)
	{
		...
	}
}
DVD dvd = new DVD(...);
CD cd = new CD(...);

database.add(dvd);
database.add(cd);
```
子类的对象可以传递给需要父类对象的函数。  

##### 子类型和容器
![childType](image/part2/childType1.png)
子类的对象可以放在存放父类对象的容器里。

##### 多态变量
在 java 当中，所有的对象变量都是多态的，多态指的是多种形态的变量。这个时候可以放这个类型的变量，过段时候可以放令一种类型的变量。多态变量有两个类型，一种类型叫**声明类型**，就是字面上看的类型，叫静态类型。**动态类型** 指的是当程序运行到这里时，它里面管理的是什么类型的对象那么他的动态类型就是什么。每个 java 的对象变量都具有两种类型，一种是它的声明类型，一种是他的动态类型。有的时候可能一致，有的时候可能不一致。这就是变量的多态，多态变量指的是运行的时候 具体的某一时刻它所管理的那个类型是会变化的，这叫做多态变量。

* Java 的对象变量是多态的，它们能保存不止一种类型的对象
* 它们可以保存的是声明类型的对象，或声明类型的子类的对象
* **当把子类的对象赋给父类的变量的时候，就发生了向上造型**

####  3.3.2 向上造型
造型的意思就是把一个类型的对象赋值给另外一个类型的变量的过程叫造型。

##### 造型 cast
* 子类的对象可以赋值给父类的变量
    + **注意！Java 中不存在对象对对象的赋值！！**
* 父类的对象不能赋值给子类的变量！  
```java
Vechicle v;  
Car c = new Car();  
v = c;  // 可以  
c = v;  编译错误  
```
* 可以用造型：
```java
c = (Car) v;
(只有当 v 这个变量实际管理的是 Car 才行)
```
在 Java 中不是那个对象给那个对象赋值，二是让这两个管理者去管理共同的对象。几乎所有的OOP语言都是这样。但是 c++ 不是这样，c++ 是改造的不够完全的 OOP 语言。**在 C++ 里面可以做两个对象之间的赋值，但 Java 做不到。** 你不可能让一个对象去修改另一个对象的值如果采用赋值运算符，赋值运算符做的事情是让一个变量去指向另外一个对象，去管理另外一个对象。在这个过程中可能发生造型，让静态类型为某个类型的变量，去管理静态类型和动态类型不符的那个对象，这就叫做造型。  

##### 造型
* 用括号围起类型放在值的前面
* 对象本身并没有发生任何变化
    + 所以不是“类型转换”
* 运行时有机制来检查这样的转化是否合理
    + ClassCastException

对于面向对象的语言来说，对于对象系统来说，我们把它叫做造型。类型转换不是造型。类型转化是说经过强制类型转化，原来的值发生改变，不再是原来的值了。造型是造型做完后把你当做另外一个类型来看待，并没有把你改造成另外一个类型。  

cast 叫造型，虽然和类型转化是同一个英文单词。对于 int double 等基本类型是类型转化，对于对象类型来说，叫做造型。  

#####向上造型
* 拿一个子类的对象，当作父类的对象来用
* 向上造像是默认的，不需要运算符
* 向上造型总是安全的

####  3.3.3 多态函数
![question](image/part2/question.png)
在 database 的循环中，每一轮都会拿到一个 item，那个 item 根据我们放进去的对象可能是 CD，也可能是 DVD。这个 item 变量是多态变量，它有两种类型，一种是声明类型，一种是多态类型。它的声明类型永远是 Item，而它的动态类型是这次拿到什么就是什么，可能是 CD，也可能是 DVD。而当我们通过.这个运算符来说，Item 你所管理的那个对象去做 print 动作的时候，它会让它实际所管理的那个对象去做 print 动作。实际管理的是 CD，就做 CD 的 print，实际管理的是 DVD，就做 DVD 的 print。这件事情叫做多态。这件事情的技术基础是什么呢？  

##### 函数调用的绑定
* 当通过对象变量调用函数的时候，调用哪个函数这件事情叫做绑定
    + 静态绑定：根据变量的声明类型来决定
		+ 动态绑定：根据变量的动态类型来决定
* 在成员函数中调用其他成员函数也是通过 this 这个对象变量来调用的

静态邦定就是说，你这个变量声明类型是什么我就调用声明类型中的那个函数。而动态绑定是说，你实际管理的对象是什么，就使用实际对象的那个类型中的函数，因为对于编译器来说，在编译的时候它并不知道 Item 到底管的是那种类型，只有运行时才知道，这就叫动态，所以叫动态绑定。  

对于 OOP 的语言来说，默认所有的绑定都是动态绑定。  

##### 覆盖 override
* 子类和父类中存在名称和参数表完全相同的函数，这一对函数构成覆盖关系
* 通过父类的变量调用存在覆盖关系的函数时，会调用变量当时所管理的对象所属的类的函数

例子：Shape 类  
你是一个 Shape，你就应该会 draw，那么，你就去 draw 吧。这个就叫做多态。  

所谓多态，是指就是通过一个变量去调用一个函数。我们只是写了一句话，并不去判断变量的类型是什么，我们只需要写 shap.draw, item.print，对应的那个函数就会被调用出来。这种事情就叫做多态。

####  3.3.4 DoME的新类型
在我们现在的媒体资料库的基础上，如果有新的媒体加入进来，那会非常容易。因为不需要对 Database 类进行改动，也不需要对 Item 类进行改动，只需要做的是增加一个新的类，这个类继承自 Item。  
1. 新建一个类
![dome1](image/part2/dome1.png)
2. 比方说叫做 VideoGame。他是继承自 Item，那么就可以在弹出框中的 Superclass 填上 Item，然后加上 main 函数，然后 finish。但是如果不创建构造函数会报错。
![dome2](image/part2/dome2.png)
3. 然后 VideoGame 就自动继承 Item。VideoGame 可能有新的成员变量，例如 numberOfPlayers 多少个玩家。我们可以使用 Ecplise 的功能自动构造构造函数。
![dome3](image/part2/dome3.png)
![dome4](image/part2/dome4.png)
4. 上面是一种做法，因为有父类，另外一种做法是构造器是从父类开的。如下，它会处理父类的构造函数。
![dome5](image/part2/dome5.png)
![dome6](image/part2/dome6.png)
5. 于是他给我们创建了一个父类构造器，这个构造器有父类要的参数并通过 super 传递。VideoGame 有自己的成员函数，叫 numberOfPlayers。稍微修改构造函数就可以了。
![dome7](image/part2/dome7.png)
![dome8](image/part2/dome8.png)
6. 由于需要添加 print 函数，所以利用 Ecplise 创建 print 函数。
![dome9](image/part2/dome9.png)
![dome10](image/part2/dome10.png)
![dome11](image/part2/dome11.png)
7. Database 需不需要动呢。里面的 ArrayList 是放 Item 的，VideoGame 是 Item 的子类，可以使用。Database 的 add 函数是 add 一个 Item 的，所以可以 add VideoGame。对于 main 函数，就可以添加 VideoGame 的对象了。Database 的 main 如下：
![dome12](image/part2/dome12.png)  

##### 增加新的媒体类型
![dome13](image/part2/dome13.png)
在现在的 Database 架构体系下，增加一个新的媒体类型是非常容易的，增加新的媒体类型，只需要增加 Item 的子类就行了。对于 Database 来说，add 函数，list item， print 函数都不需要动，这种特性我们叫做**可扩展性**。  

你的代码不需要修改，就可以扩展、去适应新的数据、新的内容，这叫做**可扩展性**。如果您的代码经过修改可以适应新的数据、新的内容，那就**可维护性**。

##### 更深的继承
现在想在 VideoGame 上增加新的类型，如下图。VideoGame 和 BoardGame 有相似的地方，例如都有 numberOfPlayers。这样我们可以在上层新建 Game 类，让 Game 管理 numberOfPlayers，VideoGame 和 BoardGame 继承 Game 类。形成更深的继承关系，更有效的表达媒体类型。
![dome14](image/part2/dome14.png)  


###  3.4 final
####  3.4.1 final 变量
##### final
* final: This cannot be changed
    + final for data
		+ final for methods
		+ final for a class

Java 有关键字 final，可以用在三个地方，可以是成员变量，可以是成员函数，也可以让整个类都是 final。final 在不同的地方有不同的意思，但是有一个基本的意思，就是不能被改变，可以被赋初值,这个初值可以是动态的。某种意义上它和 C++ 的 const 是相似的, 但它不是常数，它是不可变的变量, 它仍然是变量。变量和常数有什么区别？ 常数是编译器变量表中的一个符号，变量是要给它分配内存空间的。  

final 成员变量的例子  
![final1](image/part2/final1.png)
我们可以写 final int i1 = 9; zhe 种东西叫做 compile-time constants，编译时刻就已经知道值，确定值的。static final int I2 = 99; 这有什么区别？说明它放在那里的问题。静态和非静态是说明变量放在那里的问题。什么要有这样的区别？放在每一个对象里面和放在类里面有区别吗？有区别，它是不能改。当然这两个 const 是没有关系，如果你不是const，你是这样 final int i4 = (int)(Math.random()* 20); 这是随机数，会变化的。前面没有 static 意味着每个对象都不一样。static final int i5 = (int)(Math.random()* 20); 意味着每个对象都一样，但是每次装载不一样，这次运行和下次运行不一样。所以我们一种典型的 public static final 它等于一个常数。

![final2](image/part2/final2.png)
即使是对象也可以，它 new 一个 final 对象出来，构建一个对象。final 的对象是什么意思？xian 在我们这样写，什么是 const，是 v2 指向了 Value() 这个事情是 const，还是 v2 所指的那个 Value() 是 const，值是 const 还是指针是 const。对于Java 来说，final 的意思是说 v2 指向 Value() 这件事情是 const，也就是说指针是 const。Java 没有办法使得这个对象是 const，C++ 可以这样做。Java 认为，你的类的设计者再设计类的时候没有让类的对象成为 const，那么你就没有理由在后面把它作为 const。所以 Java 不能做这件事情，把一个对象作为 const，以保护它不被修改。  

![final3](image/part2/final3.png)
对于数组来说也是一样，不是说 a 里面的东西1,2,3… 不能修改了，能改的，但是 a 不能指向别的数组了。你不能让一个数组成为 const，成为 final。  

![final4](image/part2/final4.png)
这一行 final int j; 这一行 j 没有初始化，这是可以的，但是你必须在它的每一个构造函数里面都给值，即你可以有不同的方法给它赋初值，但是你不能不给他初值。如果它在某个构造函数中发现没有给它赋初值，会出错。所以，这叫做 Blank Final。对象的指针也可以做 Blank Final。  

![final5](image/part2/final5.png)
也可以让函数中某个参数是 final，这个 final 表面上看是没有任何意义的，既然它不能保护 g 这个指针所指向的对象，final 的意义何在？final 是说在这个函数中，g 不能指向另外的东西了。写到这里只是为了说明，以后会读到这样的代码。它是有用的，有价值的，当讲到 inner class 的时候会来提这个事情，为什么内部类外面的要被内部类里头访问的本地变量必须是 final。  

####  3.4.2 final 的函数和类
##### Final methods
* two reasons for final methods:
    + To put a "lock" on the method to prevent any inheriting class from changing its meaning.
		+ The compiler is to turn any calls to that method into inline calls.
* private is final.  

函数前面可以加 Final 关键字，如果你加上了关键字，这个 final 是说这个函数在它的子类当中不会被 override。一个函数在子类中不会被 override 意味着不管有多少代的子类，这个函数就是那个不会被改变了。当我们去调用这个函数的时候，就不需要动态绑定了。我们要动态绑定的理由是因为子类有可能有自己的函数，我们要jiao，子类有自己的jiao，所以我们要用动态绑定，因为我们不知道将来在运行的时候，这个指针所指出去的那个对象到底是哪种具体类型。如果这个函数时final，就意味着这个函数、这个指针所指的函数只有一个，不可能有新的版本出来，不需要做动态绑定，只需要静态绑定。所以 Java 是有静态绑定，但这是 final 的东西。另外，除了 final 函数还有一种函数也是 final。我这里有答案 private。private 意味着子类不可以访问，子类不可以访问的函数当然不需要动态绑定。它没有任何条件来修改它，来 override 它。所以 private 的东西也是 final。  

##### Final classes
* you don't want to inherit from this class or allow anyone else to do so.

* Discuss:
    + Final fields in a final class?
		+ Final methods in a final class?

再进一步让整个类都是 Final。整个类是 final 意思是说，这个类不能有子类，断子绝孙的。为什么需要这样子，因为 Java 是个充分多态的系统，在 Java 程序里面我们大量见到的代码都是说我在这个地方需要这个类的对象，让我我拿这个类的对象去做些事情。但是我们很少真的去检查你拿到的所谓的这个类的对象是这个类的对象还是某个子类的对象。比方说，我们需要在这里检查用户名和密码是否匹配，然后我不幸的从网上得到一个可以做这个事情的那个类的对象，但是实际上是那个类的某个子类的对象，它可能就干坏事。因此 final 就起这个作用，使得这个类不可能被别人篡改，不可能它的任何函数有新的版本出来。所以我们去做 final 类，让它里面所有的函数都是 fianl，这是 final 类的意义。另外一层意义是这个函数跑起来会很快，因为静态绑定要比动态绑定来的快，动态绑定要比静态绑定多做很多事情。
