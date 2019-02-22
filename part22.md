##  第二章：对象组合
###  2.1 对象组合
####  2.1.1 对象的识别
例子：写程序模拟一个时钟。  
![clock](image/part2/clock.png)

写程序很多时候是自然当中看到的一些事物的表述，把问题领域在计算机的领域中描述出来，从而去解决它。  
如果不是面向对象，直接一个循环就解决了。面向对象的核心就是在这个地方我们要看到有什么样的东西，每样东西有什么属性，这些东西之间是怎么交互的。如何识别对象，如何划分对象是合理的？  

##### 如何识别对象
一个四位显示器  
![fourShow](image/part2/fourShow.png)  
还是两个二位显示器  
![two](image/part2/twoShow.png)  

划分成两位显示器更合理，因为小时和分钟有很多相似的地方：现在的数值是多少；它们都能做一个动作，去加一；当它加到某一个上限的时候，要回零。设计一个类表式两位计数器，用它表示小时和分钟。  
其中一个类如下  
<img src="http://yuml.me/diagram/nofunky/class/[Display|-value;-limit|+increase();+getValue()]" >  
下面是实现：  
1. 打开Eclipse，选择File --> New --> java project，建立一个叫clock的projece
2. 在clock中新建 class叫Display。这个Display只是整个钟的一个小部件，我们依然可以为它做一个main出来，这非常有用。因为我们做这个Display就希望对这个Display单独的进行测试，这个类就给他一个main。
```java
package clock;

public class Display {
    private int value = 0;
    private int limit = 0;  //最好写上初值

    public Display(int limit)
    {
    	this.limit = limit;
    }

    public void increase()
    {
    	value++;
    	if(value == limit)
    	{
    		value = 0;
    	}
    }

    public int getValue()
    {
    	return value;
    }

	public static void main(String[] args) {
		Display d = new Display(24);
		for(;;)  //按红色按钮强制停止
		{
			d.increase();
			System.out.println(d.getValue());
		}

	}

}

```

####  2.1.2 对象组合
上节我们实现了一个Display，这个Display能从00加到23或者从00加到59。在我们的程序中应该有两个这样的东西，把这两个东西组合在一起组成另外一个对象，叫做Clock。类图如下：  
<img src="http://yuml.me/diagram/nofunky/class/[Clock|-hour;-minute|+increase();+getValue()]" >  
其中，hour 和 minute的类型都是 Display。在一个类中有另外类的对象，对象组合成了新的对象。接下来的事情是这两个类是怎么互动的？就是当 minute 从59变成00时，要通知 hour 加一了。实现这个功能有几种方式：一种方法是在表示 minute 类的里面实现一个代码，它能够调用旁边那个 hour 类的 increase 函数。单如果这样做的话，那么 minute 代码和 hour 代码就不一样了。hour 代码要通知别人，minute 代码不需要通知别人，就不可能是同一个 Display。**我们希望我们类的设计已经对象将来的结构是每个类和每个对象都尽可能的独立**。表达 hour 的类和表达 minute 的类没有直接的联系，我们希望用一个类表达两个对象。因此他们之间的联系只能通过第三方，即他们的老大 Clock 来实现。Clock 凌驾于这两个类之上，它知道 minute 和 hour 的情况，当 minute 翻转为 00 时，它可以通知 hour 加一。  
代码实现：  
1. 在 Clock project 中 New 一个 Clock 类，当然它也有 main() 函数，这是整个程序中真正的main
2. 写代码如下

Clock 类中有 Display 类型的 hour 和minute。在这里要特别小心的是，当把代码写成```private Display hour;```这个样子，hour 是成员变量，Display 是它的类型，这个时候的 Display 的对象有没有呢？没有。以前说过，对象变量是对象的管理者不是所有者。这个时候对象还没有呢。对象需要new 出来，所有要先new 一个出来。  

如何输出，可以使用printf，表示带格式的输出。然后使用字符串表示我们需要什么样的格式"%02d:%02d\n"，其中冒号是会固定输出的内容，而%开头一直到d为止表示要输出一个整数，而且这个整数一定占据两个字符的位置，如果它只有个位数，用0填上。  

在我们的 clock 这个项目里面有两个类 Display 和 Clock，这两个类都有 main 函数，但是不影响我们的使用。打开 Clock.java 时，他就会运行 Clock 类中的 main 函数。

```java
package clock;

public class Clock {
    private Display hour = new Display(24);
    private Display minute = new Display(60);

    public void start()
    {
    	while(true)
    	{
	    	minute.increase();
	    	if(minute.getValue() == 0)
	    	{
	    		hour.increase();
	    	}
	    	System.out.printf("%02d:%02d\n", hour.getValue(), minute.getValue());
    	}
    }

	public static void main(String[] args) {
		Clock clock = new Clock();
		clock.start();

	}

}
```
在这个程序中想重点表达的是，一个类里面的成员变量可以是其他类的对象，最终的结局是一个对象是由其他对象组成的。这个类可以让这两个对象互动。


