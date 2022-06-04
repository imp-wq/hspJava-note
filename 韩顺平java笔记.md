## Java基本信息

### Java的跨平台特性

* 依赖JVM，java virtual machine，java虚拟机来实现，不同的操作系统有不同的JVM。包含在JDK中。
* 实现了“一次编译，到处运行”
  * javac进行编译
  * JVM进行运行

### JDK与JRE

* JDK，Java Development Kit，java开发工具包，包含JRE和java开发工具
* JRE，java Runtime Environment，java运行环境，包含JVM和Java核心类库。运行java只需要安装JRE即可。

### 安装

* 安装jdk即可，可以选择包含公共jre，供开发软件使用

* 安装路径不要有中文或空格
* 设置环境变量
  * 我的电脑->属性->高级系统设置->高级->环境变量
  * 编辑Path变量，新建一个`%JAVA_HOME%\bin`

### Hello World

* 文件名要和类名一致

* 有中文时注意编码（设置成GBK）。通过控制台右键->属性可以查看控制台的编码。

* 控制台通过`javac 类名.java`编译文件

  通过`java 类名`运行文件，注意不要带.class后缀

* `.java`源代码文件称为源文件，编译后的`.class`成为字节码文件。

* java程序的入口是main方法，固定写法

  `public static void main(String[] args){...}`

* 输出使用`System.out.println()`方法

* 一个源文件中最多只能有一个public类，其他类不限。编译后每个类都对应一个.class文件

* 如果源文件包含一个public类，则文件名必须按该类名来命名。

* 其他类中也可以有自己的main方法，有了main方法后，编译后每个类也可以单独运行

### 学习一门新技术

* 先学习新技术的基本原理和基本语法，先不要考虑细节
* 快速入门案例（基本程序）
* 开始研究技术的注意事项，使用细节、规范，如何优化（没有尽头的）

### 转义字符

同c++

* 回车`\r`与 换行`\n`不一样，回车会让光标回到行首，覆盖输出。

### 文档注释

​	可以用@指定特定的javadoc标签，可以被javadoc解析成网页形式。

​	对于类、方法的注释，用文档注释。

```java
/**
* @author xxx
* @version 1.0
*/
```

### DOS命令

* `tree 路径`展示目录树

### +号的使用

同JS，+两边都是数值时，执行加法。当左右两边有一边为字符串时，将另一边也转换成字符串，进行字符串拼接操作。

* 只有字符串才会让+执行拼接操作，如果是字符（char）则会转换成对应的unicode码，视为整数，进行加法运算。

### 数据类型

* 基本数据类型

  * 数值类型
    * 整数类型
      * byte byte=1 -128~127
      * short byte=2 -32768~32767
      * int byte=4
      * long byte=8
    * 浮点类型
      * float 单精度 byte=4
      * double 双精度 byte=8
  * 字符类型char byte=2 0-65535的unicode码
  * 布尔型boolean byte=1

* 引用数据类型

  * 类class
  * 接口interface
  * 数组[]

#### 整型

* java中的整形常量默认为int类型，声明long类型常量需要后加L或l
* 不能将long型赋值给int，比如`int n1 = 1L//错误写法`

#### 浮点数

* 浮点数的构成：

  符号位+指数位+尾数位

  尾数部分有可能丢失，造成精度损失，小数都是近似值。

* Java的浮点型常量（具体数）默认为double型，声明float型常量，需要后面加f或F

  也可以用`0.53d`,`3d`这样的方式表示double类型的常量

  不能将双精度double类型的变量赋值给单精度float，会造成精度损失，比如

  **通常情况下，不知道精度时，使用double类型**

  `float num1 = 1.1;//错误写法`

  `float num2 = 1.1f;//正确写法`

  但是可以将单精度值赋给双精度

  `double num3 = 1.1f;//可以`

* 浮点数的表示方法

  * 十进制数

    `5.12` `512.0f` `.512//0.xxx的0可以省略`

  * 科学记数法

    `5.12e2` `5.12E-2`

