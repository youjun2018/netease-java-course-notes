## 第二章：判断
### 2.1 作比较
#### 2.1.1 比较
![ticket-vending-machine](image/part1/ticket-vending-machine.png)
``` java
public class Main{
    public static void main(String[] args){
//        初始化
        Scanner in = new Scanner(System.in);
//        读入投币金额
        System.out.print("请投币：");
        int amount = in.nextInt();
//        打印车票
        System.out.println("*******************");
        System.out.println("* Java城际铁路专线 *");
        System.out.println("*   无指定座位票   *");
        System.out.println("*    票价：10元    *");
        System.out.println("*******************");
//        计算并打印找零
        System.out.println("找零：" + （amount-10));
    }
}
```
##### 注释
以两个斜杠"//"开头的语句把程序分成了四个部分：
1. 初始化
2. 读入投币金额
3. 打印车票
4. 计算并打印找零

添加比较
``` java
public class Main{
    public static void main(String[] args){
//        初始化
        Scanner in = new Scanner(System.in);
//        读入投币金额
        System.out.print("请投币：");
        int amount = in.nextInt();
        System.out.println(amount);
        System.out.println(amount >= 10);
//        打印车票
        System.out.println("*******************");
        System.out.println("* Java城际铁路专线 *");
        System.out.println("*   无指定座位票   *");
        System.out.println("*    票价：10元    *");
        System.out.println("*******************");
//        计算并打印找零
        System.out.println("找零：" + （amount-10));
    }
}
```

#### 2.1.2 关系运算
##### 关系运算
* 计算两个值之间的关系，所以叫做关系运算  

| 运算符       | 意义           |
|:-------------:|:---------:|
|==|相等|
|！=|不相等|
|>|大于|
|>=|大于或等于|
|<|小于|
|<=|小于或等于|

##### 优先级
**所有的关系运算符的优先级比算术运算的低，但是比赋值运算的高**
* 6 > 1
* 5 == 5
* 7 >= 3 + 4
</br>例如：7 >= 3 + 4，一定是先算3+4，然后和7比较；而不是先比较 7 >= 3，然后在和 4相加。

**判断是否相等的 == 和 ！= 的优先级比其他的低，而连续的关系运算是从左到右进行的**
* 5 > 3 == 6 > 4 </br>//先计算5>3和6>4，结果再和运算==
* 6 > 5 > 4  </br>//错误的语句，因为先比较 6>5，返回true，再和4比较，显然错
* a == b == true
* a == b == 6  </br>//错误的，先计算a==b，返回true或false，再和6计算，是错的
* a == b > false  </br>//错误的，优先级>大于==，所以先计算>。当b为整数或浮点数时，不能喝false比较；若b为true和false时，true和false无法比较，也是错的。
* (a == b) > false </br>//先做括号里面的，a==b 计算结果为true或false，是不能和false作比较的。

**int vs double?**
* int a = 5;
* double b = 5.0;
* System.out.println(a==b);
</br>//是可以的，可以作比较，结果为true

**double?**  
double a = 1.0;
double b = 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1;
System.out.println(a == b);
</br> //是可以作比较的，但是结果为false。因为，double类型的浮点数在计算机中是有误差的。这里b = 0.9999999999999999,a = 1.0，所以是不相等的。
</br> //所以比较两个浮点数不能使用 == 运算符，可以使用
* Math.abs(f1 - f2) < 0.00001
```Java
System.out.println(Math.abs(a-b) < 1e-6);
```
表示 a 和 b 的绝对值小于一个很小的数。

### 2.2 判断语句
#### 2.2.1 做判断
``` java
public class Main{
    public static void main(String[] args){
//        初始化
        Scanner in = new Scanner(System.in);
//        读入投币金额
        System.out.print("请投币：");
        int amount = in.nextInt();
        System.out.println(amount);
        System.out.println(amount >= 10);
        if(amount >= 10)
        {
//        打印车票
            System.out.println("*******************");
            System.out.println("* Java城际铁路专线 *");
            System.out.println("*   无指定座位票   *");
            System.out.println("*    票价：10元    *");
            System.out.println("*******************");
//        计算并打印找零
            System.out.println("找零：" + （amount-10));
        }
    }
}
```
##### if 语句
* 一个基本的 if语句由一个关键字if开头，跟上在括号里的一个表示条件的逻辑表达式，然后是一对大括号“{}”之间的若干条语句。如果表示条件的逻辑表达式的结果为true，那么就执行后面跟着的这对大括号中的语句，否则就跳过这些语句不执行，而继续下面的其他语句。
```Java
if ( total > amount)
    total += amount + 10;
```
if 语句这一行结束的时候并没有表示语句结束的";"，而后面的赋值语句写在 if 的下一行，并且缩进了，在这一行结束的时候有一个表示语句结束的";"。这表明这条赋值语句是 if 语句的一部分，if 语句拥有和控制这条赋值语句，决定它是否要被执行。

##### debug
在要调试的一行的右边双击，出现一个点，叫"Line breakpoint"，断点。程序运行到这一行会停下来。然后在上方运行的地方的左边“虫子”的地方点击运行。
在 debug 界面右上角有java的按钮点击，就可以回到原来的窗口。

##### 比较数的大小
```java
Scanner in = new Scanner(System.in);
int x = in.nextInt();
int y = in.nextInt();
int max;
if(x > y)
    max = x;
System.out.println(max);
```

##### if-else
``` java
Scanner in = new Scanner(System.in);
int x = in.nextInt();
int y = in.nextInt();
int max;
if(x > y)
    max = x;
else
    max = y;
System.out.println(max);
```

