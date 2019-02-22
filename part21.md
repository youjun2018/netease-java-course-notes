#  Java 基础入门：面向对象程序设计
##  第一章：类与对象
###  1.1 用类制造对象
####  1.1.1 Shape 源码
可以参考文件夹shape

#####  Circle.java
```Java
package shapes;

import java.awt.Graphics;

public class Circle extends Shape {
	private int x;
	private int y;
	private int radius;

	public Circle(int x, int y, int radius)
	{
		this.x = x;
		this.y = y;
		this.radius = radius;
	}
	@Override
	public void draw(Graphics g) {
		g.drawOval(x-radius, y-radius, radius*2, radius*2);
	}
}
```
#####  Line.java
```java
package shapes;

import java.awt.Graphics;

public class Line extends Shape {
	private int x1;
	private int y1;
	private int x2;
	private int y2;

	public Line(int x1, int y1, int x2, int y2)
	{
		this.x1 = x1; this.y1 = y1;
		this.x2 = x2; this.y2 = y2;
	}

	@Override
	public void draw(Graphics g) {
		g.drawLine(x1, y1, x2, y2);
	}

}
```

#####  MyPic.java
```java
package shapes;

public class MyPic {
	public static void main(String[] args)
	{
		Picture pic = new Picture(420,300);
		Circle c1 = new Circle(320,40,80);
		Rectangle r1 = new Rectangle(100, 100, 100, 100);
		Triangle t1 = new Triangle(100, 100, 200, 100, 150, 50);
		Line l1 = new Line(0,205,400,205);
		Circle c2 = new Circle(200,200,50);
		pic.add(c1);
		pic.add(r1);
		pic.add(t1);
		pic.add(l1);
		pic.add(c2);
		pic.draw();
	}
}

```

#####  Picture.java
```java
package shapes;

import java.awt.Graphics;
import java.util.ArrayList;

import javax.swing.JFrame;
import javax.swing.JPanel;

public class Picture extends JFrame {
	private static final long serialVersionUID = 1L;
	private int width;
	private int height;

	private ArrayList<Shape> listShape = new ArrayList<Shape>();

	private class ShapesPanel extends JPanel {
		private static final long serialVersionUID = 1L;

		@Override
		protected void paintComponent(Graphics g) {
			super.paintComponent(g);
			for ( Shape s : listShape )
			{
				s.draw(g);
			}			
		}

	}

	public void add(Shape s)
	{
		listShape.add(s);
	}

	public Picture(int width, int height)
	{
		add(new ShapesPanel());
		this.setDefaultCloseOperation(EXIT_ON_CLOSE);
		this.width = width;
		this.height = height;
	}

	public void draw()
	{
		setLocationRelativeTo(null);
		setSize(width, height);
		setVisible(true);
	}
}
```

#####  Rectangle.java
```java
package shapes;

import java.awt.Graphics;

public class Rectangle extends Shape {
	private int x;
	private int y;
	private int width;
	private int height;

	public Rectangle(int x, int y, int width, int height) {
		this.x = x;
		this.y = y;
		this.width = width;
		this.height = height;
	}

	@Override
	public void draw(Graphics g) {
		g.drawRect(x, y, width, height);
	}

}

```

#####  Shape.java
```java
package shapes;

import java.awt.Graphics;

public abstract class Shape {

	public abstract void draw(Graphics g);

}

```

#####  Triangle.java
```java
package shapes;

import java.awt.Graphics;

public class Triangle extends Shape {
	private int[] x = new int[3];
	private int[] y = new int[3];

	public Triangle(int x1, int y1, int x2, int y2, int x3, int y3)
	{
		x[0] = x1; x[1] = x2; x[2] = x3;
		y[0] = y1; y[1] = y2; y[2] = y3;
	}

	@Override
	public void draw(Graphics g) {
		g.drawPolygon(x, y, x.length);
	}

}

```

####  1.1.2 用类制造对象
如果不记得 Ecplise 目录放在哪，可以这么找回：  
Ecplise 上部 --> File --> Switch Workspace --> Other --> 显示当前使用的workspace  
把项目代码放到当前 workspace 目录后，点击 File --> New --> Java Project --> 把 Project name 改成和项目代码名称一样的名字，然后 Finish，系统会自动找到刚才的代码。

使用 Shapes 源代码，实现上述所说。这只是示例。

#####  对象与类
* 对象是实体，需要被创建，可以为我们做事情
* 类是规范，根据类的定义来创建对象

######  * 对象（这只猫）
  * 表达东西或事件
  * 运行时响应消息（提供服务）

