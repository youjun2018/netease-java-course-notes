# Java 基础入门：入门篇（试学）
## 第一章：用程序来做计算
### 1.1 第一个Java程序
#### 1.1.1 准备编程软件
##### 1.1.1.1 Window 下如何安装 Eclipse  
1. 登录到 Eclipse.org 官网。  
注：下载软件要培养的习惯：1）下载软件要到官网去下，会下到最新的和最纯净的；2） 要适应阅读英文的网站和文献，它们使用的主要是常用单词，不会太难。
2. 在右上角点击 DOWNLOAD 按钮，然后在打开的界面中选择 Eclipse IDE for Java Developers（最新版的是Eclipse IDE 2018-12）。网站更新，界面可能不一样。最后显示捐赠页面，可以根据自己的情况选择捐赠或者不捐。
3. 下载的安装包是 eclipse-inst-win64.exe。双击，打开安装界面，如下图。单击选择 Eclipse IDE for Java Developers。并选择安装路径，这里选择默认。然后接受协议。点击安装，等待安装完成。
![eclipse-installer-1](image/part1/eclipse-installer-1.png)
![eclipse-installer-2](image/part1/eclipse-installer-2.png)
![Eclipse-Foundation-Software-User-Agreement](image/part1/Eclipse-Foundation-Software-User-Agreement.png)
![eclipse-installer-4](image/part1/eclipse-installer-4.png)
4. 安装完成打开界面如下。
![eclipse](image/part1/eclipse.png)
如果没出现 Package Explorer，可以按如下图调出 Package Explorer。
![package-explorer](image/part1/package-explorer.jpg)
5. 如果需要下载 JRE 的话，到官网 www.oracle.com 下载 JRE。

#### 1.1.2 Mac OS 上的编程软件
##### 1.1.2.1 Mac 如何安装 Eclipse
1. 在浏览器中输入网址 eclipse.org，打开官网。
2. 点击 DOWNLOAD 按钮，进行下载。注意官网的提示。
3. 按照提示默认安装就行。

#### 1.1.3 第一个 Java 程序
##### 1.1.3.1 写一个 Java 程序
1. File --> New --> Java Project，这里 project name 输入hello。可以设置其他选项，这里直接 Finish。
2. 在左边的 Package Explorer 下可以看到新建的 hello 项目。然后在 hello 项目下的 src 文件夹中可以写入代码。右键点击 src，选择 New --> Class，新建一个类。这里其他选项可以默认，Name 栏输入 Hello。**类的名字一般都会大写**。并且在下面勾选 public static void main(String[] args)，如下图
![ecplice-new-class](image/part1/ecplice-new-class.png)
3. 在 main 函数中输入代码，**例如输入 System，只需要输入 Sys，然后 alt + / 就会弹出提示框。** 选择需要的选项，可以双击，也可以箭头加回车。
4. 输入代码 System.out.println("hello world")，使用 alt + /来进行提示。类的名称前有星号*，表示文件还没有保存，ctrl + s 进行保存。
5. 如何运行程序？在左上角有一个 run 按钮，点击即可运行。  
![run-button](image/part1/run-button.png)
6. 中间的是编辑区域，是写源代码的地方；左边的是 Package Exploere，展式工程的内容；下面有不同的页，其中有一个业叫 Console，这个页就是程序运行的地方。
![ecplise-interface](image/part1/ecplise-interface.png)
7. 如果在代码行左边出现红色的×，表示这一行有错误。鼠标放在上面，会提示错误信息。
8. 在双引号中间可以出现中文，但是在双引号外面不要出现中文信息。注释也最好使用英文。

