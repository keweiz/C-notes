#  第六章 回顾数据类型和表达式

[TOC]

## 6.1 数据的存储

计算机处理的所有信息都以二进制形式表示，数据的**存储**和**计算**都用二进制表示。

### 整型

-   为方便计算，数值一般用**补码**表示
-   符号位：最左边一位（最高位）是符号位，`0`为正，`1`为负
-   正数：**原码 反码 补码**相同，都是`0`为符号位，其余各位表示数值
-   负数：
    -   原码：符号位是`1`，其余各位表示数值
    -   反码：符号位是`1`，其余各位对原码**取反**
    -   补码：**反码** `+1` 
-   根据存储空间大小，`int`型一般为2-4 Byte

### 实型

-   分为**符号位 阶码 尾数**三部分
-   `-1.2345e+02`中，`-`占符号位，`+02`占阶码位，`1.2345`占尾数位

### 字符型

-   每个字符在内存中占一个byte，存放其对应的ASCLL码，即转化为整数存储



## 6.2 基本数据类型

C语言的三种基本数据类型为整型、实型、字符型，整型包括`int(4)  short(2)  long(4)  unsigned(4)  unsigned short(2)  unsigned long(4)` ，字符型包括`char(1)` ，实型包括`float(4)  double(8)` 

### 整型与整型常量

-   整型：
    -   不存在小数部分的数据类型
    -   除了`int`型，还有扩展的整型`short  long  unsigned  unsigned short  unsigned long` 
    -   有符号数的最高位是**符号位**，其余各位表示数值，无符号数的全部存储单元都用于表示数值
    -   规定：`short`型不长于`int`型，`long`型不短于`int`型
-   整型常量（即整数）
    -   在各种类型合法表示范围内的数都是合法的整型常量
    -   任何一个整数都有三种表示：**十进制  八进制(0)  十六进制(0x)** 
    -   整数类型：
        -   有后缀字母时：`u/U`表示 `unsigned`型，`l/L`表示`long`型，`lu/LU`表示`long unsigned`型
        -   无后缀字母时：根据整数的范围确定其类型，非负整数可以看做相应的`unsigned`型
### 字符型与字符型常量

-   字符型：
    -   字符以`ASCLL`码存储，因此字符型有明显的**数值特征**，可以用整数表示字符
    -   `A`的ASCLL码为`65` ，`ch = 'A'`与`ch = 65`等价（前提ch为字符变量）
    -   字符型变量的值可以是字符或整数，整型变量的值可以是字符型数据，可以被定义成字符型变量。
    -   在有效的`ASCLL`码范围内，整形变量和字符型变量的**定义**和**值**都可以互相交换
-   字符型常量：
    -   一对单引号及其括起来的字符
    -   `'0'`和`0`分别为字符型常量和整型常量
    -   运算：字符型常量可以像整数一样参与运算：`'A' + 1 = 66` ，对应字符`'B'` 
    -   转义字符：**形式上多个字符，实际只代表一个字符** 
        -   特殊操作：既不能在屏幕显示，也无法用键盘输入 `\n`换行，`\t`制表符/横向跳格，`\\`反斜杠，`\"`双引号，`\'`单引号
        -   不同进制表示：`\102`表示ASCLL码中八进制数102对应的字符，即`'B'`， `\x41`表示ASCLL码中十六进制数41对应的字符，即`'A'` 
        -   ASCLL字符集中的所有字符都可以用**转义字符**表示

### 实型与实型常量

-   实型：
    -   又称**浮点型**，指存在小数部分的数
    -   `float`型和`double`型在**数据的精度**和**取值范围**不同，`double`型精度高，取值范围大
    -   `float`：有效位数`7~8`位，取值范围$$±(10^{-38} - 10 ^{38})$$ 
    -   `double`：有效位数`15~16`位，取值范围$±(10^{-308} - 10^{308})$ 
    -   **数值精度** 和**取值范围**是两个概念，`1234567.89`在`float`型取值范围内，但它的有效数字超过了8位，如果赋值给`float`，则会变为`1234567.80`，最后一个是一个随机数字，损失了有效数字，降低了精度
    -   **实数在计算机中只能近似表示，运算中也会产生误差**
-   实型常量（实数）
    -   表示法：**十进制浮点表示法**和**科学计数法**
    -   浮点表示法：小数点的前后至少一边要有数字，又称为实数的**小数形式**
    -   科学计数法：字符`e/E`为指数标志，在`e/E`之前要有数字，之后必须是整数，又称为实数的**指数形式**



## 6.3 数据的输入和输出

### 整型

-   调用函数`scanf()  printf()` 实现整型数据的输入和输出
-   格式控制说明

