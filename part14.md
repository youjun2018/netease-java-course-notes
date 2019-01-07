
## 第四章：数组
### 4.1 数组的创建和使用
#### 4.1.1 初试数组
*  如何写一个程序计算用户输入的数字的平均数？
一般做法，输入一个数就加起来，不需要记录输入的每一个数
```java
Scanner in = new Scanner(System.in);
int x;
double sum = 0;
int cnt = 0;
x = in.nextInt();
while(x != -1)
{
    sum += x;
    cnt ++;
    x = in.nextInt();
}
if(cnt > 0)
{
  System.out.println(sum/cnt);
}

```
*  如何写一个程序计算用户输入的数字的平均数，并输出所有大于平均数的数？
*  必须先记录每一个输入的数字，计算平均数之后，再检查记录下来的每一个数字，与平均数比较，决定是否输出。

#####  如何记录很多数？
*  int num1, num2, num3...?
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner in = new Scanner(System.in);
		int x;
    int[] numbers = new int[100];   // 定义数组
    double sum = 0;
    int cnt = 0;
    x = in.nextInt();
    while(x != -1)
    {
        numbers[cnt] = x;  //对数组中的元素赋值
        sum += x;
        cnt ++;
        x = in.nextInt();
    }
    if(cnt > 0)
    {
        double average = sum/cnt;
        for(int i=0; i<cnt; ++i)
        {
            if(number[i] > average)  // 使用数组中的元素
            {
                System.out.println(numbers[i]);  // 使用数组中的元素
            }
        }
        System.out.println(numbers[i]);
      }
    }
}
```
*  以上数组有安全隐患，能看出来吗？  数组大小一旦固定，就不可修改了。输入的数据可能超过 100 个

#### 4.1.2 创建数组
##### 数组
*  是一种容器（放东西的东西），特点是：
    +  其中所有的元素具有相同的数据类型；
    +  一旦创建，不能改变大小
*  数组是一种数据结构，能记录同一种类型的多个数据
    +  数组中的每个数据叫做元素
    +  所有的元素具有相同的数据类型

#####  定义数组变量
*  <类型>[]<名字>= new <类型>[元素个数]
    +  int[] grades = new int[100];
    +  double[] average = new double[20];
*  **元素个数必须是整数**
*  **元素个数必须给出**
*  **元素个数可以是变量**

##### int[] a = new int[10]
*  创建了一个 int 型的数组
*  10个元素：a[0],a[1],...,a[9]

|a[0]|a[1]|a[2]|a[3]|a[4]|a[5]|a6]|a[7]|a[8]|a[9]|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|

*  每个元素是一个 int 的变量
*  可以读和写：
    *  a[2] = a[1] + 6;

#### 4.1.3 数组的元素
*  每个元素都是那种类型的变量
*  索引或下标是从 0 开始的
    *  grades[0]
    *  grades[99]
    *  average[5]

#####  有效的下标
*  最小的下标是 0， 最大的下标是数组的元素个数 - 1
*  可是编译器不会检查看你是否用了有效的下标
*  但是如果运行的时候出现了无效的下标，可能会导致程序终止

##### 元素个数可以是变量
```Java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner in = new Scanner(System.in);
    double sum = 0;
    int cnt = 0;
    cnt = in.nextInt();
    if(cnt > 0)
    {
        int[] numbers = new int[cnt];   // 定义数组
        for(int i=0; i<cnt; ++i)
        {
            numbers[i] = in.nextInt();
            sum += numbers[i];
        }
        double average = sum/cnt;
        for(int i=0; i<cnt; ++i)
        {
            if(number[i] > average)  // 使用数组中的元素
            {
                System.out.println(numbers[i]);  // 使用数组中的元素
            }
        }
        System.out.println(sum / cnt);
      }
    }
}
```
##### length
*  每个数组有一个内部成员 length，会告诉您它的元素的数量。
```Java
for(i=0; i<100; ++i)
    sum += grade[i];
// 最好是
for(i=0; i<grade.length; ++i)  //会输出数组中所有的元素，所有的；这个代码具有可扩展型
    sum += grade[i];
