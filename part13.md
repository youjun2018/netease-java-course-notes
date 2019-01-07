
## 第三章：循环
### 3.1 循环（while和do-while循环）
#### 3.1.1 循环
##### 自动售票机实现循环
``` java
public class Main{
    public static void main(String[] args){
//        初始化
        Scanner in = new Scanner(System.in);
        int balance = 0;
//        读入投币金额
    while(true){
            System.out.print("请投币：");
            int amount = in.nextInt();
            balance = balance + amount;
            if(balance >= 10)
            {
    //        打印车票
                System.out.println("*******************");
                System.out.println("* Java城际铁路专线 *");
                System.out.println("*   无指定座位票   *");
                System.out.println("*    票价：10元    *");
                System.out.println("*******************");
    //        计算并打印找零
                System.out.println("找零：" + （balance-10));
                balance = 0;
            }
        }
    }
}
```

注：选中一行按 "tab"，选中部分会自动向右缩进

#### 3.1.2 数数字
*  程序要读入一个正整数，然后输出这个整数的位数。如：
*  输入：352，输出：3
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int number = in.nextInt();
        int count = 0;
        while(number > 0)
        {
            number = number / 10;
            count = count + 1;
        }
        System.out.println(count);
    }
}
```

#### 3.1.3 while循环
注：Atom 的流程图怎么画？
*  循环体内要有改变条件的机会

##### while 循环
*  如果我们把 while 翻译作“当”，那么一个 while 循环的意思就是：当条件满足时，不断地重复循环体内的语句。
*  循环执行之前判断是否继续循环，所以有可能循环一次也没有被执行；
*  条件成立是循环继续的条件。

##### 看程序运行结果
*  人脑模拟计算机的运行，在纸上列出所有的变量，随着程序的进展不断重新计算变量的值。当程序运行结束时，留在表格最下面的就是程序的最终结果。又名：**变量表格**。把所有变量放在第一行，向下列出所有的变量变化的值。

##### 调试
*  在程序适当的地方插入输出来显示变量的内容

##### debug
*  设置断点进行调试

##### 验证
*  测试程序常使用边界数据，如有效范围两端的数据、特殊的倍数等
*  个位数；
*  10；
*  0；
*  负数。

#### 3.1.4 do-while循环
*  上面的程序对 0 是不能输出正确结果的。因为是先判断再执行循环体。
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int number = in.nextInt();
        int count = 0;
        do
        {
            number = number / 10;
            count = count + 1;
        }while(number > 0);
        System.out.println(count);
    }
}
```
##### do-while循环
*  在进入循环的时候不做检查，而是在执行完一轮循环体的代码之后，再来检查循环的条件是否满足，如果满足则继续下一轮循环，不满足则结束循环。
```
do
{
    <循环体语句>
}while(<循环条件>);  //分号不能省
```
![flow-while](image/part1/flow-while.png)

##### 两种循环
*  do-while 循环和while 循环很像，区别是在循环体执行结束的时候才来判断条件。也就是说，无论如何，循环都会执行至少一遍，然后再来判断条件。与 while 循环相同的是，条件满足时执行循环，条件不满足时结束循环。
*  **do-while 循环后的分号不能丢掉，表明循环在这里终止**

### 3.2 for循环
#### 3.2.1 for循环
##### 阶乘
*  n! = 1 $\times$ 2 $\times$ 3 $\times$ 4 $\times$ ... $\times$ n
*  写一个程序，让用户输入 n，然后计算输出 n!
*  变量：
*  显然读用户的输入需要一个 int 的 n，然后计算的结果需要用一个变量保存，可以是 int 的 factor，在计算中需要有一个变量不断地从 1 递增到 n，那可以是 int 的 i