| 数据类型            | 十进制  | 八进制  | 十六进制 |
| --------------- | ---- | ---- | ---- |
| `int`           | %d   | %o   | %x   |
| `long`          | %ld  | %lo  | %lx  |
| `unsigned`      | %u   | %o   | %x   |
| `unsigned long` | %lu  | %lo  | %lx  |

-   输出格式控制说明中可以加**宽度限定词**，指定输出宽度。`%md`：指定数据输出宽度为`m`位（包括符号位），若小于，左端补空格，若大于，按实际位数输出

### 实型

-   实型的**输入**和**输出**控制说明不同
-   `scanf()`：

| float  | %f   | 小数形式输入一个单精度浮点数  |
| ------ | ---- | --------------- |
| float  | %e   | 指数形式 输入一个单精度浮点数 |
| double | %lf  | 小数形式输入一个双精度浮点数  |
| double | %le  | 指数形式 输入一个双精度浮点数 |

-   `printf()`：`float double`共用格式控制字符`%f  %e` 

| float/double | %f   | 小数形式输出浮点数（默认6位小数）         |
| ------------ | ---- | ------------------------- |
| float/double | %e   | 指数形式输出浮点数（小数点前有且仅有以为非0数字） |

-   输出格式控制说明中可以加宽度限定词：`%m. nf ` 表示浮点数输出宽度为`m`（包括符号位和小数点），有`n`位小数
-   数据实际位数小于`m`，则左端用空格补齐，大于则按实际位数输出

### 字符型

-   `scanf()  getchar()` 用于输入，`getchar()`只能处理单个字符
-   `printf()  putchar()`用于输出，`putchar()`只能处理单个字符
-   `scanf()  printf()`输入输出字符时，格式控制说明`%c`表示单个字符，`%s`表示字符串
-   **特别地**：`scanf()`在`Visual Studio`中被认为不安全，是因为输入时可能出现越界，因此使用`scanf_s()`函数，输入字符串时，`scanf_s("%s",&ch,m)`，字符变量`ch`最多输入`m`个字符
-   输入多个字符时，字符间不能有间隔，因为`' '`也是一个合法字符
-   与字符在程序中的表示不同，输入和输出时，字符两侧没有单引号`''`
-   **与整数互相转换**： 字符型数据既可以按照字符形式输出，也可以按照整数形式输出，可以调用`printf("%d",ch)`直接输出字符型变量`ch`对应的ASCLL码
-   **字符运算**： `ch-'a'+'A'`可以将小写字母转化为大写字母，`ch-'0'`可以把数字字符转化为数字



## 6.4 类型转换

不同类型数据可以混合运算，但要先转化为同一类型。

### 自动类型转换

#### 非赋值运算

-   水平方向：`char  short`自动转化为`int` ，`unsigned short`转换为`unsigned` ， `long`转化为`unsigned long`，所有`float`转化为`double` 
-   垂直方向：水平方向转化后类型仍不相同，再将数据自动转换为更高级别：`int`  `->` `unsigned`  `->` ` unsigned long` `->`  `double` 

#### 赋值运算

-   赋值号右侧表达式的类型自动转换成赋值号左侧变量的类型
-   如果**右侧**数据类型比左侧类型高，运算精度会降低

### 强制类型转换

一般形式为：` (DataType) expression`

```c
int i;
(double) i; /*将int型i强制转换为double型
```

-   不论是**自动类型转换**还是**强制类型转换**都是为了满足当前语句运算需要，并没有改变其在内存中的存储状态，即数据本身没有改变。
-   **强制类型转换符**是**运算符**，与**自增 自减**运算符有相同优先级



## 6.5 表达式

-   常量、变量、函数是最简单的表达式
-   **运算符**和**运算对象**所组成的有意义的运算式子称为**表达式**
-   运算符：具有运算功能的符号
-   运算对象：常量、变量、函数等表达式

### 6.5.1 算数表达式

-   算数运算符
    -   单目运算符：`++ --  +  -`  自增  自减  正  负
    -   双目运算符：`+  -  *  /  %` 加 减 乘  除  取余
-   自增运算符/自减运算符
    -   自增/自减运算符只能对**变量**使用

```c
int n = 5;
++n; 
/* 变量 n=6, 表达式 n++ = 6 */

n++;
/* 变量 n=6, 表达式 ++n = 5 */
```

-   优先级和结合性