### 1.2 用变量做计算
#### 1.2.1 输入
1. 首先创建输入 Scanner in = new Scanner(System.in); 使用 alt + / 进行提示。
2. 再输入 System.out.println(in.nextLine()); 然后在 Console 页面点击，使光标聚焦在 Console 页面。
3. 输入hello，并按回车，会显示 hello。
![run-and-stop](image/part1/run-and-stop.png)
4. 如果多次运行同一个程序，并且程序没有关闭，会出现如下情况。
![run-two-program](image/part1/run-two-program.png)
初学者很容易犯得一个错误就是程序有输入，程序等待用户输入的过程中，程序还没有运行结束，用户因为运行结束，就又开启一个程序。每一次启动一个程序就会有很多资源要被使用q 去运行你的程序，当程序运行的越来越多，最后你的 Eclipse 就运行跑不动了。当运行程序后没有反应时，可以到这里来看看是不是运行太多程序。
5. 可以使用“+”连接两个字符串，如果不是字符串，也会自动把内容变成字符串。
6. 由于运算的优先级，有些计算需要使用括号来保证运算顺序。

#### 1.2.2 变量
使用用户输入的数字来进行计算。
![variable](image/part1/variable.png)
![variable-definition](image/part1/variable-definition.png)
![Java-Reserved-Words](image/part1/Java-Reserved-Words.png)
![variable-type](image/part1/variable-type.png)

#### 1.2.3 赋值
![assignment](image/part1/assignment.png)
![variables-and-constants](image/part1/variables-and-constants.png)

### 1.3 表达式（浮点数、优先级和类型转换）
#### 1.3.1 浮点数
1. 任何程序都必须要有输入、计算、以及输出。可能计算需要的时间很长久。
![height](image/part1/height.png)
2. 若想知道自己输入是否有错，可以把输入打印出来。
3. 整型与整型的运算结果只能是整型。**可以使用 double 表示浮点型**。
![int-int](image/part1/int-int.png)
![int-float](image/part1/int-float.png)
![float](image/part1/float.png)
![float-2](image/part1/float-2.png)
![float-3](image/part1/float-3.png)
![float-4](image/part1/float-4.png)

#### 1.3.2 优先级
1. java 运算符优先级就是正常的思维，怎么想的就怎么写。
![operator](image/part1/operator.png)
![monocular-operator](image/part1/monocular-operator.png)
![combination-relationship](image/part1/combination-relationship.png)

#### 1.3.3 类型转换
1. 强制类型转换
![mandatory-type-relationship](image/part1/mandatory-type-relationship.png)
![mandatory-type-relationship-2](image/part1/mandatory-type-relationship-2.png)

### 1.4 如何做编程作业
#### 1.4.1 如何交作业
![submit-homework-1](image/part1/submit-homework-1.png)
![submit-homework-2](image/part1/submit-homework-2.png)
![submit-homework-3](image/part1/submit-homework-3.png)

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






## 第三章：循环
### 3.1 循环（while和do-while循环）
#### 3.1.1 循环
#### 3.1.2 数数字
#### 3.1.3 while循环
#### 3.1.4 do-while循环
### 3.2 for循环
#### 3.2.1 for循环
#### 3.2.2 复合赋值
### 3.3 循环控制（含复合赋值、逻辑类型）
#### 3.3.1 循环控制
#### 3.3.2 多重循环
#### 3.3.3 逻辑类型
### 3.4 循环应用
#### 3.4.1 计数循环
#### 3.4.2 算平均数
#### 3.4.3 猜数游戏
#### 3.4.4 整数分解
#### 3.4.5 求和
#### 3.4.6 最大公约数
### 3.5 《循环》编程练习
#### 3.5.1 《循环》编程练习题

## 第四章：数组
### 4.1 数组的创建和使用
#### 4.1.1 初试数组
#### 4.1.2 创建数组
#### 4.1.3 数组的元素
#### 4.1.4 投票统计
### 4.2 数组变量和运算
#### 4.2.1 数组变量
#### 4.2.2 遍历数组
#### 4.2.3 素数
### 4.3 二维数组
#### 4.3.1 二维数组
### 4.4 《数组》编程练习
#### 4.4.1《数组》编程练习题

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
