
## 第五章：函数
### 5.1 函数的定义和调用
#### 5.1.1 定义函数
#####  对象的操作
*  String s = "hello";
*  int i = s.length();
*  System.out.println(s + "bye");
*  这些都是对象在执行函数

#####  求素数的函数
```Java
import java.util.Scanner;

public class Main {
	public static boolean isPrime(int i)
	{
    //  判断素数
		boolean isPrime = true;
		for(int k=2; k<i; k++)
		{
			if(i % k == 0)
			{
				isPrime = false;
				break;
			}
		}
		return isPrime;
	}

	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		int m = in.nextInt();
		int n = in.nextInt();
		if(m == 1) m = 2;
		int cnt = 0;
		int sum = 0;
		for(int i=m; i<=n; i++)
		{

			//  做计算
			if(isPrime(i))
			{
				cnt ++;
				sum += i;
			}
		}
		System.out.println("在"+m+"和"+n+"之间有"+cnt+"个素数，总和为"+sum);


		in.close();
	}
}
```
#####  求和
*  求出 1 到 10、 20 到 30 和 35 到 45 的三个和
*  一般的做法：
```Java
int i;
int sum;
sum = 0;
for(i=1; i<=10; i++)
{
	  sum += i;
}
System.out.println(1+"到"+10+"的和是"+sum);
sum = 0;
for(i=20; i<=30; i++)
{
	  sum += i;
}
System.out.println(20+"到"+30+"的和是"+sum);
sum = 0;
for(i=35; i<=45; i++)
{
	  sum += i;
}
System.out.println(35+"到"+45+"的和是"+sum);
```

*  三段几乎一模一样的代码！
*  “代码复制”是程序质量不良的表现
*  推荐如下
```Java
public class Main {
	public static void sum(int a, int b)
	{
		int i;
		int sum;
		sum = 0;
		for(i=a; i<=b; i++)
		{
			sum += i;
		}
		System.out.println(a+"到"+b+"的和是"+sum);
	}

	public static void main(String[] args) {
		sum(1,10);
		sum(20,30);
		sum(35,45);
	}
}
```
#####  什么事函数？
*  函数是一块代码，接收零个或多个参数，做一件事情，并返回零个或一个值
*  可以先想象成数学中的函数：
    * y = f(x)

#####  函数定义
```Java
public static void sum(int a, int b)  //  函数头，园括号前面的叫函数名，
{                                    //  函数名前面的是返回值，园括号里面的是参数表，逗号分隔
  int i;                             //  大括号中间的是函数体
  int sum;
  sum = 0;
  for(i=a; i<=b; i++)
  {
    sum += i;
  }
  System.out.println(a+"到"+b+"的和是"+sum);
}
```

#### 5.1.2 调用函数
#####  调用函数
*  函数名(参数值);
*  () 起到了表示函数调用的重要作用
    *  即使没有参数也需要()
*  如果有参数，则需要给出正确的数量和顺序
*  这些值会被按照顺序依次用来初始化函数中的参数

#####  函数返回
*  函数知道每一次是哪里调用它，函数结束的时候会返回到正确的地方

#####  从函数中返回值
*  return 停止函数的执行，并送回一个值
    *  return;
    *  return 表达式;
*  一个函数中不要有多个出口，这是不好的习惯

#####  没有返回值得函数
*  void 函数名(参数表)
*  不能使用带值得 return
    *  可以没有 return
*  调用的时候不能做返回值得赋值
*  如果函数有返回值，则必须使用带值得 return

### 5.2 函数的参数和本地变量
#### 5.2.1 参数传递
#####  调用函数
*  如果函数有参数，调用函数时必须传递给它数量、类型正确的值
*  可以传递给函数的值是表达式的结果，这包括：
    *  字面量
    *  变量
    *  函数的返回值
    *  计算的结果
```Java
int a = 5;
int b = 6;
int c;
c = max(10, 12);
c = max(a, b);
c = max(c, 23);
c = max(max(c,a), 5);
System.out.println(max(a,b));
max(12,13);
```

#####  类型不匹配？
*  当函数期望的参数类型比调用函数时给的值得类型宽的时候，编译器能悄悄替你把类型转换好(**隐式转换**)
    *  char --> int --> double
*  当函数期望的参数类型比调用函数时给的值得类型窄的时候，需要你写强制类型转换
    *  (int)5.0
*  当函数期望的参数类型与调用函数时给的值得类型之间无法转换的时候 -->  不行！

#####  传过去的是什么？
```java
public class Main {
	public static void swap(int a, int b)
	{
		int t;
		t = a;
		a = b;
		b = t;
	}

	public static void main(String[] args) {
		int a = 5;
		int b = 6;
		swap(a,b);
		System.out.println("a="+a+";b="+b);
	}
}
```
*  这样的代码能交换 a 和 b 的值吗？（不能）
*  **Java 语言在调用函数时，永远只能传值给函数**

#####  传值
*  每个函数有自己的变量空间，参数也位于这个独立的空间中，和其他函数没有关系
*  过去，对于函数参数表中的参数，叫做“形式参数”，调用函数时给的值，叫做“实际参数”
*  由于容易让初学者误会实际参数就是实际在函数中进行计算的参数，误会调用参数的时候把变量而不是值传进去了，所以我不建议继续使用这种古老的方式来称呼它们。
*  我们认为，它们是参数(parameter)和值(value)得关系。（函数中的数是参数，而调用函数时给的数叫值）

#####  当参数类型是数组或对象时？

#### 5.2.2 本地变量
#####  本地变量
*  函数的每次运行，就产生了一个独立的变量空间，在这个空间中的变量，是函数的这次运行所独有的，称作本地变量
*  定义在函数内部的变量就是本地变量
*  参数也是本地变量

######  变量的生存期和作用域
*  生存期：什么时候这个变量开始出现了，到什么时候它消亡了
*  作用域：在（代码的）什么范围内可以访问这个变量（这个变量可以起作用）
*  对于本地变量，这两个问题的答案是统一的：大括号内 -- 块

#####  本地变量的规则
*  本地变量是定义在块内的
    *  它可以是定义在函数的块内
    *  也可以定义在语句的块内
    *  甚至可以随便拉一对大括号来定义变量
*  程序运行进入这个块之前，其中的变量不存在，离开这个块，其中的变量就消失了。
*  块外面定义的变量在里面仍然有效
*  不能在一个块内定义同名的变量，也不能定义块外面定义过的变量
*  本地变量不会被默认初始化
*  参数在进入函数的时候被初始化了