```

#### 4.1.4 投票统计
*  写一个程序，输入数量不确定的[0,9]范围内的整数，统计每一种数字出现的次数，输入 -1 表示结束
```java
import java.util.Scanner;
public class Main {
	  public static void main(String[] args) {
		    // TODO Auto-generated method stub
		    Scanner in = new Scanner(System.in);
        int x;
        int[] numbers = new int[10];  //  默认初始化为0
        x = in.nextInt();
        while(x != -1)
        {
            if(x>=0 && x<=9)  //一定要注意判断，因为数组越界会出问题
            {
                numbers[x] ++;
            }
            x = in.nextInt();
        }
        for(int i=0; i<numbers.length; ++i)
        {
            Syste.out.println(i+":"+numbers[i]);
        }
    }
}
```

### 4.2 数组变量和运算
#### 4.2.1 数组变量
##### 直接初始化数组
*  new 创建的数组会得到默认的 0 值
*  int[] scores = {87, 98, 69, 54, 65, 76, 87, 99};
*  直接用大括号给出数组的所有元素的初始值
*  不需要给出数组的大小，编译器替你数数
*  如何得知数组的大小？ length!

##### 数组变量赋值
```
int[] a = new int[10];
a[0] = 5;
int[] b = a;
b[0] = 16;
System.out.println(a[0]);  //  结果16
```
普通变量是变量中值得所有者，变量里面有数据；而数组变量只是管理者，变量里面没有数据，只有地址。
```Java
int[] a1 = {1,2,3,4,5};
int[] a2 = a1;
for(int i=0; i<a2.length; ++i)
{
    a2[i] ++;
}
for(int i=0; i<a1.length; ++i)
{
    System.out.prinlng(a1[i]);
}
```
![two_array](image/part1/two_array.png)

##### 数组变量
*  **数组变量是数组的管理者而非数组本身**
*  **数组必然创建出来然后交给数组变量来管理**
*  **数组变量之间的赋值是管理权限的赋予**
*  **数组变量之间的比较是判断是否管理同一个数组**

#####  复制数组
*  必然遍历源数组将每个元素逐一拷贝给目的数组
```java
import java.util.Scanner;
public class Main {
	  public static void main(String[] args) {
		    // TODO Auto-generated method stub
		    Scanner in = new Scanner(System.in);
        int[] a = {1,2,3,4,5};
        int[] b = new int[a.length];
        for(int i=0; i<b.length; ++i)
        {
            b[i] = a[i];
        }
        boolean isEqu = true;
        for(int i=0; i<b.length; ++i)
        {
            if(a[i] != b[i])
            {
              isEqu = false;
              break;
            }
            System.out.println(b[i]);
        }
        System.out.println(isEqu);
    }
}
```
注：最好先判断数组长度时候相等

#### 4.2.2 遍历数组
#####  搜索
*  在一组给定的数据中，如何找出某个数据是否存在？
```java
import java.util.Scanner;
public class Main {
	  public static void main(String[] args) {
		    // TODO Auto-generated method stub
		    Scanner in = new Scanner(System.in);
        int[] data = {3,2,5,7,4,9,11,34,12,28};
        int x = in.nextInt();
        int loc = -1;
        for(int i=0; i<data.length; ++i)
        {
            if(x == data[i])
            {
                loc = i;
                break;
            }
        }
        if(loc > -1)
        {
            System.out.println(x+"是第"+(loc+1)+“个”);
        }
        else
        {
            System.out.println(x+"不在其中");
        }
    }
}
```
以上是线性搜索
```Java
for(int i=0; i<data.length; ++i)
{
    if(x==data[i])
    {
        loc = i;
        break;
    }
}
```
*  通常都是使用 for 循环，让循环变量 i 从 0 到 < 数组的length，这样循环体内最大的 i 正好是数组最大的有效下标
*  常见错误是：
    +  循环结束条件是 <= 数组长度，或；
    +  离开循环后，继续用 i 的值来做数组元素的下标！

##### 遍历数组判断是否存在某个元素
*  **FOR-EACH 循环**
```java
import java.util.Scanner;
public class Main {
	  public static void main(String[] args) {
		    // TODO Auto-generated method stub
		    Scanner in = new Scanner(System.in);
        int[] data = {3,2,5,7,4,9,11,34,12,28};
        int x = in.nextInt();
        int loc = -1;
        boolean found = false;
        for(int i=0; i<data.length; ++i)
        {
            if(x == data[i])
            {
                loc = i;
                break;
            }
        }
        for(int k : data)
        {
            if(k == x)
            {
                found = true;
                break;
            }
        }
        if(loc > -1)
        {
            System.out.println(x+"是第"+(loc+1)+“个”);
        }
        else
        {
            System.out.println(x+"不在其中");
        }
    }
}
```
*  不能使用 FOR-EACH 改变数组中的值
```Java
for(int k : data)
{
    k = 0;
}
for(int k : data)
{
  System.out.println(k);
}
```
```Java
int[] data = {3,2,5,7,4,9,11,34,12,28};
int x = in.nextInt();
int loc = -1;
for(int i=0; i<data.length; ++i)
{
    if(x == data[i])
    {
        loc = i;
        break;
    }
}
if(loc > -1)
{
    System.out.println(x+"是第"+(loc+1)+“个”);
}
else
{
    System.out.println(x+"不在其中");
}
```
```Java
int[] data = {3,2,5,7,4,9,11,34,12,28};
int x = in.nextInt();
boolean found = false;
for(int k : data)
{
    if(k == x)
    {
        found = true;
        break;
    }
}
if(found)
{
    System.out.println(x+"在其中");
}
else
{
    System.out.println(x+"不在其中");
}
```

#####  for-each
for(<类型><变量>:<数组>)
{
    ...
}

#### 4.2.3 素数
```Java
int n = in.nexitInt();
boolean isPrime = true;
if(x == 1)
{
    isPrime = false;
}
for(int i=2; i<n; i++)
{
    if(n % i == 0)
    {
        isPrime = false;
        break;
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
```
*  从 2 到 x-1 测试是否可以整除
*  对于 n 要循环 n-1 遍
*  当 n 很大时就可以被看作是 n 遍

##### 改进一：去掉偶数后，从 3 到 x-1，每次加 2
```Java
if(x == 1 || x%2 == 0 && x != 2)
{
    isPrime = false;
}
else
{
    for(int i=3; i<x; i+=2)
    {
        if(x % i == 0)
        {
            isPrime = false;
            break;
        }
    }
}
```
*  如果 x 是偶数，返回不是素数
*  否则要循环(n-3)/2 + 遍
    *  当 n 很大时就是 n/2 遍

##### 无须到 x-1，到 sqrt(x) 就够了
```Java
for(int i=3; i<Math.sqrt(x); i+=2)
{
    if(x % i == 0)
    {
        isPrime = false;
        break;
    }
}
```
*  只需要循环 sqrt(x) 遍
*  从 n --> n/2 --> sqrt(n)

#####  判断是否能被已知的且 <x 的素数整除
*  构造前 50 个素数的表
```Java
public class Main {
	public static void main(String[] args) {
		int[] primes = new int[50];
		primes[0] = 2;
		int cnt = 1;  //  这个 cnt 表示目前数组素数的个数，以及下一素数要放得位置
		MAIN_LOOP:
		for(int x=3; cnt<50; ++x)
		{
			for(int i=0; i<cnt; i++)
			{
				if(x % primes[i] == 0)
				{
					continue MAIN_LOOP;
				}
			}
			primes[cnt++] = x;
		}
		for(int k: primes)
		{
			System.out.print(k+" ");
		}
		System.out.println();
	}
}
```
#####  构造素数表
*  欲构造 n 以内的素数表
1. 令 x 为 2
2. 将 2x、3x、4x直至 ax<n 的数标记为非素数
3. 令 x 为下一个没有被标记为非素数的数，重复 2；直到所有的数都已经尝试完毕

*  欲构造 n 以内（不含）的素数表
1. 创建 prime 为 boolean[n]，初始化其所有元素为 true，prime[x] 为 true 表示 x 是素数
2. 令 x = 2;
3. 如果 x 是素数，则对于(i=2; x*i<n; ++i) 令 prime[i*x]=false;
4. 令 x++，如果 x<n，重复3，否则结束。

```Java
public class Main {
	public static void main(String[] args) {
		boolean[] isPrime = new boolean[100];  //  初始化为0，表示false，需要修改成true
		for(int i=0; i<isPrime.length; ++i)
		{
			isPrime[i] = true;
		}
		for(int i=2; i<isPrime.length; ++i)
		{
			if(isPrime[i])
			{
				for(int k=2; i*k<isPrime.length;++k)
				{
					isPrime[i*k] = false;
				}
			}
		}

		for(int i=2; i<isPrime.length; ++i)
		{
			if(isPrime[i])
			{
				System.out.print(i+" ");
			}		
		}
	}
}
```
*  算法不一定和人的思考方式相同

### 4.3 二维数组
#### 4.3.1 二维数组
##### 二维数组
*  int[][] a = new int[3][5];
*  通常理解为a是一个 3 行 5 列的矩阵

<table>
   <tr>
      <td>a[0][0]</td>
      <td>a[0][1]</td>
      <td>a[0][2]</td>
      <td>a[0][3]</td>
      <td>a[0][4]</td>
   </tr>
   <tr>
       <td>a[1][0]</td>
       <td>a[1][1]</td>
       <td>a[1][2]</td>
       <td>a[1][3]</td>
       <td>a[1][4]</td>
   </tr>
   <tr>
       <td>a[2][0]</td>
       <td>a[2][1]</td>
       <td>a[2][2]</td>
       <td>a[2][3]</td>
       <td>a[2][4]</td>
   </tr>
</table>

#####  二维数组的遍历
```Java
for(i=0; i<3; ++i)
{
    for(j=0; j<5; ++j)
    {
        a[i][j] = i * j;
    }
}
```
*  a[i][j] 是一个 int
*  表示第 i 行第 j 列上的单元
    *  a[i,j] 并不存在

##### 二维数组的初始化
```
int[][] a ={
    {1,2,3,4},
    {1,2,3}}，
```
*  编译器来数数
*  每行一个 {}，逗号分隔
*  最后的逗号可以存在，有古老的传统
*  如果省略，表示补零

#####  tic-tac-toe 游戏
*  读入一个 3*3 的矩阵，矩阵中的数字为 1 表示该位置上有一个 X，为 0 表示 O
*  程序判断这个矩阵中是否有获胜的一方，输出表示获胜一方的字符 X 或 O，或输出无人获胜。
```Java
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		final int SIZE = 3;
		int[][] board = new int[SIZE][SIZE];
		boolean gotResult = false;
		int numOfX = 0;
		int numOfO = 0;

		//  读入矩阵
//		for(int i=0; i<SIZE; ++i)
//		{
//			for(int j=0; j<SIZE; ++j)
//			{
//				board[i][j] = in.nextInt();
//			}
//		}
		for(int i=0; i<board.length; ++i)
		{
			for(int j=0; j<board[i].length; ++j)
			{
				board[i][j] = in.nextInt();
			}
		}
		in.close();

		//  检查行

		//  检查列

		//  检查对角线

		//  检查反对角线
		if(!gotResult)
		{
			numOfX = 0;
			numOfO = 0;
			for(int i=0; i<SIZE; ++i)
			{
				if(board[i][SIZE-i-1] == 1)
				{
					numOfX ++;
				}
				else
				{
					numOfO ++;
				}
			}
			if(numOfX == SIZE || numOfO == SIZE)
			{
				gotResult = true;
			}
		}
		if(gotResult)
		{
			if(numOfX == SIZE)
			{
				//  X 赢了
			}
			else
			{
				//  O 赢了
			}
		}
		else
		{
			//  没人赢
		}
	}
}

```

## 第五章：函数
### 5.1 函数的定义和调用
#### 5.1.1 定义函数
#### 5.1.2 调用函数
### 5.2 函数的参数和本地变量
#### 5.2.1 参数传递
#### 5.2.2 本地变量
### 5.3 《函数》编程练习
#### 5.3.1 《函数》编程练习题

## 第六章 使用对象
### 6.1 字符类型
#### 6.1.1 字符类型
#### 6.1.2 逃逸字符
### 6.2 包裹类型
#### 6.2.1 包裹类型
### 6.3 字符串类型
#### 6.3.1 字符串变量
#### 6.3.2 字符串操作
### 6.4 Math类
#### 6.4.1 Math类
### 6.5 《使用对象》编程练习
#### 6.5.1 《使用对象》编程练习题