*  学编程最重要的是：从问题到程序这中间您是怎么过来的。现在要做这一件事情，想程序时要想两件事情，第一件事情我有什么样的数据要表达。我要让用户输入一个n，然后计算这个n的阶乘，显然这个n是我要表达的。我在做计算时会有一个结果，这个结果在计算过程中要记录的，最后要输出的，这肯定也是一个要表达的数据。计算的方法呢，这是一个简单的计算，直接做就行。
```Java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int i = 1;
        int factor = 1;
        while(i <= n)
        {
            factor = factor * i;
            i = i + 1;
        }
        System.out.println(factor);
    }
}
```
*  表达累积的结果应该初始化为1
*  当输入数为20时，阶乘结果为负数。为什么不能算很大的阶乘？
*  在计算机中，int 用 4 个byte 表示，最大是 $2^{31} - 1$，最小是 $-2^{31}$。而20的阶乘很大。

* for 循环实现
```Java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int i = 1;
        int factor = 1;
        // while(i <= n)
        // {
        //     factor = factor * i;
        //     i = i + 1;
        // }
        for(i=1; i<=n; i=i+1)
        {
            factor = factor * i;
        }
        System.out.println(factor);
    }
}
```
##### for循环
for 循环像一个计数循环：设定一个计数器，初始化它，然后在计数器到达某值之前，重复执行循环体，而每执行一轮循环，计数器值以一定步进进行调整，比如加1或者减1。
```Java
for(i=0; i<5; i=i+1){
    System.out.println(i);
}
```
```Java
for(初始化 ; 条件 ; 单步动作){

}
```
1. 第一个部分是一个初始化，可以定义一个新的变量：int count=10 或者直接赋值：i=10。
2. 第二个部分是循环维持的条件。这个条件是先验的，与 while 循环一样，进入循环之前，首先要检验条件是否满足，条件满足才执行循环；条件不满足就结束循环。
3. 第三个部分是步进，即每轮执行了循环体之后，必须执行的表达式。通常我们在这里改变循环变量，进行加或减的操作。

##### for = 对于
*  for(count=10; count>0; count=count-1)
*  就读成：“对于一开始的count=10，每当count>0时，重复做循环体，每一轮循环在做完循环体内语句后，使得 count 递减。”

* 循环控制变量 i 只在循环里被使用了，在循环外面它没有任何用处。因此，我们可以把变量 i 的定义写到 for 语句里面去。
```Java
int n = in.nextInt();
int factor = 1;
for(int i=1; i<=n; i=i+1)
{
    factor = factor * i;
}
System.out.println(factor);
```
![for=while](image/part1/for=while.png)
```
for(初始动作; 条件; 每轮的动作){

}
```
*  for中的每一个表达式都是可以省略的, for(;条件;) == while(条件)

##### 空循环
```java
for(i=0; i<10; i++);

for(i=0; i<10; i++)
    System.out.println(i);
```
注： 强烈建议：只要是for语句，就一定跟上一对大括号

##### 循环次数
*  for(i=0; i<n; i=i+1)
*  则循环的次数是 n，而循环结束以后，i 的值是 n。循环的控制变量 i，是选择从 0 开始还是从 1 开始，是判断 i<n 还是判断 i<=n，对循环的次数，循环结束后变量的值都有影响

![three-loop](image/part1/three-loop.png)

##### **Tips for loops**
*  如果有固定次数，用 for
*  如果必须执行一次，用 do_while
*  其他情况用 while

#### 3.2.2 复合赋值
##### 符合赋值
*  5个算术运算符，+ - * / %，可以和赋值运算符“=”结合起来，形成复合赋值运算符：“+=”、“-=”、“\*=”、“/=”、“%=”
*  total += 5
*  total = total + 5
*  注意两个运算符中间不要有空格
*  前置++i和后置i++，建议单独使用，不要用在复杂的运算中

### 3.3 循环控制（含复合赋值、逻辑类型）
#### 3.3.1 循环控制
##### 素数
*  只能被 1 和自己整除的数，不包括1
*  2,3,5,7,11,13,17,19...
```Java
import java.unti.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nexitInt();
        int isPrime = 1;
        for(int i=2; i<n; i++)
        {
            if(n % i == 0)
            {
                isPrime = 0;
                System.out.println(n + "不是素数,i=" + i);
                break;  //当循环不需要进行下去，可以用break 跳出循环。
            }
        }
        if(isPrime ==1)
        {
            System.out.println(n + "是素数");
        }
        else
        {
            System.out.println(n + "不是素数");
        }
    }
}
```

