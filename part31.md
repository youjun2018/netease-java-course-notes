# Java 基础入门：容器、异常和IO

## 第一章：标准类库
### 1.1 Object类
#### 1.1.1 Object类

Java 实现一个单根结构，在 Java 中所有的类，不管声明不声明，这些类一定都是一个叫做 Object 的子类。这个 Object 就是 Java 系统当中的 root，那个根，所以这叫做单根结构。几乎所有的 OOP 语言都实现了单根结构。除了 C++。

**Object 类**

![objectClass](image/part3/objectClass.png)

在这个图当中，系统内部的类 String， 我们自己做的类 Person，Vehicle 它们都是继承自 Object。不用申明，默认就是 Object 的子类。我们讲继承是说，如果从某个类继承，那个类的所有的 public 的东西都是你的东西，Object 这个类给了我们什么东西呢，其实我们之前就遇到过两个：

* **toString()**
* **equals()**

Object 定义了一个 toString，我们怎么知道 Object 类有哪些函数是我们可以用的呢，有两种简单的方式。

创建一个 Object 的对象，然后使用点 **.** 运算符，就可以看到可以使用的函数。



```Java
Object o = new Object();
o.
/**
 * 主要有：
 * getClass():Class<?>
 * toString():String
 * equals(Object arg0):boolean
 * hashCode():int
 * notify():void
 * notifyAll():void
 * wait():void
 * wait(long arg0):void
 * wait(long arg0, int arg1):void
*/
```



这里重点说 toString()。它表示返回一个对象的字符串的表达形式。如果我们自己做的类没有 toString() 函数，但是用此类的对象去调用 toString() 函数会发生什么？例如在上次做的 CD 类的 main 函数里面。



```Java
public static void main(String[] args) {
  CD cd = new CD("a", "b", 2, 2, "...");
  cd.print();
  System.out.println(cd.toString());  //继承自 Object，所以可以调用
}//~
// output: dome.CD@e76cbf7
//~
```



输出的是 "dome.CD@e76cbf7" "@" 前面是类的名字，后面是类在内存中的地址。其实，如果一个类没有写 toString() 函数，但是需要一个字符串，可以直接用 cd，不需要加上 toString，编译器会知道在这里需要调用 toString，去把它转成 String。

如果说我用如下方式，用字符串 "aa" 加上一个对象 cd。这时编译器会找到一个方案去把非字符串的东西转换成字符串。对于一个对象来说，那个方案就是 toString。



```Java
public static void main(String[] args) {
  CD cd = new CD("a", "b", 2, 2, "...");
  cd.print();
  String s = "aa" + cd;
  System.out.println(s);
}
```



所以如果我们先用这种手段能够给我们产生一个有意义的、表达CD对象的字符串，我们就要自己去写一个 toString() 函数。怎么去写呢？

空白处 右键 --> Source --> Generate toString()... --> 然后弹出如下窗口

![generatorToString](image/part3/generatorToString.png)

让你选择把那些字段放到 toString 里面。它列出了自己的 artist, numofTracks。还可以点开 Inherited methods，包含其他的函数。如果点上 Inherited methods 中的 toString()，它会把 Item 中的 toString 也会包含进去。就会产生如下函数：



```Java
@Override
public String toString() {
    return "CD [artist=" + artist + ",numofTracks=" + numofTracks + ", toString()=" + super.toString() + "]";
} //~
// output：CD [artist=b, numofTracks=2, toString()=dome.CD@22998b08]
//~
```



还有一个我们之前见到过的有用的东西 equals。我们知道比较两个对象是否相同用 "==" 是比较不了的。"==" 只能比较这两个管理者是不是管理同样的对象，要比较对象是否相同要使用 "equals"。



```Java
public static void main(String[] args) {
    CD cd = new CD("a","b",2,2,"...");
    CD cd1 = new CD("a","b",2,2,"...");
    System.out.println(cd.equals(cd1));  // false  理由是没有做自己的 equals，用的是 Object 的 equals。Object 的 equals 只能判断这两个管理者是否管理同一个对象。仅此而已。
}
```



我们要写一个自己的 equals。同样的 source --> Override/Implement Methods。它做的事情是列出父类拥有的函数，并询问你要改写什么函数。选择 equals 函数。

![overrideImplementMethods](image/part3/overrideImplementMethods.png)

会返回以下函数，