``` java
final double RATE = 8.25;
final int STANDARD = 40;
doble pay = 0.0;
Scanner in = new Scanner(System.in);
System.out.print("Enter the number of hours worked: ");
int hours = in.nextInt();
System.out.println();
if(hours > STANDARD)
    pay = STANDARD * RATE + (hours - STANDARD) * (RATE * 1.5);
else
    pay = hours * RATE;
System.out.println("Gross earnings: " + pay);
```

``` java
final double PASS = 8.25;
Scanner scan = new Scanner(System.in);
System.out.print("请输入成绩：");
int hours = scan.nextInt();
System.out.println("你输入的成绩是" + score);
if(score > PASS)
    System.out.println("很遗憾，这个成绩没有及格。");
else
    System.out.println("祝贺你，这个成绩及格了。");
System.out.println("再见");
```

``` java
final double PASS = 8.25;
Scanner scan = new Scanner(System.in);
System.out.print("请输入成绩：");
int hours = scan.nextInt();
System.out.println("你输入的成绩是" + score);
if(score > PASS)
    System.out.println("很遗憾，这个成绩没有及格。");
else
{
    System.out.println("祝贺你，这个成绩及格了。");
    System.out.println("再见");
}
```

#### 2.2.2 判断语句
#### 2.2.3 嵌套和级联的判断
##### 三个数比较大小
``` java
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        int x;
        int y;
        int z;
        System.out.println("请输入两个数：")；
        x = in.nextInt();
        y = in.nextInt();
        z = in.nextInt();
        in.close();
        int max = 0;
        if(x > y)
        {
            if(x > z)
            {
                max = x;
            }
            else
            {
                max = z;
            }
        }
        else
        {
            if(y > z)
            {
                max = y;
            }
            else
            {
                max = z;
            }
        }
        System.out.println(max);
    }
}
```
##### 嵌套的判断
* 当if的条件满足或者不满足的时候要执行的语句也可以是一条if或if-else语句，这就是嵌套的if语句
``` java
if(code == READY)
    if(count < 20)
        System.out.println("一切正常\n");
    else
        System.out.println("继续等待\n");
```

##### else 的匹配
* **else 总是和最近的那个 if 匹配**
* 若想和较远的if匹配，要把最近的if放到大括号中

##### tips
* 在 if 或 else 后面总是用 {}
* 即使只有一条语句的时候

##### 分段函数
```
//一个公式
f(x) = -1; x<0
        0; x=0;
       2x; x>0
```

```Java
// 级联的实现
if(x < 0){
    f = -1;
}else if(x == 0){
    f = 0;
}else{
    f = 2 * x;
}
```
不建议使用以下方式实现，常规是单一出口
```Java
// 级联的实现
if(x < 0){
    System.out.println(-1);
}else if(x == 0){
    System.out.println(0);
}else{
    System.out.println(2 * x);
}
```

#### 2.2.4 判断语句的常见问题
##### 忘了大括号
```Java
// 不管age是否大于60，都会输出“salay”
if(age > 60)
    salary = salary * 1.2;
    System.out.println(salay);
```
* 建议：永远在 if 和 else 后面加上大括号，即使当时后面只有一条语句

##### if 后面的分号
```Java
if(age > 60);
{
    System.out.println("A = B");
}  
```

##### 错误使用 == 和 =
* if 只要求()里的值是零或非零
```Java
if(a = b);
{
    salary = salary * 1.2;
    System.out.println(salay);
}  
```

##### 代码风格
* 在 if 和 else 之后必须加上大括号形成语句块；
* 大括号内的语句缩进一个 tab 的位置；

##### 风格是三观
* 最原始的一种
```Java
if(x < 0){
    f = -1;
}else if(x == 0){
    f = 0;
}else{
    f = 2 * x;
}
```
* 中间一种
```Java
if(x < 0)
{
    f = -1;
}else if(x == 0)
{
    f = 0;
}else
{
    f = 2 * x;
}
```

* **建议使用的一种，方便注释**
```Java
if(x < 0)
{
    f = -1;
}
else if(x == 0)
{
    f = 0;
}
else
{
    f = 2 * x;
}
```
* 在if和else之后必须加上大括号形成语句块；
* 大括号内的语句缩进一个tab的位置；

### 2.3 多路分支
#### 2.3.1 多路分支
##### switch-case
* 级联的if语句可以改写成 switch 语句。
```Java
if(type == 1)
    System.out.println("您好");
else if(type == 2)
    System.out.println("早安");
else if(type == 3)
    System.out.println("晚安");
else if(type == 4)
    System.out.println("晚安");
else
    System.out.println("啊，什么啊？");
```

```java
switch(type){
    case 1:
        System.out.println("您好");
        break;
    case 2:
        System.out.println("早上好");
        break;
    case 3:
        System.out.println("晚上好");
        break;
    case 4:
        System.out.println("再见");
        break;
    default:
        System.out.println("啊，什么啊？");
        break;
}
```

```java
switch-case
switch(控制表达式){
case 常量：
    语句
    ......
case 常量:
    语句
    ......
default:
    语句
    ......
}
```

* 控制表达式只能是整数型的结果
* 常量可以是常数，也可以是常数计算的表达式
* **根据表达式的结果，寻找匹配的 case，并执行 case 后面的语句，一直到 break 为止**
* 如果所有的 case 都不匹配，那么就执行 default 后面的语句；如果没有 default，那么就什么都不做

##### break
* swith 语句可以看做是一种基于计算的跳转，计算控制表达式的值后，程序会跳转到相匹配的 case （分支标号）处。分支标号只是说明 switch 内部位置的路标，在执行完分支中的最后一条语句后，如果后面没有break，就会顺序执行到
下面的 case 里去，直到遇到一个 break，或者 switch 结束为止。