######  * 类（猫）
  * 定义所有猫的属性
  * 就是 Java 中的类型
  * 可以用来定义变量

###### 类 --（定义了）--> 对象  
###### 对象 --（是..的实体）--> 类

##### 对象 = 属性 + 服务
* 数据：属性或状态
* 操作：函数  

常常用蛋图表示对象这种关系  
![duixiang](image/part2/duixiang.png)
对象内部的数据要用操作紧紧包围着，不能简单的暴露到外面。  

##### 把数据和对数据的操作放在一起 --> 封装

##### OOP 特性
1. 一切都是对象
2. 程序就是一堆互相发送消息的对象
3. 每个对象有自己的存储空间，里面是其他的对象
4. 每个对象都有一个类型
5. 所有属于某个特定类型的对象可以提供相同的服务


###  1.2 定义类
####  1.2.1 定义类
例子：如何实现仿真自动售货机？  
1. 它有什么数据，需要做什么动作

#####  创建对象
* new VendingMachine();
* VendingMachine v = new VendingMachine()

* 对象变量是对象的管理者

#####  让对象做事
* .运算符
* v.insertMoney(10);
* v.getFood();


###  1.3 类的成员
####  1.3.1 成员变量和成员函数
我们在写类的时候可以定义一些变量，这些变量表达了属于这个类的所有对象应该具有的所有属性。将来在 new 出来这个类的每个对象之后，这些对象里面就有这些变量，每个对象还具有和其他对象不同的那些值。这是在 VendingMachine 中观察出来的。

#####  成员变量
* 类定义了对象中所具有的变量，这些变量称作成员变量
* 每个对象有自己的变量，和同一个类的其他对象时分开的

它有一种机制，可以使类的成员函数和当时调用这个成员函数的对象之间建立联系。是使用 this 实现的。

#####  函数与成员变量
* 在函数中可以直接写成员变量的名字来访问成员变量
* 那么究竟访问的是哪个对象的呢？

* 函数是通过对象来调用的
    * v.insertMoney()
    * 这次调用临时建立了 insertMoney() 和 v 之间的关系，让 insertMoney() 内部的成员变量指的是 v 的成员变量

##### this
* this 是成员函数的一个特殊的固有的本地变量，它表达了调用这个函数的那个对象。

##### 调用函数
* 通过.运算符调用某个对象的函数
* 在**内部直接**调用自己（this）的其他函数
    * 在成员函数内部调用其他成员函数，只需要直接调用就行，可以不加 this
    * 在成员函数外部，需要通过对象的名字来调用

##### 本地变量
* 定义在函数内部的变量是本地变量
    * 定义在函数外面的变量，这些变量叫做成员变量
* 本地变量的生存期和作用域都是函数内部
* 成员变量的生存期是对象的生存期，作用域是类内部的成员函数


###  1.4 对象初始化
####  1.4.1 对象初始化
成员变量在定义的时候没有赋初值，则会被默认赋值为0。最好手动赋初值。

#####  成员变量定义初始化
* 成员变量在定义的地方就可以给出初始值
    * 甚至可以使用函数，如果这个函数的执行不牵扯其他东西的话。
    * 可以使用构造函数给成员变量赋值
    * new 一个对象的执行顺序。**先执行构造函数函数名，然后去执行成员变量，最后进入到构造函数里面。（为什么要先执行构造函数函数名？因为这里可以给成员变量赋初值**）
* 没有给出初始值的成员变量会自动获得0值
    * 对象变量的0值表示没有管理任何对象，也可以主动给null值
* 定义初始化可以调用函数，甚至可以使用已经定义的成员变量

#####  构造函数
* 如果有一个成员函数的名字和类的名字完全相同，则在创建这个类的每一个对象的时候会自动调用这个函数 --> 构造函数
* 这个函数不能有返回类型
* 构造函数可以重载

**调用函数时会根据所给函数值的方式（有多少值，每个值得类型）来决定调用那个函数，这件事情叫做重载。**

##### 函数重载
* 一个类可以有多个构造函数，只要他们的参数表不同
* 创建对象的时候给出不同的参数值，就会自动调用不同的构造函数
* 通过 this() 还可以调用其他构造函数
* 一个类里的同名但参数表不同的的函数构成了重载关系

* 构造函数的一个特殊的用法，使用 this 调用其他的构造函数，例如：
```java
VendingMachine(int price)
{
    this();
    this.price = price;
}
```
**但这个 this 只能在构造函数中，并且是在构造函数的第一句。**