```Java
@Override
public boolean equals(Object obj) {
    // TODO Auto-generated method stub
    return super.equals(obj);
}
```



改写后的函数如下：



```Java
@Override
public boolean equals(Object obj) {
    // TODO Auto-generated method stub
    CD cc = (CD)obj;  // 必须适用向下造型，这样 cc 表达的就是 CD，就可以用了。因为 equals 需要传输的参数是 Object 对象。
    return artist.equals(cc.artist);
} //~
// output: true
//~
```



还有一个问题，这里的 "@Override" 有什么作用？ 它告诉编译器下面的一行函数是覆盖了父类函数的函数。它必须和父类函数具有完全相同的函数签名或函数原型。即函数的名字、参数表必须一样，并且必须是 public。如果有一个不相同就会认为是错误的。



```Java
//@Override
public boolean equals(Object obj, int i) {
    // TODO Auto-generated method stub
    CD cc = (CD)obj;  // 必须适用向下造型，这样 cc 表达的就是 CD，就可以用了。因为 equals 需要传输的参数是 Object 对象。
    return artist.equals(cc.artist);
} //~
// output: false
//~
```



得到 false 的理由是什么？当我们在做 equals 时，根本没有进入到我们写的 equals 里面去，又回到了 Object 里面的 equals 了。因为去掉了 "@Override"，自己写的函数并不会去取代 Object 中的 equals。

### 1.2 包裹类
#### 1.2.1 类库和包裹类

这里主要讲 jdk 中系统类库中的类，有哪些类我们是可以去用的。C 语言有标准库，我们可以直接去用，例如 printf 等。Java 也有标准类库，和 C 的标准类库的区别在于，C 的标准类库是可以丢到的，是可以使用其他的类库来和 C 的编译器结合在一起的。但对于 Java 来说语言和编译器是紧密结合在一起的。接下来将详细讲解 String 类。String 类与语言、编译器结合的很紧密。Java 语言和类库是密不可分的。对于 Java 来说，我们需要知道什么东西来研究一个类。例如下面提到的：

##### **interface of a class**

* **name of the class**
* **general description of the purpose of the class**
* **a list of the class's ctors and methods**
* **the parameters and return types of each ctors(构造函数) and methods**
* **a description of the purpose of each ctor and method**

以上这些东西去哪里看呢？Java 提供了系统类库的文档，有一个很重要的包，叫做 Java.lang

##### **Java.lang**

* java.lang **is automatically imported into all programs. It is Java's most widely used package.**
* **Contains classes and interfaces that are fundamental to virtually all of Java programming.**
* **This package contains lots of classes and three interface.** Clonable, Runnable **and** Comparable.

Java.lang 是不需要 import 的，可以直接在程序里面用。包括 包裹类，比如说下面列出 Character Class 类的函数。

##### **the Character Class**

||
|-|
|static boolean isDigit(char ch) <br> Determines if the specified character is a digit.|
|static boolean isLetter(char ch) <br> Determines if the specified character is a letter.|
|static boolean isLetterOrDigit(char ch) <br> Determines if the specified character is a letter or a digit.|
|static boolean isLowerCase(char ch) <br> Determines if the specified character is a lowercase letter.|
|static boolean isUpperCase(char ch) <br> Determines if the specified character is an uppercase letter.|
|static boolean isWhitespace(char ch) <br> Determines if the specified character is whitespace (spaces and tabs).|
|static char toLowerCase(char ch) <br> Converts ch to its lowercase equivalent, if any. if not, ch is returned unchanged.|
|static char toUpperCase(char ch) <br> Converts ch to its uppercase equivalent, if any. if not, ch is returned unchanged.|

这些是对单个字符处理的函数，所以 Java 提供了这些函数。

##### **-128~127**

* For Short and Integer in the range of -128 to 127, and char in the range of \\u0000 to \\u007f, there are fixed value objects.
* true to
    * Integer.valueOf(3) == Integer.valueOf(3);
* false to
    * Integer.valueOf(129) == Integer.valueOf(129);

对于 Short 和 Integer 这两个类，它们的范围在 -128 到 127。char 的范围在 \\u0000 到 \\u007f 的范围，它们都是 **fixed value objects**。

也即，Integer.valueOf(3) == Integer.valueOf(3) 这个等式，会生成 **同一个对象**，因为 3 在 Integer 范围内。Integer.valueOf(129) == Integer.valueOf(129) 不相等，因为 129 不在 Integer 范围内，会生成两个对象。