```Java
int sum = 0;
int number = 0;

while(number < 20) {
    number++;
    sum += number;
    if(sum >= 100)
        break;
}

System.out.println("The number is " + number);
System.out.println("The sum is " + sum);
```

##### break vs continue
*  break: 跳出循环
*  continue: 跳过循环这一轮剩下的语句进入下一轮
![break-vs-continue](image/part1/breakvscontinue.png)

#### 3.3.2 多重循环
##### 100 以内的素数
*  如何写程序输出 100 以内的素数？
```Java
import java.unti.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
//        int n = in.nexitInt();
        for(int n=2; n<100; n++)
        {
            int isPrime = 1;
            for(int i=2; i<n; i++)
            {
                if(n % i == 0)
                {
                    isPrime = 0;
                    System.out.println(n + "不是素数,i=" + i);
                    break;  //当循环不需要进行下去，可以用break 跳出循环。
                }
            }
            if(isPrime ==1)
            {
                System.out.print(n + "是素数");
            }
            else
            {
                // System.out.println(n + "不是素数");
            }
        }
    }
}
```
##### 多重循环
```Java
for(int n1=0; n1<10; ++n1)
{
    for(int n2=0; n2<50; ++n2)
    {
        System.out.println(n1 + ":" + n2);
    }
}
```
#### 九九乘法表
```java
for(int i=1; i<=9; i++)
{
    for(int j=1; j<=9; j++)
    {
        System.out.println("\t"+(i * j));
    }
    System.out.println();
}
```

##### 前50个素数
*  如何写程序输出前50个素数

##### 凑硬币
*  如何用 1角、2角和5角的硬币凑出 10 元以下的金额呢？
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int amount = scan.nextInt();
		scan.close();
		for(int one = 0; one <= amount; ++one)
		{
			for(int five = 0; five <= amount/5; ++five)
			{
				for(int ten = 0; ten <= amount/10; ++ten)
				{
					for(int twenty = 0; twenty <= amount/20; ++twenty)
					{
						if(one + five*5 + ten*10 + twenty*20 == amount)
						{
							System.out.println(one + "张1元，"+ five + "张5元，" + ten + "张10元，" + twenty + "张20元." + "->" + amount);
						}
					}
				}
			}
		}
	}
}
```
*  如果得到一个结果就返回怎么办？
*  break 只能返回最内层循环。
*  **使用标号**
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int amount = scan.nextInt();
		scan.close();
		OUT:
		for(int one = 0; one <= amount; ++one)
		{
			for(int five = 0; five <= amount/5; ++five)
			{
				for(int ten = 0; ten <= amount/10; ++ten)
				{
					for(int twenty = 0; twenty <= amount/20; ++twenty)
					{
						if(one + five*5 + ten*10 + twenty*20 == amount)
						{
							System.out.println(one + "张1元，"+ five + "张5元，" + ten + "张10元，" + twenty + "张20元." + "->" + amount);
							break OUT;
						}
					}
				}
			}
		}

	}
}

```
##### break和continue
*  再循环前可以放一个标号来标示循环：
*  label:
*  带标号的break和continue对那个循环起作用

#### 3.3.3 逻辑类型
*  把 isPrime 类型改为 boolean。
```Java
import java.unti.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nexitInt();
        boolean isPrime = true;
        for(int i=2; i<n; i++)
        {
            if(n % i == 0)
            {
                isPrime = 0;
                System.out.println(n + "不是素数,i=" + i);
                break;  //当循环不需要进行下去，可以用break 跳出循环。
            }
        }
        if(isPrime)
        {
            System.out.println(n + "是素数");
        }
        else
        {
            System.out.println(n + "不是素数");
        }
    }
}
```
##### 逻辑类型
*  关系运算的结果是一个逻辑值，true或false。这个值可以保存在一个对应的逻辑类型的变量中，这样的变量类型是 boolean
*  布尔（Boolean）是为了纪念 George Boole 对逻辑计算的贡献
*  boolean flag = true;
*  boolean tooHigh, tooSmall, tooRough;
*  boolean done = false;

