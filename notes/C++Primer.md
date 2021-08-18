# 第二章 变量和基本类型
## 2.1 基本内置类型
### 2.1.1 算术类型
算术类型的尺寸再不同机器上不同。下表是C++标准规定的尺寸的最小值。
| 类型 | 含义 | 最小尺寸 | 备注 |
| :--: | :--: | :--: | :--: |
| `bool` | 布尔类型 | 未定义 |  |
| `char` | 字符 | 8位 | 一个`char`的大小和一个机器字节一样 |
| `wchar_t` | 宽字符 | 16位 | 拓展字符集 |
| `char16_t` | Unicode字符 | 16位 | 拓展字符集（Unicode） |
| `char32_t` | Unicode字符 | 32位 | 拓展字符集（Unicode） |
| `short` | 短整型 | 16位 |  |
| `int` | 整型 | 16位 |  |
| `long` | 长整型 | 32位 |  |
| `long long` | 长整型 | 64位 |  | 
| `float` | 单精度浮点数 | 6位有效数字 |  |
| `double` | 双精度浮点数 | 10位有效数字 |  |
| `long double` | 拓展精度浮点数 | 10位有效数字 |  |


#### 带符号类型和无符号类型
除去布尔型和扩展的字符型之外，其他整型可以划分为 **带符号的** 和 **无符号的** 两种，从而可以表示正数、负数或0。  

类型 `int`、`short`、`long` 和 `long long` 都是带符号的，无符号类型需再类型名前加上 `unsigned`。类型 `unsigned int` 可以缩写成 `unsigned`。  

字符型有三种类型：`char`、`signed char`、`unsigned char`。类型 `char` 实际上会表现为上述两种形式中的一种（由编译器决定）。


### 2.1.2 字面值常量
#### 2.1.2.1 整型和浮点型字面值

#### 2.1.2.2 字符和字符串字面量  
由单引号括起来的一个字符称为`char`型字面量，双引号括起来的零个或多个字符则构成字符串型字面量。

#### 2.1.2.3 转义序列  
| 符号 | 含义 |
| :-: | :-: |
| `\n` | 换行符 |
| `\t` | 横向制表符 |
| `\a` | 报警（响铃）符 |
| `\v` | 纵向制表符 || `\b` | 退格符 |
| `\"` | 双引号 |
| `\\` | 反斜线 |
| `\?` | 问号 |
| `\'` | 单引号符 |
| `\r` | 回车符 |
| `\f` | 进纸（转页）符 |