前面说过包裹类型，包裹类型有很多函数可以直接用。

##### **TYPE Wrappers**

* Every Primitive data type has corresponding type wrapper
* **Long**
  - **Field Summary**
      static long MAX_VALUE = The largest value of type long.
          static long MIN_VALUE = The smallest value of type long.
      static ClassTYPE = The Class object representing the primitive type long.
  - **Constructor Summary**
      Long(long value) : Constructs a newly allocated Long object that represents the primitive long argument.
      Long(String s) : Constructs a newly allocated Long object that represents the value represented by the string in decimal form.
* **some methods of the class Long**
  - static <font color="blue">String</font> <font color="red">toHexString</font>(long i)  
      **Creates a string representation of the long argument as an unsigned integer in base 16.**
  - static <font color="blue">String</font> <font color="red">toOctalString</font>(long i)  
      **Creates a string representation of the long argument as an unsigned integer in base 8.**
  - static <font color="blue">long</font> <font color="red">parseLong</font>(String s)  
      **Parses the string argument as a signed decimal long.**
  - static <font color="blue">long</font> <font color="red">parseLong</font>(String s, int radix)  
      **Parses the string argument as a signed long in the radix specified by the second argument.**
  - static <font color="blue">long</font> <font color="red">valueOf</font>(String s)  
      **Returns a new long object initialized to the value of the specified String.**

在 1.7 以前，如果要比较两个包裹值是否相等，我们可以用 compareTo。String 我们刚才也看过。x.compareTo(y) 比较 x 与 y 是否相等。现在还有另外一种用法，Integer.compare(x, y)，能这样写意味着 compare 是 Integer 的静态函数。不需要制造 Integer 这个类的对象，就可以使用 Integer 这个类的静态对象来比较 x 和 y 这两个 Integer 是否相等。

##### **compare wraps**

* x.compareTo(y);
* Integer.compare(x, y);


#### 1.2.2 包裹类

到目前为止，我们见到了 Java 的四种基本的数据类型。从 boolean，它只能表达 true 和 false；字符；整数；浮点数。这四种类型都有对应的包裹类型。每一种基础类型都对应一种包裹类型。

##### **包裹类型**
* **每种基础类型都有对应的包裹类型**

|基础类型|包裹类型|
|---|---|
|boolean|Boolean|
|char|Character|
|int|Integer|
|double|Double|


包裹类型有什么用？包裹类型和基础类型一样都是类型，**可以使用包裹类型定义变量**。



```Java
int i = 10;
Integer k = 10;  //是可以的
k = i;  // 是可以的
```



包裹类型可以做一些特殊的事情。比如说，对于整数来说，我们可以从 Integer 类型得到一些有趣的信息。



```Java
System.our.println(Integer.MAX_VALUE);  // output: 2147483647
```



在数学中，整数的范围是(-&infin;, +&infin;)。但是在计算机中是使用二进制的数表示整数的。在计算机内部，对于 Java 来说，如果要表达一个 int 使用 4 个字节，也即 32bit。能表达的最大的整数是 $2^{31}-1$，最小的整数是 $-2^{31}$，其中还包括一个 0。这就是 Java 所能够表达的整数的范围。Integer.MAX_VALUE 也即 $2^{31}-1$。包裹类型有一些工具可以帮我们来做一些事情。例如获得最大值、最小值。

##### **包裹类型的用处**

* 获得该类型的最大最小值
    * Integer.MIN_VALUE
    * Integer.MAX_VALUE


##### **.运算符**

* 当需要让一个类或对象做事情的时候，用 . 运算符
    * a.length
    * Integer.MAX_VALUE


我们之前也遇到过，说数组.length 可以得到这个数组的大小。对于包裹类型也可以用点。在点的左边是一个对象或是一个类，在点的右边是这个对象或者类能提供给你的服务、或者数据、或者能做的动作。

对于 Character 这个类来说就有很多有意义的东西。

##### **Charact**

||
|-|
|static boolean isDigit(char ch) <br> 判断这个字符是不是数字|
|static boolean isLetter(char ch) <br> 判断这个字符是不是字母|
|static boolean isLetterOrDigit(char ch) <br> 判断这个字符是不是字母或数字|
|static boolean isLowerCase(char ch) <br> 判断这个字符是不是小写字母|
|static boolean isUpperCase(char ch) <br> 判断这个字符是不是大写字母|
|static boolean isWhitespace(char ch) <br> 判断这个字符是不是一种空格|
|static char toLowerCase(char ch) <br> 把这个字符转换成小写|
|static char toUpperCase(char ch) <br>把这个字符转换成大写|