##### 逻辑运算
*  逻辑运算是对逻辑量进行的运算，只有逻辑量可以参与运算。
![luojiyunsuan](image/part1/luojiyunsuan.png)

##### TRY
*  如果要表达数学中的区间，如：$x \in (4,6)$ 或 $x \in [4,6]$ ，应该如何写 Java 的表达式？
*  像 4 < x < 6 这样的式子，不是 Java 能接受的式子，因为 4 < x 的结果是一个逻辑值，逻辑值是不能和数值6做关系计算的
*  x > 4 && x < 6

##### 优先级
*  ! > && > ||
*  !done && (count > MAX)
![youxianji](image/part1/youxianji.png)

### 3.4 循环应用
#### 3.4.1 计数循环
```Java
int count = 100;
while(count >= 0) {
    count = count - 1;
    System.out.println(count);
}
System.out.println("发射！");
```
*  这个循环需要执行多少次？
*  循环停下来的时候，有没有输出最后的0？
*  循环结束后，count 的值是多少？
*  小套路：
如果要模拟运行一个很大次数的循环，可以模拟较少的循环次数，然后作出推断。
*  如果改成 do-while 呢？
```Java
int count = 100;
do
{
    count = count - 1;
    System.out.println(count);
}while(count >= 0);
System.out.println("发射！");
```

#### 3.4.2 算平均数
$sum = \frac{\sum_{i=0}^{n}X_{i}}{n}$
*  让用户输入一系列的正整数，最后输入-1表示输入结束，然后程序计算出这些数字的平均数，输出输入的数字的个数和平均数
*  变量 -> 算法 -> 流程图 -> 程序
*  写程序，要想两件事情，一个是输入的数据，在计算中要表达它，计算过程中的数据要怎么表达它；二是要做计算，这些计算有哪些步骤，最后得到怎么样的结果。

##### 变量
*  一个记录读到的整数的变量
*  平均数要怎么算？
*  只需要每读到一个数，就把它加到一个累加的变量里，到全部数据读完，再拿它去除读到的数的个数就可以了
*  一个变量变量记录累加的结果，一个变量记录读到的数的个数
![pingjunshu](image/part1/pingjunshu.png)
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int number;
		int sum = 0;
		int count = 0;
//		number = scan.nextInt();
//		while(number != -1)
//		{
//			sum += number;
//			count += 1;
//			number = scan.nextInt();
//		}
		do
		{
			number = scan.nextInt();
			if(number != -1)
			{
				sum += number;
				count += 1;
			}
		}while(number != -1);  //输入 -1 程序结束
		scan.close();
		if(count>0)
		{
			System.out.print("平均数=" + (double)sum/count);
		}


	}
}

```

#### 3.4.3 猜数游戏
*  让计算机来想一个数，然后让用户来猜，用户每输入一个数，就告诉它是大了还是小了，直到用户猜中为止，最后还要告诉用户它猜了多少次。
*  因为需要不断重复让用户猜，所以需要用到循环
*  在实际写出程序之前，我们可以先用文字描述程序的思路
*  核心重点是循环的条件
*  人们往往会考虑循环终止的条件

1. 计算机随机想一个数，记在变量 number 里；
2. 一个负责计次数的变量 count 初始化为 0；
3. 让用户输入一个数字a；
4. count 递增（加一）；
5. 判断 a 和 number 的大小关系，如果 a 大，就输出“大”；如果 a 小就输出 “小”；
6. 如果 a 和 number 是不相等的（无论大还是小），程序转回到第3步；
7. 否则，程序输出“猜中”和次数，然后结束。

*  for 和 while 循环的循环条件是循环维持的条件，不是离开的条件。
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int number = (int)(Math.random()*100 + 1); //[0,1) -->[0,100) -->[1,101) --> [1,100]
		int a;
		int count = 0;
		do {
			a = scan.nextInt();
			count += 1;
			if(a > number)
			{
				System.out.println("偏大");
			}
			else if(a < number)
			{
				System.out.println("偏小");
			}
		} while(a != number);

		System.out.println("恭喜您猜对了，您猜了" + count + "次");
		scan.close();
	}
}
```