| 运算符种类 | 运算符                          |   结合方向    |
| :---: | ---------------------------- | :-------: |
| 逻辑运算符 | `!`                          | 从右向左（右结合） |
| 算数运算符 | `++` `--` `+` `-` `*`  单目    |           |
|       | `*`  `/`  `% `  双目           | 从左向右（左结合） |
|       | `+` `-`  双目                  |           |
| 关系运算符 | `<` `<=` `>` `>=`            |           |
|       | `==` `!=`                    |           |
| 逻辑运算符 | `&&`                         |           |
| 逻辑运算符 | `||`                         |           |
| 条件运算符 | `?:`                         | 从右向左（右结合） |
| 赋值运算符 | `=` `+=` `-=` `*=` `/=` `%=` |           |
| 逗号运算符 | `,`                          | 从左向右（左结合） |

-   算数表达式：用算数运算符把运算对象连接起来的表达式
-   **副作用说明**
    -   自增和自减运算要谨慎使用，尤其在构造复杂表达式时，应尽量避免
    -   根据运算符**优先级**和**结核性**决定运算顺序，但对两侧操作对象的求值顺序并未作出明确规定，`f()+g()` ，可以先求`f()`也可以先求`g()` 

### 6.5.2 赋值表达式

-   赋值号左侧必须是一个变量，将赋值号右侧**表达式的值**赋给左侧变量
-   一般形式：`variable = expression` 
-   运算过程：
    -   计算赋值号右侧**`表达式的值`**
    -   将**`表达式的值`**赋给**`变量`**
    -   将**`变量的值`**作为**`赋值表达式的值`** 
-   类型转换：第二步时先右侧**`表达式`**的值，再将其类型自动转换为**`变量`** 的类型

```c
double x;
x = 10/4;
/*先计算10/4，其值为2，再自动转换类型为2.0,即此时x=2.0*/
x = 1.0*10/4;
/*计算右侧时，int型自动垂直转换为float型，结果为2.5，然后赋值给x,x=2.5*/
```

-   连续赋值：`x=y=3` 与 `x=(y=3)` 等价
    -   第一个表达式计算过程：赋值号为右结合，则先计算`y=3`，此时变量`y`的值为`3`，表达式`y=3`的值也是`3`，再将表达式的值赋给`x`

### 6.5.3 关系表达式

-   关系运算符优先级低于算数运算符，高于赋值运算符，结合方向左结合
-   **关系表达式**的值是一个**`逻辑量`**：真`1`，假`0` 不同于`R语言`中的真`True`和 假`Flase`
-   关系表达式的值为整型
-   连续关系比较

```c
if(3 <= x <=5){
  ...
}
/*该表达式无法表示数学区间[3,5]，因为关系运算符为左结合，则 3<=x 不论为 1 还是 0 ,都小于 5 ，表达式整体值始终为 1 */
```

### 6.5.4 逻辑表达式

-   逻辑运算对象：逻辑量 和 关系表达式
-   逻辑表达式运算结果：也是一个逻辑量
-   **逻辑量**为非零，就是`真`
-   `!`：为单目运算符，优先级最高
-   `&&` `||`：为双目运算符，优先级低于  关系表达式
-   **特殊**提前结束运算：求解用`&&` `||`连接的逻辑表达式时，一旦能得出结果，立刻终止
    -   `exp1 && exp2`中，左结合先计算exp1,若结果为`0`，提前结束运算，逻辑表达式的值一定为`0`

### 6.5.5 条件表达式

-   条件运算符为**三目运算符**
-   一般形式：`exp1 ? exp2 : exp3` 
-   运算过程：先计算`exp1`的值，若为真，将`exp2`的值作为条件表达式的值，若为假，将`exp3`的值作为条件表达式的值
-   运算优先级：低于 逻辑运算符 ，高于 赋值运算符

```c
z = (a > b) ? a : b;
/*等价于下式*/
if(a > b)
  z = a;
else
  z = b;
```

### 6.5.6 逗号表达式

-   `,` 既可以用作**分隔符**，也可以用作**运算符**，作运算符时优先级最低
-   一般形式：`exp1, exp2, ... ,expn` 
-   运算过程：先计算`exp1`的值，再计算`exp2`的值，最后计算`expn`的值，并将`expn`的值作为**逗号表达式的值**
-   常用于`for()`循环

```c
/*逗号作分隔符*/
int a,b,c; //用于分隔不同变量
printf("%d",x); //用于分隔函数的不同参数

/*运算符*/
a = 1, b = 2, c = a + b; //结合顺序从左向右，最后算得c的值
//优先级最低，无需括号
```

### 6.5.7 位运算（未完成）



### 6.5.8 其他运算

-   长度运算符 `sizeof()` 
    -   单目运算符
    -   用于返回变量或数据类型的字节长度，单位`Byte`
-   特殊运算符
    -   `()`：改变运算顺序
    -   `[]`：表示数值元素
    -   `*` `&` ：指针运算
    -   `->` `.` ：表示结构分量
