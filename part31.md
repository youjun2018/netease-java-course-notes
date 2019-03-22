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
#### 1.2.2 包裹类














### 1.3 String类
#### 1.3.1 String的构造
#### 1.3.2 String常用函数
#### 1.3.3 理解String是不可写的对象
#### 1.3.4 String的格式化和转换

### 1.4 StringBuffer类
#### 1.4.1 StringBuffer类

### 1.5 其他常用类
#### 1.5.1 Math类
#### 1.5.2 Random类
#### 1.5.3 日期与时间




































endof part31