```Java
System.out.println(Character.isLowerCase('a'));  // output: true
```



善用 Java 类库提供的这些东西，比如包裹类型等等。这些提供的工具可以帮助做很多事情。


### 1.3 String类
#### 1.3.1 String的构造

String 类的包是 java.lang，类名是 String。String 里面是一串字符，所以叫字符串。

##### **String Handing**

* String is sequence of characters
* In Java, String is an **immutable(不可修改) object**  // 不可修改，就是没有提供任何手段去修改那个对象
* Immutable : Strings within objects of type **String** are unchangeable means that the contents of the **String** instance cannot be changed after it has been created.
* However, a variable declared as a **String** reference can be changed to point at some other **String** object at any time.

什么叫做修改一个对象？比方说，一个对象有一个函数 setColor，你调用这个函数就把 color 变成另外一种颜色了，如果这样的话，这个对象就是 mutable 的，可以修改的。如果这个对象没有任何函数去做这个事情，除了在构造的时候给他一个颜色之外，以后只能 getColor。如果想要另外一个颜色的话，只能再造一个新的对象。那个时候我们就说这个类的对象是 immutable 的，而 String 就是这样一种 immutable 的东西。

String 类的对象不能改变，所以它里面的内容一旦被创建出来就不能被改变了。但是一个被声明 String 类型的变量可以指向其他的 String 的对象。所以当对这个变零赋值的时候，要考虑其实发生的是什么。

去构造一个 String 有几种手段:

##### **String constructors**

* **Following default constructor cteates an instance of string with no character in it.**



```java
String s = new String();
```



* **To create a String initialized by an array of characters, use the constructor shown here:**



```java
String(char chars[]);
char chars[] = {'a', 'b', 'c'};
String s = new String(chars);
```



* **Specify a subrange of a character array as an initializer using the following constructor:**



```Java
String(char chars[], int startIndex, int numChars)
```



    - startIndex **specifies the index at which the subrange begins, and numChars specifies the number of characters to use.**



```Java
char chars[] = {'a', 'b', 'c', 'd', 'e', 'f'};
String s = new String(chars, 2, 3);
```



* This initializes **S** with the characters **cde**.



String s = new String() 会创建一个空的字符串，不能向里面加任何东西，一直到抛弃它为止，它都是空的。其实不是抛弃他，抛弃需要动作。只是放到内存中不用它，最后被垃圾处理机制处理。

C 中的字符串有一个专有的名字，叫 C 字符串；其他语言的字符串就叫字符串。 C 的字符串截尾有一个零；其他语言的字符串截尾没有零，是使用一个表示字符串长度的变量来表示字符长度。

一个 bit 的数组和 char 的数组在 Java 中有什么区别？一个是字节，一个是字符。字符有两个字节。你把一个 bit 的数组变成 String 有很多种做法，要么把连续的两个字节当做一个字符，要么它设法把单个字节的东西变成一个字符。把单个字节的东西变成一个字符会遇到很多问题。

#### 1.3.2 String常用函数

##### **String APIs**
```Java
String s1 = "Hello";
s1.length();  // gives the length of string
int age = 25;
String s2="I am" + age + "years young";
```



##### **String Operations**

* **equals()** - Compares the invoking(调用) string to the specified object. The result is true if and only if the argument is not null and is a String object that represents the same sequence of characters as the invoking object.



```Java
public boolean equals(Object anObject)
```



* **equalsIgnoreCase()** - Compares this String to another String, ignoring case considerations. Two strings are considered equal ignoring case if they are of the same length, and corresponding characters in the two strings are equal ignoring case.



```Java
public boolean equalsIgnoreCase(String anotherString)
```



##### **.intern()**

```Java
"Hello" == "Hello";
new String("Hello") == "Hello";
(new String("Hello").intern() == "Hello");
```









#### 1.3.3 理解String是不可写的对象



#### 1.3.4 String的格式化和转换







### 1.4 StringBuffer类
#### 1.4.1 StringBuffer类

### 1.5 其他常用类
#### 1.5.1 Math类
#### 1.5.2 Random类
#### 1.5.3 日期与时间




































endof part31