###  2.2 访问属性
####  2.2.1 封闭的访问属性
对象可以是这样的东西，把它想象成一个剖开的鸡蛋，里面是表达这个对象的属性数据，外面包围起来的是针对这个对象的操作，或者说是针对这些数据的操作，是对象对外提供的一些服务。外面的蛋白紧紧的把蛋黄包围起来，这就叫做封装。  

**private**  
 只能用于成员变量或者成员函数，表示是这个类私有的，私有的表示只有在这个类的内部才能访问它。  

**对于成员变量只有两个地方才能访问它，一个地方是成员函数里面或者构造函数里，另一个地方时成员变量定义初始化的时候，可以使用别的已经定义的成员变量来初始化。其他地方一律不能使用。** 类中的 main 函数可以使用成员变量，但这是特殊情况。  

除非有合理的理由，否则成员变量都是私有的。成员变量只有是私有的，才能按照类的设计者的设计进行改变。

##### private
* 只有这个类内部可以访问
    + 类内部指类的成员函数和定义初始化
    + **这个限制是对类的而不是对对象的**

##### public
* 任何人都可以访问
    + 任何人指的是在任何类的函数或定义初始化中可以使用
    + 使用指的是调用、访问或定义变量

##### friendly
如果没有在成员（成员变量或成员函数）前面加 private 或 public关键字来限定它，我们称它为 friendly。意思是说和它位于同一个包的类可以访问。

##### protected
将继承时再说

####  2.2.2 开放的访问属性
##### 类用 public 修饰
**一个类前面有 public，表示任何人可以使用这个类来定义变量。有个限制条件，就是这个类必须处在源代码文件中，并且这个源代码文件名必须和这个类的名字相同。**

##### 编译单元
一个源代码文件，或者一个.java文件时一个编译单元。编译单元意思是编译源代码文件的时候一次是对这个编译单元进行编译的动作，一次拿一个.java文件来做编译。

在一个编译单元里面可以很多 java 类，但只能有一个类是 public。如果一个类前面没有 public，那个这个类只能在这个包里面起作用，出了这个包就不能起作用了。


###  2.3 包
在 Ecplise 中，如果做了一个 project 叫 clock，在这个 clock 里面 new 一个 class，它就会自动添加 clock 的包。  
![packageExample](image/part2/packageExample.png)  
可以看到在类 Clock 和 clock project项目中间有 src 和 clock。  
![packageExample2](image/part2/packageExample2.png)  
在 Display.java 和 Clock.java 文件的第一行都有一行 package clock; 这又是做什么的？  

在 Ecplise 的 workspace 中找到 clock 文件夹。在这个文件夹中有一个 src 目录，src 目录下有 clock 目录，clock 目录下有 Clock.java 和 Display.java 文件。文件夹的结构和 Ecplise 的结构一样。

如果要使用另外一个包里面的那个类，那就要 import 导入到当前文件中。**只要使用的类不在当前包里面，就要 import 它。所以 import 的用法是 包的名字.包里类的名字; 。如果有了一个包，那个源代码文件的第一行就一定是那个包的名字。表明我们用文件夹来管理包。**  

在一个目录下的所有的文件、所有的源代码文件、编译单元，它们都是属于同一个包，那个包的名字就是那个目录的名字。

这样还形成了另一个结果。例如 import display.Display; 表示 display 包下的 Display类,这就形成了 display.Display 类的全名。如果不使用 import，在源代码文件中使用类的全名也可以。

也可以使用 import display.* ; 通配符*，这种方法可以用，但不建议，因为如果有重名的东西，把他们引进来可能会引起和别的东西的冲突。

包的名字里面可以带有.（这里指包的名字，不是包的名字.类）表示的是在文件系统中文件夹的层次，每一个点表示一个文件夹层次。java 通过这种手段来管理这些类，给这些类起上全名，然后分门别类的放到不同的包里面，形成有效类的管理机制，**这种管理机制叫做包**。

我们要把一个类放到一个包里面，只需要建立一个目录，然后在前面说 package 什么什么；要使用别的包里面的类，要 import 那些东西。这就是 java 报的管理机制。


###  2.4 类成员
####  2.4.1 类变量
##### static  
开始接触 java，就遇到过 static。我们使用的 main 函数就是 public static void main。static 是做什么的？(一般不使用 静态 来解释 static，因为它不是一般意义上的静态和动态)  

在成员变量前加 static.

```java
package clock;

public class Display {
    private int value = 0;
    private int limit = 0;  //最好写上初值
    private static int step = 1;  // 测试 static

    public Display(int limit)
    {
    	this.limit = limit;
    }

    public void increase()
    {
    	value++;
    	if(value == limit)
    	{
    		value = 0;
    	}
    }

    public int getValue()
    {
    	return value;
    }

	public static void main(String[] args) {
		Display d1 = new Display(10);
		Display d2 = new Display(20);
		d1.increase();
		System.out.println(d1.getValue());
		System.out.println(d2.getValue());
		System.out.println(d1.step);
		System.out.println(d2.step);
		d1.step = 2;
		System.out.println(d1.step);
		System.out.println(d1.step);
    Display.step = 3;
    System.out.println(d1.step);
    System.out.println(d2.step);

	}

}

```
结果为 1 0 1 1 2 2 3 3  