* 注意：同js，不要对运算后得到的浮点数进行相等判断，因为会有精度误差！

  ```java
  double num1 = 2.7;
  double num2 = 8.1;
  //错误写法
  if( num2/num1 == 3 ){
      System.out.println("相等");
  }
  ```

  

  比如8.1/3，得不到精确的2.7 

  解决方案：比较两数之差的绝对值和某个精度范围

  ```java
  //正确写法
  if( Math.abs(num2/num1 - 3) < 0.000001 ){
      System.out.println("差值小于精度，认为相等");
  }
  ```

#### 字符型

* char

* 本质是存储了一个整数，字符对应的unicode码。可以视为整数参与运算。

#### 布尔型

* boolean，只允许true和false
* **不可以用整数带代替**，这点与C和js不一样。 

#### 数据类型转换

* 基本数据类型转换

  java在进行赋值或运算时，精度小的类型会自动转换为精度大的类型

  char->int->long->float->double

  byte->short->int->long->float->double

  * 有多种类型的数据混合运算时，系统首先将所有数据转换成容量最大的数据类型，然后计算。

  * 将精度大的数据赋值给精度小的数据，会报错。

    将精度小的数据赋值给精度大的数据，会进行自动类型转换。

  * 把常量赋值给byte/short时，比如`byte b1 = 10;`会先判断常量是否在byte范围内，如果是就可以赋值。此时不涉及类型转换问题。

  * byte、short和char之间不会互相转换。（不能直接互相赋值）

    这三者互相可以进行计算，计算时精度会提升到**int**类型（即使是同类型之间的计算）。

    char可以保存int常量的值，不能保存int变量的值。

    ```java
    byte b1 = 10;
    char c = b1;//错误写法，不能将byte赋值给char
    short s2 = 1;
    int s2 = b1 + s1;//正确，此处必须用int型变量接收结果，不能用short，因为byte和short的运算结果为int类型。
    byte b2 = 1;
    int b4 = b1 + b2;//正确，byte与byte运算的结果仍然是int
    ```

    :star:在byte、short和char与复合赋值运算符`++`、`+=`使用时，会进行类型转换

    ```java
    byte b = 1;
    b++;//等价于b = (byte)(b+1);
    b += 2;//等价于b = (byte)(b+2);
    ```

    

  * boolean类型不参与转换。

* 强制类型转换

  将容量大的数据转换成容量小的数据，可能造成精度降低或溢出。

#### 基本数据类型与String的转换

整体上类似js

* 基本数据类型->String：`基本数据类型+"";`

* String->基本数据类型：调用基本数据类型对应的包装类的相应方法 `类型.parsexxx(字符串);`

  ```java
  		String s1 = "123";
  		int num1 = Integer.parseInt(s1);
  		double num2 = Double.parseDouble(s1);
  		float num3 = Float.parseFloat(s1);
  		Long num4 = Long.parseLong(s1);
  		byte num5 = Byte.parseByte(s1);
  		boolean b = Boolean.parseBoolean("true");
  		short num6 = Short.parseShort(s1);
  ```

* 如果String转换成基本数据类型时，格式不正确无法转换，就会抛出异常，程序终止。



### JAVA文档