#### 3.4.4 整数分解
*  先不考虑 while 还是 do-while，先写循环体内的部分；最后在想循环条件是使循环维持的条件；
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int number;
		number = scan.nextInt();
		int result = 0;
		do{
			int digit = number % 10;
			result = result * 10 + digit;
			number = number / 10;
		}while(number > 0);
		System.out.println(result);
		scan.close();
	}
}
```

#### 3.4.5 求和
$f(n) = 1 + \frac{1}{2} + \frac{1}{3} + \frac{1}{4} + ... + \frac{1}{n}$
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		double sum = 0.0;
		for(int i=1; i<=n; ++i)
		{
			sum += 1.0 / i;
		}
		System.out.println(sum);
		System.out.printf("%.2f", sum);  // printf 表示按照自定义格式输出，会自动四舍五入
		scan.close();
	}
}
```
$f(n) = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + ... + \frac{1}{n}$
*  方法一：增加符号位，符号依次正负交替
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		double sum = 0.0;
		int sign = 1;
		for(int i=1; i<=n; ++i)
		{
			sum += sign*1.0 / i;
			sign = -sign;
		}
		System.out.println(sum);
		System.out.printf("%.2f", sum);  // printf 表示按照自定义格式输出，会自动四舍五入
		scan.close();
	}
}
```

*  方法二：i 值偶数为负，奇数为正
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		double sum = 0.0;
//		int sign = 1;
		for(int i=1; i<=n; ++i)
		{
//			sum += sign*1.0 / i;
//			sign = -sign;
			if(i%2 == 1)
			{
				sum += 1.0 / i;
			}
			else
			{
				sum -= 1.0 / i;
			}
		}
		System.out.println(sum);
		System.out.printf("%.2f", sum);  // printf 表示按照自定义格式输出，会自动四舍五入
		scan.close();
	}
}
```
*  在 for 循环的每个表达式中，可以使用逗号放多个表达式
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		double sum = 0.0;
		int sign = 1;
		for(int i=1; i<=n; ++i,sign = -sign)
		{
			sum += sign*1.0 / i;
		}
		System.out.println(sum);
		System.out.printf("%.2f", sum);  // printf 表示按照自定义格式输出，会自动四舍五入
		scan.close();
	}
}
```

#### 3.4.6 最大公约数
##### 求最大公约数
*  输入两个数 a 和 b，输出它们的最大公约数
*  输入：12 18
*  输出：6

##### 枚举
1. 设 i 为 2；
2. 如果a 和 b 都能被 i 整除，则记下这个i;
3. i 加 1 后重复第2步，直到 i 等于 a 或 b;
4. 那么，曾经记下的最大的可以同时整除 a 和 b 的 i 就是 gcd。

```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int a = scan.nextInt();
		int b = scan.nextInt();
		int gcd = 1;
		for(int i=2; i<=a && i<=b; i++)
		{
			if(a % i == 0 && b % i == 0)
			{
				gcd = i;
			}
		}
		System.out.println(a+"和"+b+"的最大公约数是"+gcd);  // printf 表示按照自定义格式输出，会自动四舍五入
		scan.close();
	}
}
```

##### 辗转相除法
1. 如果 b 等于 0，计算结束，a 就是最大公约数；
2. 否则，计算 a 除以 b 的余数，让 a 等于 b，而 b 等于那个余数；
3. 回到第一步。
*  最好保证 a > b
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scan = new Scanner(System.in);
		int a = scan.nextInt();
		int b = scan.nextInt();
		int oa = a;
		int ob = b;
		while(b!=0)
		{
			int r = a % b;
			System.out.println(a+","+b+","+r);
			a = b;
			b = r;
		}

		System.out.println(oa+"和"+ob+"的最大公约数是"+a);  // printf 表示按照自定义格式输出，会自动四舍五入
		scan.close();
	}
}
```
