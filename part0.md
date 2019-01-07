# 常用 Java 代码段
## 输入
Scanner in = new Scanner(System.in);
使用 ctr + / 进行代码提示

使用方向键移动到要操作的行，然后按住 shift 键，再按向下方向键，选中多行。最后使用 Ctrl + / 进行注释

System.out.print()  //输出不带回车
System.out.println()  //输出带回车

在需要高亮的代码块的前一行及后一行使用三个反引号“`” ，同时第一行反引号后面表面代码块所使用的语言

``` c++
#include<iostream>
using namespace std;
int main(){
    cout<<"hello world";
    return 0;
}
```

无序列表
无序列表使用星号* 加号+ 减号- 作为列表标记，在标记符号与文本直接应加入空格 或 Tab  

有序列表则使用数字接着一个英文句点1. 2.，在标记符号与文本直接应加入空格 或 Tab
在列表标记上使用的数字并不会影响输出的 HTML 结果


表格

| Tables       | Are           | Cool |
|:-------------  |  :---------:| ----:|
| 靠左对齐   | 居中对齐  | 靠右对齐     |
| 书写时      | 原始文字     |  可以不用对整齐 |
*斜体*      | **加粗**     | `渲染效果`
冒号: 在第二行中不同的位置表示对齐方式，在无冒号：的情况下默认靠左对齐
标题元件(表头)至少需要3个---来分隔
最外面的竖线|可以省略，书写的时候也可以不必需让原始的文字对得很整齐

至少有表头和对齐方式

一般表格的处理
http://www.ituring.com.cn/article/3452
https://blog.csdn.net/tuxingchen6/article/details/55222951


半方大的空白&ensp;或&#8194;
全方大的空白&emsp;或&#8195;
不断行的空白格&nbsp;或&#160;

删除线
~~您好~~

&nbsp; 空格（去掉空格）
</br>回车（去掉空格）

数学公式
https://blog.csdn.net/katherine_hsr/article/details/79179622
别忘了加$，并且要留有空格
上标 $21^{31} - 1$
下标 $21_{31} - 1$

markdown 如何插入公式
https://atom-china.org/t/atom-markdown/1099/2
Atom china

atom 左侧文件夹怎么打开
在打开文件的选项卡上单击右键，在弹出的菜单中点击"Reveal in Tree View" 就可以了

列表缩进：
* + - 不同级最好用不同的列表符好，同级最好用相同的列表符号
在不同级的一行打印两个 tab 或者 4个 space
