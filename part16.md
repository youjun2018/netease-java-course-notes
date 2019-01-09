## 第六章 使用对象
### 6.1 字符类型
#### 6.1.1 字符类型
#####  字符类型
*  单个的字符是一种特殊的类型：char
    *  用单引号表示的字符字面量：'a', '1'
    *  Java 使用 Unicode 来表示字符，可以表达包括汉子在内的多种文字

#####  字符计算
```Java
char c = 'A';
c++;
System.out.println(c);  //65

int i = 'Z' - 'A';
System.out.println(i);  //25
```

##### 大小写转换
*  字母和数字在 Unicode 表中是顺序排列的
    *  '0'、'1'、...
*  大写字母和小写字母是分开排列的，并不在一起

#####  字符大小
*  字符可以被比较大小，依据是它们在 Unicode 表中的编号
  *  '0' --> '9'
  *  'A' --> 'Z'
  *  'a' --> 'z'
  *  'Z' < 'a'

#### 6.1.2 逃逸字符
#####  逃逸字符
*  用来表达无法打印出来的控制字符或特殊字符，它由一个反斜杠"\\"开头，后面跟上另一个字符，这两个字符合起来，组成了一个字符
<table>
  <tr>
    <th>字符</th>
    <th>意义</th>
    <th>字符</th>
    <th>意义</th>
  </tr>
  <tr>
    <th>\b</th>
    <th>回退一格</th>
    <th>\"</th>
    <th>双引号</th>
  </tr>
  <tr>
    <th>\t</th>
    <th>到下一个表格位</th>
    <th>\'</th>
    <th>单引号</th>
  </tr>
  <tr>
    <th>\n</th>
    <th>换行</th>
    <th>\\</th>
    <th>反斜杠本身</th>
  </tr>
  <tr>
    <th>\r</th>
    <th>回车</th>
    <th></th>
    <th></th>
  </tr>
</table>
#####  制表位
*  每行的固定位置
*  一个 \t 使得输出从下一个制表位开始
*  用 \t 才能使得上下两行对齐

### 6.2 包裹类型
#### 6.2.1 包裹类型
#####  包裹类型
*  每种基础类型都有对应的包裹类型
<table>
  <tr>
    <th>基础类型</th>
    <th>包裹类型</th>
  </tr>
  <tr>
    <th>boolean</th>
    <th>Boolean</th>
  </tr>
  <tr>
    <th>char</th>
    <th>Character</th>
  </tr>
  <tr>
    <th>int</th>
    <th>Integer</th>
  </tr>
  <tr>
    <th>double</th>
    <th>Double</th>
  </tr>
</table>
*  包裹类型和基础类型一样，都是类型。包裹类型可以用来定义变量
*  包裹类型可以做一些特殊的事情，

#####  包裹类型的用处
*  获得该类型的最大最小值
  *  Integer.MIN_VALUE
  *  Integer.MAX_VALUE

#####  .运算符
*  当需要让一个类或对象做事情的时候，用.运算符
  *  a.length
  *  Integer.MAX_VALUE

#####  Character
<table>
<tr>
  <th>static boolean isDigit(char ch)</th>
  <th>判断这个字符是不是数字</th>
</tr>
  <tr>
    <th>static boolean isLetter(char ch)</th>
    <th>判断这个字符是不是字母</th>
  </tr>
  <tr>
    <th>static boolean isLetterOrDigit(char ch)</th>
    <th>判断这个字符是不是字母或数字</th>
  </tr>
  <tr>
    <th>static boolean isLowerCase(char ch)</th>
    <th>判断这个字符是不是小写字母</th>
  </tr>
  <tr>
    <th>static boolean isUpperCase(char ch)</th>
    <th>判断这个字符是不是大写字母</th>
  </tr>
  <tr>
    <th>static boolean isWhitespace(char ch)</th>
    <th>判断这个字符是不是一种空格</th>
  </tr>
  <tr>
    <th>static char toLowerCase(char ch)</th>
    <th>把这个字符转换成小写</th>
  </tr>
  <tr>
    <th>static char toUpperCase(char ch)</th>
    <th></th>
  </tr>
</table>

### 6.3 字符串类型
#### 6.3.1 字符串变量
#####  字符串
*  用双引号括起来的 0 个或多个字符就是一个字符串字面量
  *  "hello"
  *  "1"
  *  ""

#####  字符串变量
*  String s;
*  String 是一个类，String 的变量是对象的管理者而非所有者
    *  就像数组变量是数组的管理者而非所有者一样
*  String 的第一个字母是大写的。包裹类型的第一个字母也是大写的。

#####  new = 创建
```Java
String s = new String("a string");
```
*  创建了一个 String 的对象
*  用"a string"初始化这个对象
*  创建管理这个对象的变量 s
*  让 s 管理这个对象