* 在线文档[在线API中文手册 - 码工具 (matools.com)](https://www.matools.com/api)

### 运算符

#### 算数运算符

* 关于除法的易错点

  `double d = 10/4;`d为2.0 先计算10/4，都为int型，结果为2（int类型），将其转换为double类型赋值给d，得到2.0

* 取模运算%

  本质是`a % b = a - a / b * b`，尤其是在处理a或b中有负数的情况！

  对于有a为小数的情况，`a % b = a - (int)a / b * b`，但需要注意，小数运算结果有可能为近似值！

* 关于自增运算符++

  ```java
  int i = 1;
  i = i++;//会使用临时变量temp来保存i的值：(1)temp = i;(2)i = i + 1;(3)i = temp;
  		//在i完成自增后temp的值会覆盖掉自增后的结果，因此i为1
  System.out.println(i);//最后输出为1
  ```

  ```java
  int i = 1;
  i = ++i;//会使用临时变量temp来保存i的值：(1)i = i + 1;(2)temp = i;(3)i = temp;i为2
  System.out.println(i);//最后输出为2
  ```

#### 关系运算符

大体上跟c++一样，多了一个`instanceof`检查是否是类的对象。

* 关系表达式：关系运算符组成的表达式

* 关系表达式的结果一定是布尔值，true或false

* 短路与&&/逻辑与&，短路或||/逻辑或|

  这与c++的按位与/或和逻辑与/或是不一样的，类似js的逻辑短路。

  * &&短路与：如果第一个条件为false，后面的条件不会判断
  * &逻辑与：如果第一个条件为false，后面的条件仍然会判断

  

  * ||短路或：如果第一个条件为true，后面的条件不会判断
  * |逻辑或：如果第一个条件为true，后面的条件仍然会判断

  开发基本都用短路或和短路与，效率比较高。

### 命名规范

* 包名：全部小写
* 类名、接口名：大坨峰
* 变量名、方法名：小驼峰
* 常量名：所有字母大写，多个单词下划线连接

### 键盘输入语句

* 导入java.util包的Scanner类 `import java.util.Scanner;`

* 创建Scanner对象　｀Scanner scanner = new Scanner(System.in);｀］

* 用`scanner.next()`方法接收用户输入

  ```java
  String name = scanner.next();// 接收用户输入的字符串
  int age = scanner.nextInt();// 接收用户输入的int
  double salary = scanner.nextDouble();// 接收用户输入的double
  ```

### 进制

对于整数，有4种表示方式：

* 二进制：以`0b`或`0B`开头 `int n1 = 0b1010;`
* 十进制
* 八进制：以数字0开头 `int n3 = 01010;`

* 十六进制：以0x或0X开头，A-F不区分大小写 `int n4 = 0x10101;` 

### 位运算

* java没有无符号数，所有数都是有符号的，最高位为符号位
* 正数原码反码补码三码合一
* 负数反码为符号位不变，其他位取反，补码为反码+1
* 计算机在运行时，以补码的方式运算；在看运算结果时，要看原码

逻辑运算符：

* &：按位与
* |：按位或
* ^：按位异或
* ~：按位取反



* `>>`：算数右移，低位溢出，符号位不变，用符号位补高位。右移一位相当于除以2一次。
* `<<`：算数左移，符号位不变，低位补0。左移一位相当于乘2一次。
* `>>>`：逻辑右移/无符号右移，低位溢出，高位补0
* 没有`<<<`符号

### 分支+循环

* if-else

* switch

  * switch表达式的数据类型，应该与case后的常量一致，或者是可以**自动转换**成可以互相比较的类型。

    switch表达式应该是这些数据类型：

    byte,short,int,char,enum,String

    不能是double、float等

  * case子句中必须是常量，不能是变量

* for：

  * 循环条件必须返回一个**布尔**值

  * 初始化和变量迭代可以写到其他地方，但分号不能省略`for(;循环条件;)`

    ```java
    // 作用：扩大i的作用域
    int i = 1;
    for(; i <= 10 ;){
        /*循环体*/
        i++;
    }
    ```

  * 可以有多条循环初始化语句/循环迭代语句，中间用逗号隔开

* break
  * break语句出现在多层嵌套语句块时，可以通过**标签**指明终止哪一层语句块。
    * 实际开发中尽量不要使用标签（可读性差）
    * 没有指定标签时，默认退出最近的循环体

### 一些字符串的方法

* 取字符串的第x（索引，整型）个字符 `char c = String.charAt(x);`

* 字符串比较 `String1.equals(String2);`比较String1和String2是否完全一致。

  * 推荐将String1的位置放常量字符串，String2的位置放变量字符串，以避免空指针的问题

    `"abc".equals(String);