> 泛化的转义序列  
其形式是`\x`后紧跟一个或多个十六进制数字，或者`\`后紧跟一个、两个或三个八进制数字，其中数字部分表示的是字符对应的数值。  
如：`\7（响铃）`、`\40（空格）`、`\115（字符M）`
需注意的是如果反斜线`\`后面跟着的八进制数字超过3个，只有前3个数字与`\`构成转义序列。

#### 2.1.2.4 指定字面量的类型
通过添加前缀和后缀，可以改变整型、浮点型和字符型字面量的默认类型。
- 字符和字符串字面值  
  | 前缀 | 含义 | 类型 |
  | :-: | :-: | :-: |
  | `u` | `Unicode`16字符 | `char16_t` |
  | `U` | `Unicode`32字符 | `char32_t` |
  | `L` | 宽字符 | `wchar_t` |
  | `u8` | `UTF-8`(仅用于字符串字面常量) | char |

- 整型字面值
  | 后缀 | 最小匹配类型 |
  | :-: | :-: |
  | `u/U` | `unsigned` |
  | `l/L` | `long` |
  | `ll/LL` | `long long` | 

- 浮点型字面值
  | 后缀 | 类型 |
  | `f/F` | `float` |
  | `l/L` | `long double` |


## 2.2 变量
### 2.2.1 列表初始化
用花括号来初始化变量的形式被称为 **列表初始化**。例如`int sold = {0}`和`int sold{0}`。  

当用于内置类型的变量时，如果我们使用列表初始化存在丢失信息的风险时，编译器将报错：
```c++
long double ld = 3.1415926536;
int a{ld}, b = {ld};//error
int c(ld), d = ld;//works
```
上述情况，使用`long double`的值初始化`int`变量时可能丢失数据，所以编译器拒绝了`a`和`b`的初始化请求。

### 2.2.2 变量声明和定义的关系
**声明** 使得名字为程序所知，一个文件如果想使用别处定义的名字必须包含对那个名字的声明。  
**定义** 负责创建与名字关联的实体。  
变量声明规定了变量的类型和名字，定义也一样。但是定义还能申请存储空间，也可能会为变量赋一个初始值。  
如果想声明一个变量而非定义它，就在变量名前添加关键字`extern`，而且不要显示地初始化变量：
```c++
extern int i; //declaration
int j; //definition
extern double pi = 3.14159; //defintion
```
在函数体内部，如果试图初始化一个由`extern`关键字标记的变量，将会引发错误。
> !!!变量能且只能被定义依次，但是可以被多次声明。

### 2.2.3 标识符
注意保留字

### 2.2.4 名字的作用域
- 全局作用域
- 块作用域
- 嵌套作用域：内层作用域、外层作用域


## 2.3 复合类型
**复合类型** 是指基于其他类型定义的类型。  

### 2.3.1 引用
**引用** 为对象起了另外一个名字，引用类型引用另外一种类型，通过声明符写成`&d`的形式来定义引用类型，其中`d`是声明的变量名。需注意的是 **①引用必须初始化，且初始值必须是一个匹配的对象** ！ **②使用与初始值是绑定在一起的，可理解为该变量的别名** 。 **③一位引用本身不是一个对象，所以不能定义引用的引用** 。
```c++
int ival = 1024;
int &refVal = ival;
int &refVal2; //error
```

### 2.3.2 指针
**指针** 是“指向”另外一种类型的复合类型。指针有以下特点：
- 指针本身就是一个对象，允许对指针赋值和拷贝，而且在指针的声明周期内它可以先后指向几个不同的对象
- 指针无需在定义时赋初值。  

定义指针类型的方法将声明符写成`*d` 的形式，其中`d`是变量名。如果在一条语句中定义了几个指针变量，每个变量前面都必须有符号`*`。

#### 2.3.2.1 获取对象的指针
指针存放某个对象的地址，获取该地址需要使用 **取地址符（操作符`&`）**

#### 2.3.2.2 指针值
指针的值（即地址）应属下面4种状态之一：
1. 指向一个对象
2. 指向紧邻对象所占空间的下一个位置
3. 空指针，意味着指针没有指向任何对象
4. 无效指针（上述情况外的其他值）

#### 2.3.2.3 利用指针访问对象
如果指针指向了一个对象，则可以使用 **解引用符（操作符`*`）** 来访问对象

#### 2.3.2.4 空指针
空指针不指向任何对象。下面是生成空指针的几种方法：
```c++
int *p1 = nullptr;//recommand
int *p2 = 0;//需要 #include <cstdlib>
int *p3 = NULL;
```
#### 2.3.2.5 赋值和指针
给指针赋值就是令它存放一个新的地址，从而指向一个新的对象。

#### 2.3.2.6 void* 指针
`void*`是一种特殊的指针类型，可用于存放 **任意对象** 的地址。一个`void*`指针存放着一个地址，但对于该地址中的对象是什么类型并不了解。所以不能直接操作`void*`指针所指的对象，没法访问内存空间中所存的对象。  
利用`void*`指针的事情比较有限：
- 与其他指针比较
- 作为函数的输入或输出
- 赋给另一个`void*`指针


### 2.3.3 理解符合类型的声明
#### 2.3.3.1 定义多个变量
涉及到指针或引用的声明，一般有两种写法。
- 把修饰符和变量标识符写在一起。这种形式着重强调变量具有的复合类型。  
  `int *p1, *p2;`
- 把修饰符和类型名写在一起，并且每条语句只定义一个变量。这种形式着重强调本次声明只定义了一种复合类型。  
  ```c++
  int* p1;
  int* p2;
  ```

#### 2.3.3.2 指向指针的指针
通过`*`的个数可以区分指针的级别。

#### 2.3.3.3 指向指针的引用
面对一条比较复杂的指针或引用的声明语句，从右向左阅读有助于弄清楚它的真实含义。（离变量名最近的符号对变量的类型有最直接的影响。）


## 2.4 const 限定符
关键字`const`对变量的类型进行限定可以使该变量的值不能被改变。因为`const`对象一旦创建后其值就不能再改变，所以`const`对象必须初始化。

默认情况下，`const`对象仅在文件内有效。如果想要`const`变量再文件间共享，则可以通过添加关键字`extern`来实现。

### 2.4.1 const 的引用
可以把引用绑定到`const`对象上（对常量的引用），对常量的引用不能用作修改它绑定的对象。

#### 2.4.1.1 初始化和对 const 的引用
一般情况下，引用的类型必须与其所引用的对象的类型一致，但是有两个例外。第一种例外情况就是： **在初始化变量引用时允许用任意表达式作为初始值，只要该表达式的结果能转换成引用的类型即可。** 尤其，允许一个常量引用绑定非常量的对象、字面值，甚至是个一般表达式：
```c++
double dval = 3.14;
const int &ri = dval;
```
编译器执行上述代码时，会产生一个临时量对象来处理类型转换。
```c++
const int temp = dval;
const int &ri = temp;
```

#### 2.4.1.2 对 const 的引用可能引用一个并非const的对象
常量引用仅对引用可参与的操作做出了限定，对于引用的对象本身是不是一个常量未作限定。因为对象也可能是个非常量，所以允许通过其他途径改变它的值。

### 2.4.2 指针和 const
**指向常量的指针** 不能用于改变其所指对象的值。想要存放常量对象的地址，只能使用指向常量的指针。但指向常量的指针仅仅要求不能通过该指针改变对象的值，而没有规定那个对象的值不能通过其他途径改变。

一般情况下，指针的类型必须与其所指对象的类型一致，但是有两个例外。第一种例外情况是 **允许令一个指向常量的指针指向一个非常量对象**。

#### 2.4.2.1 const 指针
`const pointer`必须初始化，一旦初始化完成，则它的值（存放在指针中的地址）就不能改变了。把`*`放在`const`关键字之前用以说说明指针是一个常量，这样的书写形式意味着，不变的是指针本身的值而非指向的那个值。


### 2.4.3 顶层 const
**顶层`const`** 表示指针本身是个变量，**底层`const`** 表示指针所指的对象是一个常量。  
一般地来说，**顶层`const`** 可以表示任意的对象是常量，而 **底层`const`** 则与指针和引用等复合类型的基本类型部分有关。比较特殊的是，指针类型既可以是顶层`const`也可以是底层`const`。
```c++
int i = 0;
int *const p1 = &i;//顶层const,指针指向的内存地址不能改变，但是其内容可以改变
const int ci = 42;//顶层const，不能改变ci的值
const int *p2 = &ci;//底层const，指针指向的内容不可改变，但可以改变指针的指向
const int *const p3 = p2;//靠右的const是顶层const，靠左的是底层const，指针指向的内存地址和指针指向的内容均不可改变
const int &r = ci;//用于声明引用的const都是底层const
```
> ？？？粗浅的理解：底层`const`使指向的对象的内容不能改变，顶层`const`使对象本身不能改变？

当执行对象的拷贝操作时，常量是顶层`const`还是底层`const`区别明显，顶层`const`不受影响，而对于底层`const`来说，拷入和拷出的对象必须 **具有相同的底层`const`资格** ，或者两个对象的数据类型必须能够转换。一般来说，非常量可以转换成常量，反之则不行。
```c++
int *p = p3;//error，p3包含底层const的定义，而p没有
p2 = p3;//works，p2和p3都是底层const
p2 = &i;//works，int*能转化成const int*
int &i = ci;//error，普通的int&不能绑定到int常量上
const int &r2 = i;//works，const int&可以绑定到一个普通的int上
```

### 2.4.4 constexpr 和常量表达式
**常量表达式** 是指值不会改变并且在编译过程就能得到计算结果的表达式。

#### 2.4.4.1 constexpr 常量
c++新标准规定，允许将变量声明为`constexpr`类型以便由编译器来验证变量的值是否是一个常量表达式。声明为`constexpr`的变量一定是一个常量，而且必须用常量表达式初始化。

#### 2.4.4.2 字面值类型
一些类型比较简单，值也显而易见、容易得到，就把它们称为"字面值类型"。算术类型、引用和指针都属于字面值类型。

指针和引用定义成`constexpr`的初始值收到严格限制。一个`constexpr`指针的初始值必须是`nullptr`或者`0`，或者是存储于某个固定地址中的对象（`constexpr`引用）。

#### 2.4.4.3 指针和`constexpr`
在`constexpr`声明中定义了一个指针，限定符`constexpr`仅对指针有效，与指针所指的的对象无关，`constexpr`把它所定义的对象置为了顶层`const`：
```c++
const int *p = nullptr; //p是一个指向整型常量的指针
constexpr int *q = nullptr; //p是一个指向整数的常量指针
```
与其他指针类似，`constexpr`指针既可以指向常量也可以指向一个非常量。


## 2.5 处理类型
### 2.5.1 类型别名
类型别名是一个名字，它是某种类型的同义词。适用类型别名可以让复杂的类型名字简单化，易于理解和使用。有两种方法可以定义类型别名：
- 使用关键字`typedef`  
  ```c++
  typedef double wages; //wages是double的同义词
  typedef wages base, *p; //base是都变了的同义词，p是 double* 的同义词
  ```

- 使用 **别名声明** 来定义类型的别名（c++新标准）  
  这种方法用关键字`using`作为别名声明的开始，其后紧跟别名和等号，其作用是把等号左侧的名字规定成右侧类型的别名。
  ```c++
  using SI = Sales_item; //SI是Sales_item的同义词
  ```

#### 2.5.1.1 指针、常量和类型别名
如果某个类型别名指代的是符合类型或常量，那么把它用到声明语句里可能会产生歧义，例如：
```c++
typedef char *pstring;
const pstring cstr = 0;//cstr是指向char的常量指针
const pstring *ps;//ps是一个指针，它的对象是指向char的常量指针
```
应该整体理解别名而不是带入重写语句进行理解！！！

### 2.5.2 auto 类型说明符
c++新标准引入了`auto`类型说明符，用它能让编译器替我们去分析表达式所属的类型。`auto`定义的变量必须有初始值。

#### 2.5.2.1 复合类型、常量和 auto
- 当引用被作为初始值时，编译器以引用对象的类型作为`auto`的类型
- `auto`一般会忽略掉顶层`const`，同时底层`const`会保留下来
- 如果希望别推断出的`auto`类型是一个顶层`const`，需要明确指出
- 设置一个类型为`auto`的引用时，初始值中的顶层变量属性仍然被保留。如果我们给初始值绑定一个引用，则此时的常量就不是顶层常量了。

### 2.5.3 decltype 类型指示符
c++新标准引入了`decltype`类型符，它的作用是选择并返回操作数的数据类型。在此过程中，编译器分析表达式并得到它的类型，却不实际计算表达式的值。  

如果`decltype`使用的表达式是一个变量，则`decltype`返回该变量的类型（包括顶层`const`和引用在内）：
```c++
const int ci = 0, &cj = ci;
decltype(ci) x = 0; // x的类型是const int
decltype(cj) y = x; // y的类型是const int&，y绑定到变量x
decltype(cj) z;  // error：z是一个引用，必须初始化
```

#### 2.5.3.1 decltype 和引用
如果`decltype`使用的表达式不是一个常量，则`decltype`返回表达式结果对应的类型。  
如果表达式的内容是解引用操作(`*`)，则`decltype`将得到引用类型。  
对于`decltype`所用的表达式来说，如果变量名加上了一层或者多层括号，编译器会把它当成一个表达式，从而得到引用类型；如果`decltype`使用的是一个不加括号的变量，则得到的结果就是该变量的类型。


# 第三章 字符串、向量和数组
## 3.1 命名空间的using声明
使用`using声明`可以直接访问命名空间的名字。

## 3.2 标准库类型string
标准库类型`string`表示可边长的字符序列，使用`string`类型必须首先包含`string`头文件。作为标准库的一部分，`string`定义在命名空间`std`中。

### 3.2.1 定义和初始化string对象
下面是初始化对象常用的一些方式：
| 初始化方式 | 说明 |
| :--: | :--: |
| `string s1` | 默认初始化，`s1`是一个空字符串 |
| `string s2(s1)` | `s2`是`s1`的副本 |
| `string s2 = s1` | 等价于`s2(s1)`，`s2`是`s1`的副本 |
| `string s3("value")` | `s3`是字面值`"value"`的副本，除了字面值最后的那个那个空字符外 |
| `string s3 = "value"` | 等价于`s3("value")`，`s3`是字面值`"value"`的副本 |
| `string s4(n,'c')` | 把`s4`初始化为由连续`n`个字符`c`组成的串 |

### 3.2.1.1 直接初始化和拷贝初始化
如果使用等号（`=`）初始化一个变量，实际上执行的是 **拷贝初始化** ，编译器将等号右边的初始值拷贝到新创建的对象中去。如果不使用等号，则执行的是 **直接初始化**。

### 3.2.2 string对象上的操作
下面是string的部分常用操作：
| 操作 | 含义 |
| :-: | :-: |
| `os << s` | 将`s`写到输出流`os`当中，返回`os` |
| `is >> s`  | 从`is`中读取字符串赋给`s`，字符串以空白分隔，返回`is` | 
| `getline(is, s)` | 从`is`中读取一行赋给`s`，返回`is` |
| `s.empty()` | `s`为空返回`true`，否则返回`false` |
| `s.size()` | 返回`s`中的字符的个数 |
| `s[n]` | 返回`s`中第`n`个字符的引用，位置从`0`计起 |
| `s1 + s2` | 返回`s1`和`s2`连接后的结果 |
| `s1 = s2` | 用`s2`的副本代替`s1`中原来的字符 |
| `s1 == s2` | 如果`s1`和`s2`中所含的字符完全一样，则它们相等，`string`对象的相等性判断对字母的大小写敏感 |
|  `s1 != s2` | 判断`s1`和`s2`中所含的字符是否不等 |
| `<, <=, >, >=` | 利用字符在字典中的顺序进行比较，且对字母的大小写敏感 |

#### 3.2.2.1 读写string对象
执行读取操作时，`string`对象会自动忽略开头的空白，并从第一个真正的字符开始读起，知道遇见下一个空白为止。

#### 3.2.2.2 使用getline读取一整行
`getline`函数的参数是一个输入流和一个`string`对象，函数从给定的输入流中读入内容，知道遇到换行符为止（换行符被读入），然后把所读的内容存入`string`对象中（不存换行符）。

#### 3.2.2.3 string::size_type 类型
`size`函数返回的是一个`string::size_type`类型的值，且是一个 **无符号** 类型的值，

#### 3.2.2.4 比较string对象
`string`对象相等表示它们的长度相同而且所包含的字符也全都相同。  
关系运算符依照（大小写敏感的）字典顺序：
- 如果两个`string`对象的长度不同，而且较短`string`对象的每个字符都与较长`string`对象对应位置上的字符相同，较短`string`对象小于较长`string`对象
- 如果两个`string`对象在某些对应的位置上不一致，则`string`对象比较的结果其实是`string`对象中第一对相异字符比较的结果

#### 3.2.2.5 string对象相加
对`string`对象使用`+`的结果是一个新的`string`对象。复合赋值运算符（`+=`）负责把右侧的`string`对象添加到左侧`string`对象的后面

#### 3.2.2.6 字面值和string对象相加
当`string`对象和字符字面值及字符串字面值混在一条语句中使用时，必须确保每个`+`的两侧运算对象至少有一个是`string`对象。
```c++
string s1 = "hello" + ",";//error
```

### 3.2.3 处理string对象中的字符
在`cctype`头文件中定义了一组标准函数处理判断字符特性：
| 函数 | 说明 | 
| :--: | :--: |
| `isalnum(c)` | 当`c`是字母或者数字时为真 |
| `isalpha(c)` | 当`c`是字母时为真 |
| `iscntrl(c)` | 当`c`是控制字符时为真 |
| `isdigit(c)` | 当`c`是数字时为真 |
| `isgraph(c)` | 当`c`不是空格但可打印时为真 |
| `islower(c)` | 当`c`是小写字母时为真 |
| `isprint(c)` | 当`c`是可打印字符时为真（即`c`是空格或`c`具有可视形式） |
| `ispunct(c)` | 当`c`是标点符号时为真 |
| `isspace(c)` | 当`c`是空白时为真 |
| `isupper(c)` | 当`c`是大写字母时为真 |
| `isxdigit(c)` | 当`c`是十六进制数字时为真 |
| `tolower(c)` | 输出`c`对应的小写字母 |
| `toupper(c)` | 输出`c`对应的大写字母 |

#### 3.2.3.1 处理每个字符？使用基于范围的for语句
范围`for`语句，这种语句遍历给定顶序列中的每个元素对序列中的每个值执行某种操作，其语法形式是：
```c++
for (declaration : expression)
    statement
```

#### 3.2.3.2 利用范围for语句改变字符串中的字符
如果要改变string对象中的字符的值，必须把循环变量定义成引用类型。

#### 3.2.3.2 利用下标进行迭代
```c++
string s("some string")
for (decltype(s.size()) index = 0; index != s.size() && !isspace(s[index]); ++index)   s[index] = toupper(s[index]);
```

> 使用下标时必须确保其在合理范围之内，一种简便易行的方法是，总是设下表的类型为`string::size_type`，因为此类型是无符号数，可以确保下标不会小于0。此时，代码只需保证下标小于`size()`的值就可以了。


## 3.3 标准库类型vector
标准库类型`vector`（容器）表示 **对象** 的集合，其中所有对象的类型都相同。集合中每个对象都有一个与之对应的索引用于访问对象。  
要使用`vector`必须包含适当的头文件和`using`声明：
```cpp
#include <vector>
using std::vector;
```