static 的表现是通过一个对象来修改 static，那么其他对象中的 static 也跟着修改。  
Display.step = 3; 也可以修改 step，但 Display 是个类，也可以修改 step。类是定义，是规范，决定者类长什么样子，有什么样的成员变量，什么样的成员函数。成员变量是在对象中，不在类中。现在可以使用类的名字.static 变量的名字来访问这个变量。不是static 类型的变量，是不能使用这种方式的。

**所以 static 成员变量是 类变量。** 它不是成员变量，它是类的变量，它不属于类的任何一个对象，它属于这个类，所以这个类的任何对象都拥有这个变量，但只有一份，这个变量不在任何一个对象里面。

####  2.4.2 类函数
对于类中的 public static void main(String[] args)函数，函数前面的 static 表示这个函数不属于任何对象，这个函数属于这个类。这个函数不能直接调用对象中的任何函数，想调用要使用对象名.函数名。  
如果这个类中有其他的 static 修饰的函数，则这些函数可以相互调用，当然也可以使用对象名.函数名调用。当然 static 函数中也不能调用非 static 变量。  

规则很简单，static 函数只能调用 static 函数，只能访问 static 成员变量。static 成员函数和 static 成员函数可以通过对象的名字去访问，也可以通过某个对象的名字进行访问，只是通过某个对象进行访问的时候他不能获得这个对象的信息。

static 变量的初始化只能做一次。只在类的装载中初始化一次。和对象的创建没有关系。


###  2.5 初识容器
####  2.5.1 记事本例子
记事本的功能：记住一些条目信息。  
如何写程序实现这个记事本？  

##### 需求分析
记事本有哪些功能，即对记事本的需求是什么？  
* 能存储记录
* 不限制能存储的记录的数量
* 能知道已经存储的记录的数量
* 能查看存进去的每一条记录
* 能删除一条记录
* 能列出所有的记录

##### 接口设计
* add(String note);
* getSize();
* getNote(int index);
* removeNote(int index);
* list();

人机交互和业务逻辑
人机交互指的是输入的地方和输出的地方  
业务逻辑对输入数据进行计算的部分  

真正的软件里面的界面 UI 和业务逻辑要分离  
这里的接口设计只考虑业务逻辑。  

每个类都有一个 main函数，方便进行调试。  
接口编写如下：
```java
package notebook;

public class NoteBook {

	public void add(String s)
	{

	}

	public int getSize()
	{
		return 0;
	}

	public String getNote(int index)
	{
		return "";
	}

	public boolean removeNote(int index)
	{
		return true;
	}

	public String[] list()
	{
		return new String[10];
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub

	}

}

```

####  2.5.2 泛型容器
##### 容器类
* ArrayList<String> notes = new ArrayList<String>;

* 容器类有两个类型：
    + 容器的类型（例如ArrayList）
    + 元素的类型（例如String）

容器类是这样的一种东西，它用来存放对象，在里面可以存放任意数量的对象。

```java
package notebook;

import java.util.ArrayList;

public class NoteBook {
	private ArrayList<String> notes = new ArrayList<String>();  // ArrayList<String> 是泛型类，是一种容器

	public void add(String s)
	{
		notes.add(s);
	}

	public int getSize()
	{
		return notes.size();
	}

	public String getNote(int index)
	{
		return "";
	}

	public boolean removeNote(int index)
	{
		return true;
	}

	public String[] list()
	{
		return new String[10];
	}

	public static void main(String[] args) {
		String[] a = new String[2];
		a[0] = "fist";
		a[1] = "second";
		NoteBook nb = new NoteBook();
		nb.add("first");
		nb.add("second");
		System.out.println(nb.getSize());

	}

}
```

####  2.5.3 ArrayList 类的基本操作

使用容器类时，要清楚类中的所有的操作，用它提供的操作，效率更高。

```java
package notebook;

import java.util.ArrayList;

public class NoteBook {
	private ArrayList<String> notes = new ArrayList<String>();  // ArrayList<String> 是泛型类，是一种容器

	public void add(String s)
	{
		notes.add(s);
	}

	public void add(String s, int location)
	{
		notes.add(location, s);
	}
	public int getSize()
	{
		return notes.size();
	}

	public String getNote(int index)
	{
		return notes.get(index);
	}

	public void removeNote(int index)
	{
		notes.remove(index);
	}

	public String[] list()
	{
		String[] a = new String[notes.size()];
//		for(int i=0; i<notes.size(); i++)
//		{
//			a[i] = notes.get(i);
//		}
		notes.toArray(a);
		return a;
	}

	public static void main(String[] args) {
		NoteBook nb = new NoteBook();
		nb.add("first");
		nb.add("second");
		nb.add("third", 1);
		System.out.println(nb.getSize());
		System.out.println(nb.getNote(0));
		System.out.println(nb.getNote(1));
		nb.removeNote(1);
		String[] a = nb.list();
		for(String s : a)
		{
			System.out.println(s);
		}

	}

}

```