#####  初始化字符串变量
*  String s = "hello";
*  编译器帮你创建一个 String 类型的对象交给 s 来管理

#####  字符串连接
*  用加号 (+) 可以连接两个字符串
    *  "hello"+"world" --> "helloworld"
*  当这个+的一边是字符串而另一边不是时，会将另一边表达为字符串然后做连接
    *  "I'm " + 18 --> "I’m 180"
    *  1 + 2 + "age" --> "3 age"
    *  "age" + 1 + 2 --> "age12"

#####  输入字符串
*  in.next(); 读入一个单词，单词的标志是空格
    *  空格包括空格、tab 和 换行
*  in.nextLine(); 读入一整行

#####  对象变量的赋值
*  前面说过，字符串变量和数组变量一样，它是字符串的管理者而不是所有者，所以很多事情和基础类型不一样。比如说赋值，对于基础类型来说，如果有一个 int a，一个 int b。我们要把 a 的值 赋给 b，我们做 b = a；因为它们都有自己的存储空间，实际发生的是 b 得到了 a 里面的值。这是两个独立的变量。
*  但对于两个字符串变量字符串 a 和 字符串 b，做 b = a这样的赋值，实际上是b和a共同管理了 a 所管理的字符串。
![duixiangfuzhi](image/part1/duixiangfuzhi.png)

#####  比较两个 String
```Java
if(input == "bye"){          //  比较是否同一个
    ...
}

if(input.equals("bye")){     //  比较内容是否相同
    ...
}
```
*  Strings 应该用 .equals 来比较

#####  同一个还是相同
![person1_person2](image/part1/person1_person2.png)

*  == 比较是否同一个
*  equals 比较内容是否相同

#### 6.3.2 字符串操作
#####  字符串操作
*  字符串是对象，对它的所有操作都是通过"."这个运算符来进行的
    *  字符串.操作
*  它表示对.左边的这个字符串做右边的那个操作
*  这里的字符串可以是变量也可以是常量

#####  Strings 大小的比较
*  两个字符串可以比较大小：
```Java
s1.compareTo(s2)
```
如果 s1 比 s2 小，那么结果是负的；如果 s1 和 s2 相等，那么结果是 0；如果 s1 比 s2 大，那么结果是正的
*  compareToIgnoreCase 可以不区分大小写地来比较大小

#####  获得 String 的长度
*  用 length() 函数
```java
String name = "Hellola",
Str1 = "one",
str2 = "",
str3;

name.length();  -->  7
str1.length();  -->  3
str2.length();  -->  0
str3.length();  -->  Error!  //  因为str3没有管理任何String对象
```

#####  访问 String 里的字符
*  s.charAt(index)
    *  返回在 index 上的单个字符
    *  index 的范围是 0 到 length() - 1
    *  第一个字符的 index 是 0，和数组一样
*  但是不能用 for-each 循环来遍历字符串

#####  得到子串
*  s.substring(n)
    *  得到从 n 号位置到末尾的全部内容
*  s.substring(b,e)
    *  得到从 b 号位置到 e 号位置之前的内容

#####  寻找字符
*  s.indexOf(c)
    *  得到 c 字符所在的位置，-1 表示不存在
*  s.indexOf(c, n)
    *  从 n 号位置开始寻找 c 字符
*  s.indexOf(t)
    *  找到字符串 t 所在的位置
*  从右边开始找
    *  s.lastIndexOf(c)
    *  s.lastIndexOf(c, n)
    *  s.lastIndexOf(t)

#####  其他 String 操作
*  s.startsWith(t)  //  以 t 开头的
*  s.endsWith(t)    //  以 t 结尾的
*  s.trim()         //  把字符串两边的空格删除掉
*  s.replace(c1, c2)  //  把字符串中所有的 c1 换成 c2
*  s.toLowerCase()  //  把字符串中所有字符转化成小写字符
*  s.toUpperCase()  //  把字符串中所有字符转化成大写字符

#####  不可变的 String
*  所有的字符串都是不可变的，对它们的操作的结果都是制造新的字符串出来
```Java
String s = "abc";
System.out.println(s.toUpperCase());
System.out.prinln(s)
```

#####  在 switch-case 中使用字符串
```Java
switch(s){
    case "this":...break;
    case "that":...break;
}
```
*  1.7 版本以上才可以使用

### 6.4 Math类
#### 6.4.1 Math类
#####  Math
*  是 java 系统内部提供的一个类，提供一些基本的数学操作。
*  abs  //  算绝对值
*  pow  //  幂次
*  random  //  返回随机数
*  round  //  四舍五入


### 6.5 《使用对象》编
