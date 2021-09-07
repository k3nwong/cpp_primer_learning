# 第二章
## 2.1 基本内置类型
### 2.1.1 算数类型
#### 练习2.1 
类型`int`、`long`、`long long`、`short`的区别是什么？无符号类型和带符号类型的区别是什么？`float`和`double`的区别是什么？ 
> 1. c++规定`short`和`int`至少为16位，`long`至少为32位，`long long`至少为64位。  
> 2. 带符号类型能够表示正数、负数和`0`，而无符号类型只能够表示`0`和正整数。
> 3. 一般使用`int`做整数运算，`short`因为太小在实际中用的少，`long`通常和`int`有着相同的大小。如果数据非常大，可以使用`long long`。
> 4. 如果你确认数据是非负的，那么就使用`unsigned`无符号类型。
> 5. 执行浮点运算时用`double`，因为`float`通常精度不够而且双精度浮点数和单精度浮点数的计算代价相差无几。

#### 练习2.2 
计算按揭贷款时，对于利率、本金和付款分别应选择何种数据类型？说明你的理由。
> 使用`float`或者`double`来计算按揭贷款


### 2.1.2 类型转换
#### 练习2.3
读程序写结果
```c++
unsigned u = 10, u2 = 42;
std::cout << u2 - u << std::endl;
std::cout << u - u2 << std::endl;

int i = 10, i2 = 42;
std::cout << i2 - i << std::endl;
std::cout << i - i2 << std::endl;
std::cout << i - u << std::endl;
std::cout << u - i << std::endl;
```
> 32, 4294967264, 32, -32, 0, 0


### 2.1.3 字面值常量
#### 练习2.5 
指出下述字面值的数据类型并说明每一组内几种字面值的区别  
a) `'a', L'a', "a", L"a"`  
b) `10, 10u, 10L, 10uL, 012, 0xC`  
c) `3.14, 3.14f, 3.14L`  
4) `10, 10u, 10., 10e-2`  
> a) 字符字面值，宽字符字面值，字符串字面值，宽字符串字面值。  
> b) 十进制整型，十进制无符号整型，十进制长整型，十进制无符号长整型，八进制整型，十六进制整型。  
> c) double, float, long double  
> d) 十进制整型，十进制无符号整型，double, double  

#### 练习2.6
下面两组定义是否有区别，如果有，请叙述之：
```c++
int month = 9, day = 7;
int month = 09, day = 07; 
```
> 第一行定义的是十进制整型。 第二行定义的是八进制整型且第二行`month`定义无效（超出8进制范围8）

#### 练习2.7
下面字面值表示何种含义？它们各自的数据类型是什么？  
a) `"Who goes with F\145rgus?\012"`  
b) `3.14e1L`  
c) `1024f`  
d) `3.14L`  
> a) `Who goes with Fergus?(换行)`，string 类型  
> b) `31.4`，long double类型  
> c) 无效，因为后缀`f`只能用于浮点字面量，而`1024`是整型  
> d) `3.14`，long double类型  

#### 练习2.8 
请利用转义序列编写一段程序，要求先输出`2M`，然后转到新一行。修改程序使其先输出`2`，然后输出制表符，再输出`M`，最后转到新一行。
> ```c++
> #include <iostream>
> 
> int main()
> {
>     std::cout << 2 << "\115\012";
>     std::cout << 2 << "\t\115\012";
>     return 0;
> }
> ```


## 2.2 变量
### 2.2.1 变量定义
#### 练习2.9 
解释下列定义的含义。对于非法的定义，请说明错在何处并将其改正。 
a) `std::cin >> int input_value;`   
b) `int i = { 3.14 };`  
c) `double salary = wage = 9999.99;`  
d) `int i = 3.14;`  
> a) 应该先定义后使用  
> b) 欲用列表初始化`int`型的变量，用列表初始化内置类型的变量时，如果存在丢失信息的风险，则编译器将报错  
> c) 变量`wage`未定义，需定义后再初始化
> d) 用浮点数`3.14`初始化整型`i`，小数点后面会被截断

#### 练习2.10
下面变量的初值分别是什么？
```c++
std::string global_str;
int global_int;
int main()
{
    int local_int;
    std::string local_str;
}
```
> `global_int`是全局变量，所以初值为`0`。`local_int`是局部变量并且没有初始化，它的初值是未定义的。`global_str`和`local_str`是`string`类的对象，该对象定义了默认的初始化方式，即初始化为空字符串。

### 2.2.2 变量声明和定义的关系
#### 练习 2.11 
指出下面的语句是声明还是定义：  
a) `extern int ix = 1024;`
b) `int iy;`
c) `extern int iz;`

> a) 定义； b) 定义； c) 声明；

### 2.2.3 标识符
#### 练习2.12 
请指出下面的名字中哪些是非法的？  
(a) `int double = 3.14;`  
(b) `int _;`  
(c) `int catch-22;`  
(d) `int 1_or_2 = 1;`  
(e) `double Double = 3.14;`  
> (a), (c), (d) 非法。

### 2.2.4 名字的作用域
#### 练习2.13
下面程序中的`j`值是多少？  
```c++
int i = 42;
int main()
{
    int i = 100;
    int j = i;
}
```
> 100

#### 练习2.14
下面程序合法吗？如果合法，它将输出什么？  
```c++
int i = 100, sum = 0;
for (int i = 0; i != 10; ++i)  sum += i;
std::cout << i << " " << sum << std::endl;
```
> 合法，输出是`100(i)`,`45(sum)`


## 2.3 复合类型
### 2.3.1 引用
#### 练习2.15
下面的哪个定义是不合法的？为什么？  
(a) `int ival = 1.01;`  
(b) `int &rval1 = 1.01;`  
(c) `int &rval2 = ival;`  
(d) `int &rval3;`  
> (b)不合法，因为引用类型的初始值必须是一个对象；(d)不合法，因为引用必须初始化

#### 练习2.16
考查下面的所有赋值然后回答：哪些赋值是不合法的？为什么？哪些赋值是合法的？它们执行了什么样的操作？  
```c++
int i = 0, &r1 = i; double d = 0, &r2 = d;
(a) r2 = 3.14159;
(b) r2 = r1;
(c) i = r2;
(d) r1 = d;
```
> (a)合法。给`d`赋值为`3.14159`  
> (b)合法。会执行自动类型转换（`int->double`）  
> (c)合法。会发生小数截取   
> (d)合法。会发生小数截取

#### 练习2.17
> 执行下面的代码段将输出什么结果？
```cpp
int i, &ri = i;
i = 5; ri = 10;
std::cout << i << " " << ri << std::endl;
```
> 输出：10 10

### 2.3.2 指针
#### 练习2.18
编写代码分别更改指针的值以及指针所指的对象的值。
> ```c++
> int a = 1, b = 2;
> int *p1 = &a, *p2 = p1;
> //change value of pointer
> p1 = &b;
> //change the value of the object which pointer pointing at
> p2 = b;
> ```

#### 练习2.19
请说明指针和引用的主要区别。
> 主要区别：
> 1. 引用只是一个对象的别名，本身不是一个对象，而指针指向该对象（内存的一个存储单元）且本身也是一个对象，它存储的是目标对象的地址。
> 2. 引用必须初始化,引用的值不能为`NULL`，且一旦定义了引用就无法再绑定到其他对象上。指针可以不再定义时初始化，也可以重新赋值使其指向其他的对象且指针的值可以为空。
> 3. 可以有`const`指针，但是没有`const`引用

#### 练习2.20
请叙述下面这段代码的作用
```c++
int i = 42;
int *p1 = &i;
* p1 = *p1 * *p1;
```
> 初始化一个`int`型变量`i`为`42`，再初始化一个`int`型指针`p1`，并使指针`p1`指向`i`，然后将`i`的值重新设置为`42*42`。

#### 练习 2.21
请解释下述定义。在这些定义中有非法的吗？如果有，为什么？
```c++
int i = 0;
(a) double* dp = &i;
(b) int *ip = i;
(c) int *p = &i;
```
> (a)非法，指针类型与所指对象类型不一样。
> (b)非法，应该用变量`i`的地址(`&i`)初始化指针
> (c)合法

#### 练习2.22
假设p是一个int型指针，请说明下述代码的含义。
```c++
if (p) //...
if (*p) //...
```
> `if (p) //...` 判断 `p`是否为空指针
> `if (*p) //...` 判断`p`所指向的对象的值是否为`0`

#### 练习2.23
给定指针p，你能知道它是否指向了一个合法的对象吗？如果能，叙述判断的思路；如果不能，也请说明理由。
> 不能，因为首先要确定这个指针是不是合法的（指针的值的四种状态），才能判断它所指向的对象是不是合法的。假设指针没有被初始化，则其存放的是一个随机的地址；如果其没有被合法地初始化，恶意存放了一个地址，这两种情况都是很危险的情况。

#### 练习2.24
在下面代码中为什么p合法而lp非法？
```c++
int i = 42;
void *p = &i;
long *lp = &i;
```
> `void *` 是从 C语言那里继承过来的一类特殊类型的指针类型，可以指向任何类型的对象。而其他指针类型必须要与所指对象类型严格匹配。

### 2.3.3 理解复合类型的声明
#### 练习2.25 
说明下列变量的类型和值
```c++
(a) int* ip, i, &r = i;
(b) int i, *ip = 0;
(c) int* ip, ip2;
```
> (a)`ip`是指向`int`的指针，`i`是`int`类型的变量，`r`是`i`的引用
> (b)`i`是`int`类型的变量，`ip`是一个空指针
> (c)`ip`是指向`int`的指针，`ip2`是`int`类型的变量

## 2.4 const限定符
#### 练习2.26
下面哪些句子是合法的？如果有不合法的句子，请说明为什么？
```c++
(a)const int buf;
(b)int cnt = 0;
(c)const int sz = cnt;
(d)++cnt; ++sz;
``` 
> (a)不合法，`const`变量必须初始化；(d)不合法，`const`变量`sz`不能被改变  
> (b)(d)均合法

### 2.4.1 const的引用

### 2.4.2 指针和const
#### 练习2.27
下面的哪些初始化是合法的？请说明理由。
```c++
(a)int i = -1, &r = 0;         
(b)int *const p2 = &i2;        
(c)const int i = -1, &r = 0;   
(d)const int *const p3 = &i2;  
(e)const int *p1 = &i2;        
(f)const int &const r2;        
(g)const int i2 = i, &r = i;   
```
> (b)(c)(d)(e)(g)合法  
> (a)不合法，因为`r`引用必须引用一个对象  
> (f)不合法，`r2`是引用必须初始化且引用没有顶层`const`

#### 练习2.28
说明下面的这些定义是什么意思，挑出其中不合法的。
```c++
(a)int i, *const cp;
(b)int *p1, *const p2;
(c)const int ic, &r = ic;
(d)const int *const p3;  
(e)const int *p;    
```
> (a)、(b)、(d)均不合法，`const`指针必须初始化   
> (c)不合法，`const int`必须初始化  
> (e)合法，含义为指向一个`const int`类型的指针

#### 练习2.29
假设已有上一个练习中定义的那些变量，则下面的哪些语句是合法的？请说明理由。
```c++
(a)i = ic;    
(b)p1 = p3; 
(c)p1 = &ic;  
(d)p3 = &ic; 
(e)p2 = p1;    
(f)ic = *p3;   
```
> (a)、(d)、(e)、(f)均合法  
> (b)不合法，`p3`是常量指针，不能赋值给普通指针  
> (c)不合法，**普通指针不能指向常量**

### 2.4.3 顶层const
#### 练习2.30
对于下面的这些语句，请说明对象被声明成了顶层`const`还是底层`const`？
```c++
const int v2 = 0;
int v1 = v2;
int *p1 = &v1, &r1 = v1;
const int *p2 = &v2, *const p3 = &i, &r2 = v2;
```
> v2是顶层`const`，p2是底层`const`，p3既是底层`const`又是顶层`const`，r2是底层`const`


#### 练习2.31
假设已有上一个练习中所做的那些声明，则下面的哪些语句是合法的？请说明顶层const和底层const在每个例子中有何体现？
```c++
r1 = v2;//合法，顶层const在拷贝时不受影响
p1 = p2;//不合法，p2是底层const，如果要拷贝必须要求p1也是底层const
p2 = p1;//合法，因为int* 可以转换成const int*
p1 = p3;//不合法，p3是一个底层const，p1是只是一个普通的指针
p2 = p3; //合法，p2和p3都是底层const，拷贝时忽略掉底层const
```

### 2.4.4 constexpr和常量表达式
#### 练习2.32 
下面代码是否合法？如果非法，请设法将其修改正确。
```c++
int null = 0, *p = null;
```
> 非法.  把int变量直接赋给指针是错误的操作,即使int变量的值恰好等于0也不行.  
> `int null = 0, *p = &null;`

## 2.5 处理类型
### 2.5.1 类型别名

### 2.5.2 auto类型说明符
#### 练习2.33
利用本节定义的变量，判断下列语句的运行结果。
```c++
a = 42; b = 42; c = 42;
d = 42; e = 42; g = 42;
```

> ```c++
> a = 42; // a 是 int
> b = 42; // b 是一个 int,(ci的顶层const在拷贝时被忽略掉了)
> c = 42; // c 也是一个int
> d = 42; // d 是一个 int *,所以语句非法
> e = 42; // e 是一个 const int *, 所以语句非法
> g = 42; // g 是一个 const int 的引用，引用都是底层const，所以不能被赋值
> ```

#### 练习2.34
基于上一个练习中的变量和语句编写一段程序，输出赋值前后变量的内容，你刚才的推断正确吗？如果不对，请反复研读本节的示例知道你明白错在何处为止。
> ```c++
> #include <iostream>
> int i = 0, &r = i;
> auto a = r;
> 
> const int ci = i, &cr = ci;
> auto b = ci;
> auto c = cr;
> auto d = &i;
> auto e = &ci;
> 
> const auto f = ci;
> auto &g = ci;
> 
> std::cout << a << std::endl;// 0
> std::cout << b << std::endl;// 0
> std::cout << c << std::endl;// 0
> std::cout << d << std::endl;// 0x61fee8
> std::cout << e << std::endl;// 0x61fee4
> std::cout << f << std::endl;// 0
> std::cout << g << std::endl;// 0
> std::cout << "--------------" << std::endl;
> a = 42;
> b = 42; 
> c = 42;
> 
> std::cout << a << std::endl;// 42
> std::cout << b << std::endl;// 42
> std::cout << c << std::endl;// 42
> std::cout << d << std::endl;// 0x61fee8
> std::cout << e << std::endl;// 0x61fee4
> std::cout << f << std::endl;// 0
> std::cout << g << std::endl;// 0
> 
> return 0;
> ```

#### 练习2.35
判断下列定义推断出的类型是什么，然后编写程序进行验证。
```c++
const int i = 42;
auto j = i; 
const auto &k = i;
auto *p = &i;
const auto j2 = i, &k2 = i;
```

> `j`是`int`，`k`是`const int`的引用，`p`是`const int *`，`j2`是`const int`，`k2`是`const int`的引用。

### 2.5.3 decltype 类型指示符
#### 练习2.36
关于下面的代码，请指出每一个变量的类型以及程序结束时它们各自的值。
```c++
int a = 3, b =4;
decltype(a) c = a;
decltype((b)) d = a;
++c;
++d;
```
> `c`的类型是`int`，`d`的类型是`int &`。程序结束时，`c`的值为`4`，`d`为`4`。

#### 练习2.37
赋值是会产生引用的一类典型表达式，引用的类型就是左值的类型。也就是说，如果`i`是`int`，则表达式`i = x`的类型是`int&`。根据这一特点，请指出下面代码中每一个变量的类型和值。
```c++
int a = 3, b = 4;
decltype(a) c = a;
decltype(a = b) d = a;
```
> `c`的类型是`int`，`d`的类型是`int&`，`c`和`d`的值为`3`。

#### 练习2.38
说明由`decltype`指定类型和由`auto`指定类型有何区别。请举一个例子，`decltype`指定的类型与`auto`指定的类型一样；再举一个例子，`decltype`指定的类型与`auto`指定的类型不一样。
> `decltype`处理顶层`const`和引用的方式与`auto`不同，`decltype`会将顶层`const`和引用保留起来。
> ```cpp
> int i = 0, &r = i;
> //相同
> auto a = i;
> decltype(i) b = i;
> //不同 d 是一个 int&
> auto c = r;
> decltype(r) d = r;
> ```



# 第三章 字符串、向量和数组
## 3.1 命名空间的using声明

## 3.2 标准库类型string
### 3.2.1 定义和初始化string对象

### 3.2.2 string对象上的操作
#### 练习3.2
编写一段程序从标准输入中依次读入一整行，然后修改该程序使其依次读入一个词
> ```c++
> #include <iostream>
> #include <string>
> 
> using std::string;
> using std::cin;
> using std::cout;
> using std::endl;
> using std::getline;
> 
> int main()
> {
>     string s;
>     while (getline(cin, s))
>     {
>         cout << s << endl;
>     }
>     cout << "-------------------" << endl;
>     while (cin >> s)
>     {
>         cout << s << endl;
>     }
>     return 0;
> }
> ```

#### 练习3.3
请说明string类的输入运算符和getline函数分别是如何处理空白字符的
> `string`类的输入运算符的读取，`string`对象会忽略开头的空白并从第一个真正的字符开始，直到遇见下一空白为止
> `getline()`函数的读取，string对象会从输入流中读取字符，直到遇见换行符为止


#### 练习3.4 
编写一段程序读入两个字符串，比较其是否相等并输出结果。如果不相等，输出较大的那个字符串。改写上述程序，比较输入的两个字符串是否等长，如果不等长，输出长度较大的那个字符串
> ```c++
> #include <iostream>
> #include <string>
> using std::string;
> using std::cout;
> using std::cin;
> using std::endl;
>
> int main()
> {
>     string s1,s2;
>     getline(cin, s1);
>     getline(cin, s2);
> 
>     if (s1 == s2)
>     {
>         cout << "equal!" << endl;
>     }
>     else 
>     {
>         cout << ((s1 > s2) ? s1 : s2) << endl;
>     }
> }
> ```

> ```c++
> #include <iostream>
> #include <string>
> using std::string;
> using std::cout;
> using std::cin;
> using std::endl;
> 
> int main()
> {
>     string s1,s2;
>     getline(cin, s1);
>     getline(cin, s2);
>
>     if (s1.size() == s2.size())
>     {
>         cout << "equal!" << endl;
>     }
>     else 
>     {
>         cout << ((s1.size() > s2.size()) ? s1 : s2) << endl;
>     }
> }
> ```


#### 练习3.5
编写一段程序从标准输入中读入多个字符串并将它们连接在一起，输出连接成的大字符串，然后修改上述程序，用空格把输入的多个字符串分隔开来
> ```c++
> #include <iostream>
> #include <string>
> using std::string;
> using std::cout;
> using std::cin;
> using std::endl;
> 
> int main()
> {
> 	string result, s;
> 	while (getline(cin, s))
> 	{
> 		result += s;
> 	}
> 	cout << result << endl;
>
> 	return 0;
> }
> ```

> ```c++
> #include <iostream>
> #include <string>
> using std::string;
> using std::cout;
> using std::cin;
> using std::endl;
>
> int main()
> {
> 	string result, s;
> 	while (getline(cin, s))
> 	{
> 		result += s + " ";
> 	}
> 	cout << result << endl;
>
> 	return 0;
> }
> ```

### 3.2.3 处理string对象中的字符
#### 练习3.6
编写一段程序，使用范围`for`语句将字符串内所有字符用`X`代替。
> ```cpp
> for (auto &x : s)
> 	{
> 		x = 'X';
> 	}
> ```

#### 练习3.7
就上一题完成的程序而言，如果将循环控制的变量设置为char将发生什么？先估计一下结果，然后实际编程进行验证。
> 如果设置为char，那么原来的字符串不会发生改变。


#### 练习3.8
分别用while循环和传统for循环重写第一题的程序，你觉得哪种形式更好呢？为什么？
> 范围for语句不直接操作索引，更简洁。


#### 练习3.9
下面的程序有何作用？它合法吗？如果不合法？为什么？
```cpp
string s;
cout << s[0] << endl;
```
> 不合法。使用下标访问空字符串是非法的行为。

#### 练习3.10
编写一段程序，读入一个包含标点符号的字符串，将标点符号去除后输出字符串剩余的部分。
> ```cpp
> string s, result;
> for (auto x : s)
> 	{
> 		if (!ispunct(x))
> 		{
> 			result += x;
> 		}
> 	}
> ```

#### 练习3.11
下面的范围for语句合法吗？如果合法，c的类型是什么？
```cpp
const string s = "Keep out!";
for(auto &c : s){ /* ... */ }
```
> 要根据`for`循环中的代码来看是否合法，`c`是`string`对象中字符的引用，`s`是常量。因此如果`for`循环中的代码重新给`c`赋值就会非法，如果不改变`c`的值，那么合法。


## 3.3 标准库类型vector
### 3.3.1 定义和初始化vector对象
#### 练习3.12
下列vector对象的定义有不正确的吗？如果有，请指出来。对于正确的，描述其执行结果；对于不正确的，说明其错误的原因。
```cpp
(a)vector<vector<int>> ivec;
(b)vector<string> svec = ivec;
(c)vector<string> svec(10, "null");
```
> (a)合法，将对`ivec`进行默认初始化 (b)不合法，`ivec`和`svec`的类型不一致 (c)合法，将把`svec`初始化为10个初始值为`"null"`的`string`集合。


#### 练习3.13 下列的vector对象各包含多少个元素？这些元素的值分别是多少？
```cpp
(a)vector<int> v1;
(b)vector<int> v2(10);  
(c)vector<int> v3(10, 42); 
(d)vector<int> v4{10};   
(e)vector<int> v5{10, 42 }; 
(f)vector<string> v6{10}; 
(g)vector<string> v7{ 10, "hi" }; 
```
> (a)`size：`0； `value：`no value  
> (b)`size：`10； `value：`0  
> (c)`size：`10 ；`value：`42  
> (d)`size：` 1；`value：`10  
> (e)`size：` 2；`value：`10，42  
> (f)`size：` 10；`value：`""  
> (g)`size：` 10；`value：`"hi"

### 3.3.2 向vector对象中添加元素
#### 练习3.14
编写一段程序，用cin读入一组整数并把它们存入一个vector对象。
> ```cpp
> #include <iostream>
> #include <vector>
> using std::vector;
> using std::cin;
> using std::cout;
> using std::endl;
> 
> int main()
> {
>  	vector<int> v;
> 	int i;
> 	while (cin >> i)
> 	{
> 		v.push_back(i);
> 	}
> 	return 0;
> }
> ```

#### 练习3.15
改写上题程序，不过这次读入的是字符串。
> ```cpp
> #include <iostream>
> #include <vector>
> #include <string>
> #include <cctype>
> using std::vector;
> using std::string;
> using std::cin;
> using std::cout;
> using std::endl;
> 
> int main()
> {
> 	vector<string> v;
> 	string i;
> 	while (cin >> i)
> 	{
> 		v.push_back(i);
> 	}
> 	return 0;
> }
> ```

### 3.3.3 其他vector操作
#### 练习3.16
编写一段程序，把练习3.13中`vector`对象的容量和具体内容输出出来
> ```cpp
> #include <iostream>
> #include <string>
> #include <cctype>
> #include <vector>
> using std::cin;
> using std::cout;
> using std::endl;
> using std::vector;
> using std::string;
> 
> int main()
> {
> 	vector<int> v1;     
> 	vector<int> v2(10);    
> 	vector<int> v3(10, 42); 
> 	vector<int> v4{ 10 };    
> 	vector<int> v5{ 10, 42 }; 
> 	vector<string> v6{ 10 };  
> 	vector<string> v7{ 10, "hi" }; 
> 
> 	cout << "v1 size :" << v1.size() << endl;
> 	cout << "v2 size :" << v2.size() << endl;
> 	cout << "v3 size :" << v3.size() << endl;
> 	cout << "v4 size :" << v4.size() << endl;
> 	cout << "v5 size :" << v5.size() << endl;
> 	cout << "v6 size :" << v6.size() << endl;
> 	cout << "v7 size :" << v7.size() << endl;
> 
> 	cout << "v1 content: ";
>	for (auto i : v1)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>
>	cout << "v2 content: ";
>	for (auto i : v2)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>
>	cout << "v3 content: ";
>	for (auto i : v3)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>
>	cout << "v4 content: ";
>	for (auto i : v4)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>
>	cout << "v5 content: ";
>	for (auto i : v5)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>
>	cout << "v6 content: ";
>	for (auto i : v6)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>
>	cout << "v7 content: ";
>	for (auto i : v7)
>	{
>		cout << i << " , ";
>	}
>	cout << endl;
>	return 0;
> }
> ```

#### 练习3.17
从`cin`读入一组词并把它们存入一个`vector`对象，然后设法把所有词都改为大写形式。输出改变后的结果，每个词占一行。
> ```cpp
> #include <iostream>
> #include <string>
> #include <cctype>
> #include <vector>
>
> using std::cin;
> using std::cout;
> using std::endl;
> using std::vector;
> using std::string;
>
> int main()
> {
>	vector<string> v;
>	string s;
>
>	while (cin >> s)
>	{
>		v.push_back(s);
>	}
>
>	for (auto &str : v)
>	{
>		for (auto &c : str)
>		{
>			c = toupper(c);
>		}
>	}
>
>	for (auto i : v)
>	{
>		cout << i << endl;
>	}
>	return 0;
> }
> ```

#### 练习3.18
下面的程序合法吗？如果不合法，你准备如何修改？
```cpp
vector<int> ivec;
ivec[0] = 42;
```
> 不合法，不能对空`vector`进行下标赋值操作。应改为：
> ```cpp
> ivec.push_back(42);
> ```

#### 练习3.19
如果想定义一个含有`10`个元素的`vector`对象，所有元素的值都是42，请例举三种不同的实现方法，哪种方式更好呢？  
> 如下三种：
> ```cpp
> vector<int> ivec1(10, 42);
> vector<int> ivec2{ 42, 42, 42, 42, 42, 42, 42, 42, 42, 42 };
> vector<int> ivec3;
> for (int i = 0; i < 10; ++i)
> 	ivec3.push_back(42);
> ```
> 第一种方式最好。

#### 练习3.20
读入一组整数并把他们存入一个`vector`对象，将每对相邻整数的和输出出来。改写你的程序，这次要求先输出第一个和最后一个元素的和，接着输入第二个和倒数第二个元素的和，以此类推。
> ```cpp
> #include <iostream>
> #include <vector>
> using std::cout;
> using std::cin;
> using std::endl;
> using std::vector;
>
> int main()
> {
>    //question 1
>    vector<int> ivec;
>    int i;
>    while (cin >> i)
>    {
>        ivec.push_back(i);
>    }
>
>    for (int i = 0; i < ivec.size() - 1; i++)
>    {
>        cout << ivec[i] + ivec[i + 1] << endl;
>    }
>
>    //question 2
>    int m = 0;
>    int n = ivec.size() - 1;
>    while (n > m)
>    {
>        cout << ivec[m] + ivec[n] << endl;
>        ++m;
>        --n;
>    }
>    return 0;
>    }
> ```

## 3.4 迭代器介绍
### 3.4.1 使用迭代器
#### 练习3.21
请使用迭代器重做 **练习3.16**
> ```cpp
> #include <iostream>
> #include <string>
> #include <iterator>
> #include <vector>
> using std::cout;
> using std::string;
> using std::endl;
> using std::vector;
>
> void print(const vector<int>& vec)
> {
>    cout << "size: " << vec.size() << endl 
>        << " content :";
>    for (auto it = vec.begin(); it !=  vec.end(); ++it)
>    {
>        cout << *it << (it != vec.end() - 1 ? ", " : "");
>    }
>    cout << endl;
>    
> }
>
> void print(const vector<string>& vec)
> {
>    cout << "size: " << vec.size() << endl 
>        << " content :";
>    for (auto it = vec.begin(); it !=  vec.end(); ++it)
>    {
>        cout << *it << (it != vec.end() - 1 ? ", " : "");
>    }
>    cout << endl;
> }
>
> int main()
> {
>    vector<int> v1;     
>	vector<int> v2(10);    
>	vector<int> v3(10, 42); 
>	vector<int> v4{ 10 };    
>	vector<int> v5{ 10, 42 }; 
>	vector<string> v6{ 10 };  
>	vector<string> v7{ 10, "hi" }; 
>
>    print(v1);
>    print(v2);
>    print(v3);
>    print(v4);
>    print(v5);
>    print(v6);
>    print(v7);
>
>    return 0;
> }
> ```

#### 练习3.22
修改之前那个输出text第一段的程序，首先把text的第一段全部改成大写形式，然后输出它。
> ```cpp
> #include <iostream>
> #include <vector>
> #include <string>
> using namespace std;
>
> int main()
> {
>    vector<string> text;
>    text.push_back("aaaaaaaaaa aaaaaaaaa aaaaaa"); 
>    text.push_back("");
>    text.push_back("bbbbbbbbbbbbbb bbbbbbbbbbb bbbbbbbbbbbbb");
>
>    for (auto it = text.begin(); it != text.end() && !it->empty(); ++it)
>    {
>        for (auto &c : *it)
>        {
>            if (isalpha(c)) c = toupper(c);
>        }
>    }
>
>    for (auto it : text)
>    {
>        cout << it << endl;
>    }
>    
>    return 0;
>    
> }
> ```

#### 练习3.23
编写一段程序，创建一个含有10个整数的`vector`对象，然后使用迭代器将所有的元素都变成原来的两倍，输出`vector`对象的内容，检验程序是否正确。
> ```cpp
> #include <iostream>
> #include <vector>
> #include <iterator>
> using namespace std;
>
> int main()
> {
>    vector<int> ivec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
>    
>    for (auto it = ivec.begin(); it != ivec.end(); ++it)
>    {
>        *it  = *it * 2;
>        cout << *it << endl;
>    }
>    return 0;
> }
> ```


### 3.4.1 迭代器运算
#### 练习3.24 
请使用迭代器重做练习3.20
> ```cpp
> #include <iostream>
> #include <string>
> #include <vector>
> using namespace std;
>
> int main()
> {
>    vector<int> ivec;
>    int i;
>    while (cin >> i)
>    {
>        ivec.push_back(i);
>    }
>    
>    for (auto it = ivec.begin(); it != ivec.end() - 1; it++)
>    {
>        cout << *it + *(it + 1) << endl;
>    }
>
>    cout << "---------------------------------" << endl;
>
>	auto it1 = ivec.begin();
>	auto it2 = ivec.end() - 1;
>	while (it1 < it2)
>	{
>		cout << *it1 + *it2 << endl;
>		++it1;
>		--it2;
>	}
>	return 0;
> }
> ```

#### 练习3.25 
3.3.3节划分分数段的程序是使用下标运算符实现的，请利用迭代器改写该程序实现完全相同的功能。
> ```cpp
> #include <vector>
> #include <iostream>
> using namespace std;
>
> int main()
> {
>	vector<unsigned> scores(11, 0);
>	unsigned grade;
>	while (cin >> grade)
>	{
>		if (grade <= 100)
>			++*(scores.begin() + grade / 10);
>	}
>
>	for (auto s : scores)
>		cout << s << " ";
>	cout << endl;
>
>	return 0;
> }
> ```

#### 练习3.26
在100页的二分搜索程序中，为什么用的是`mid = beg + (end - beg) / 2`, 而非`mid = (beg + end) / 2`; ?
> 因为迭代器支持的运算只有 `-` ，而没有 `+` 。`end - beg` 意思是相距若干个元素，将之除以`2`然后与`beg`相加，表示将`beg`移动到一半的位置。


## 3.5 数组
### 3.5.1 定义和初始化内置数组
#### 练习3.27
假设`txt_size`是一个无参函数，它的返回值是`int`。请回答下列哪个定义是非法的，为什么？
```cpp
unsigned buf_size = 1024;
(a) int ia[buf_size];
(b) int ia[4 * 7 - 14];
(c) int ia[txt_size()];
(d) char st[11] = "fundamental";
```
> (a) 非法。纬度必须是一个常量表达式。   
> (b) 合法。  
> (c) 非法。txt_size() 的值必须要到运行时才能得到。  
> (d) 非法。数组的大小应该是12。

#### 练习3.28
下列数组中元素的值是什么？
```cpp
string sa[10];
int ia[10];
int main() {
	string sa2[10];
	int ia2[10];
}
```
> 数组的元素会被默认初始化。`sa`的元素值全部为空字符串，`ia`的元素值全部为`0`。`sa2`的元素值全部为空字符串，`ia2`的元素值全部未定义。

#### 练习3.29
相比于`vector`来说，数组有哪些缺点，请列举一些。
> 1. 数组的大小是确定的  
> 2. 不能随意增加元素  
> 3. 不允许拷贝和赋值  

### 3.5.2 访问数组元素
#### 练习3.30
指出下面代码中的索引错误。
```cpp
constexpr size_t array_size = 10;
int ia[array_size];
for (size_t ix = 1; ix <= array_size; ++ix)
	ia[ix] = ix;
```

当`ix`增长到`10`的时候，`ia[ix]`的下标越界。

#### 练习3.31
编写一段程序，定义一个含有`10`个`int`的数组，令每个元素的值就是其下标值。
> ```cpp
> #include <iostream>
> using std::cout;
> using std::endl;
>
> int main()
> {
>    int a[10];
>    for (auto i = 0; i < 10; i++){
>        a[i] = i;
>        cout << a[i] << endl;
>    }
>    return 0;
> }
> ```

#### 练习3.32
将上一题刚刚创建的数组拷贝给另一数组。利用`vector`重写程序，实现类似的功能。
> ```cpp
> #include <iostream>
> #include <vector>
> using std::cout;
> using std::endl;
> using std::vector;
>
> int main()
> {
>    int a[10] = {0,1,2,3,4,5,6,7,8,9};
>    int b[10];
>    for (auto i = 0; i < 10; i++){
>        b[i] = a[i];
>    }
>    return 0;
>
>    //--------------------------------
>    vector<int> c(10);
>    for (auto j = 0; j < 10; j++)
>    {
>        c[j] = a[j];
>    }
>    vector<int> v2(c);
> }
> ```

#### 练习3.33
对于104页的程序来说，如果不初始化`scores`将会发生什么？
> 数组中所有元素的值将会未定义。

### 3.5.3 指针和数组
#### 练习3.34
假定`p1`和`p2`都指向同一个数组中的元素，则下面程序的功能是什么？什么情况下该程序是非法的？
```cpp
p1 += p2 - p1;
```
> 将`p1`移动到`p2`的位置。任何情况下都合法。

#### 练习3.35
编写一段程序，利用指针将数组中的元素置为0。
> ```cpp
> #include <iostream>
> using std::cout; 
> using std::endl;
> 
> int main()
> {
>	const int size = 10;
>	int arr[size];
>	for (auto ptr = arr; ptr != arr + size; ++ptr) 
>		*ptr = 0;
>
>	for (auto i : arr) cout << i << ", ";
>	cout << endl;
>
>	return 0;
> }
> ```

#### 练习3.36
编写一段程序，比较两个数组是否相等。再写一段程序，比较两个`vector`对象是否相等。
> ```cpp
> #include <iostream>
> #include <vector>
> #include <iterator>
> using namespace std;
>
> bool compare(int* const beg1, int* const end1, int* const beg2, int* const end2)
> {
>	if ((end1 - beg1) != (end2 - beg2)) 
>		return false;
>	else
>	{
>		for (int* i = beg1, *j = beg2; (i != end1) && (j != end2); ++i, ++j)
>			if (*i != *j)
>				return false;
>	}
>
>	return true;
> }
>
> int main()
> {
>	int arr1[3] = { 0, 1, 2 };
>	int arr2[3] = { 0, 2, 4 };
>
>	if (compare(begin(arr1), end(arr1), begin(arr2), end(arr2)))
>		cout << "The two arrays are equal." << endl;
>	else
>		cout << "The two arrays are not equal." << endl;
>
>	vector<int> vec1 = { 0, 1, 2 };
>	vector<int> vec2 = { 0, 1, 2 };
>
>	if (vec1 == vec2)
>		cout << "The two vectors are equal." << endl;
>	else
>		cout << "The two vectors are not equal." << endl;
>
>	return 0;
> }
> ```

### 3.5.4 C风格字符串
#### 练习3.37
下面的程序是何含义，程序的输出结果是什么？
```cpp
const char ca[] = { 'h', 'e', 'l', 'l', 'o' };
const char *cp = ca;
while (*cp) {
    cout << *cp << endl;
    ++cp;
}
```
> 会将`ca`字符数组中的元素打印出来。但是因为没有空字符的存在，程序不会退出循环。

#### 练习3.38
在本节中我们提到，将两个指针相加不但是非法的，而且也没有什么意义。请问为什么两个指针相加没有意义？
> 指针是用来代表内存地址的。指针的数值是该地址相对于最低位地址也就是0位地址的偏移量，也可称之为坐标。坐标相加得到的新值是没什么意义的，坐标相减则是距离，坐标加距离则是新坐标，后两者是有意义的。

#### 练习3.39
编写一段程序，比较两个string对象。再编写一段程序，比较两个C风格字符串的内容
> ```cpp
> #include <iostream>
> #include <string>
> #include <cstring>
> using std::cout; 
> using std::endl; 
> using std::string;
>
> int main()
> {
>	string s1("aaaaaaaaaa"), s2("bbbbbbbbbb");
>	if (s1 == s2)
>		cout << "same string." << endl;
>	else if (s1 > s2)
>		cout << "aaaaaaaaaa > bbbbbbbbbb" << endl;
>	else
>		cout << "aaaaaaaaaa < bbbbbbbbbb" << endl;
>
>	const char* cs1 = "aaaaaaaaaa";
>	const char* cs2 = "bbbbbbbbbb";
>	auto result = strcmp(cs1, cs2);
>	if (result == 0)
>		cout << "same string." << endl;
>	else if (result < 0)
>		cout << "aaaaaaaaaa < bbbbbbbbbb" << endl;
>	else
>		cout << "aaaaaaaaaa > bbbbbbbbbb" << endl;
>
>	return 0;
> }
> ```

#### 练习3.40
编写一段程序，定义两个字符数组并用字符串字面值初始化它们；接着再定义一个字符数组存放前面两个数组连接后的结果。使用strcpy和strcat把前两个数组的内容拷贝到第三个数组当中。
> ```cpp
> #include <iostream>
> #include <cstring>
>
> const char cstr1[] = "Hello ";
> const char cstr2[] = "world!";
>
> int main()
> {
>	char cstr3[100];
>
>	strcpy(cstr3, cstr1);
>	strcat(cstr3, cstr2);
>
>	std::cout << cstr3 << std::endl;
> }
> ```

### 3.5.5 与旧代码的接口
#### 练习3.41
编写一段程序，用整型数组初始化一个`vector`对象
> ```cpp
> #include <iostream>
> #include <vector>
> using namespace std;
> 
> int main()
> {
>	int arr[] = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
>	vector<int> v(begin(arr), end(arr));
>
>	for (auto i : v) cout << i << " ";
>	cout << endl;
>
>	return 0;
> }
> ```

#### 练习3.42
编写一段程序，将含有整数元素的`vector`对象拷贝给一个整型数组
> ```cpp
> #include <iostream>
> #include <vector>
>
> using namespace std;
>
> int main()
> {
>	vector<int> v{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
>	int arr[10];
>	for (int i = 0; i < v.size(); ++i) 
>		arr[i] = v[i];
>
>	for (auto i : arr) cout << i << " ";
>	cout << endl;
>
>	return 0;
> }
> ```


## 3.6 多维数组
#### 练习3.43
编写3个不同版本的程序，令其均能输出`ia`的元素。版本1使用范围`for`语句管理迭代过程；版本2和版本3都使用普通`for`语句，其中版本2要求使用下标运算符，版本3要求使用指针。此外，在所有3个版本的程序中都要直接写出数据类型，而不能使用类型别名、`auto`关键字和`decltype`关键字。
> ```cpp
> #include <iostream>
> #include <iterator>
> using namespace std;
>
> int main()
> {
>    int ia[3][4] = 
>    {
>		{ 0, 1, 2, 3 },
>		{ 4, 5, 6, 7 },
>		{ 8, 9, 10, 11 }
>	};
>
>    //vesion 1
>    for (const int(&row)[4] : ia)
>        for (int col : row)
>            cout << col << " ";
>    cout << endl;
>
>    //version 2
>    for (size_t i = 0; i < 3; i++)
>        for (size_t j = 0; j < 4; j++)
>            cout << ia[i][j] << " ";
>    cout << endl;
>
>    //version 3 
>    for (int(*row)[4] = begin(ia); row != end(ia); row++)
>        for (int *col = begin(*row); col != end(*row); ++ col)
>            cout << *col << " ";
>    cout << endl;
>
>    return 0;
> }
> ```

#### 练习3.44
改写上一个练习中的程序，使用类型别名来代替循环控制变量的类型。
> ```cpp
> #include <iostream>
> using std::cout; 
> using std::endl;
>
> int main()
> {
>	int ia[3][4] = 
>    {
>		{ 0, 1, 2, 3 },
>		{ 4, 5, 6, 7 },
>		{ 8, 9, 10, 11 }
>	};
>	using int_array = int[4];
>
>	for (int_array& p : ia)
>		for (int q : p)
>			cout << q << " ";
>	cout << endl;
>
>	for (size_t i = 0; i != 3; ++i)
>		for (size_t j = 0; j != 4; ++j)
>			cout << ia[i][j] << " ";
>	cout << endl;
>
>	for (int_array* p = ia; p != ia + 3; ++p)
>		for (int *q = *p; q != *p + 4; ++q)
>			cout << *q << " ";
>	cout << endl;
>
>	return 0;
> }
> ```

#### 练习3.45
再一次改写程序，这次使用`auto`关键字。
> ```cpp
> #include <iostream>
> using std::cout;
> using std::endl;
>
> int main()
> {
>	int ia[3][4] = 
>    {
>		{ 0, 1, 2, 3 },
>		{ 4, 5, 6, 7 },
>		{ 8, 9, 10, 11 }
>	};
>
>	for (auto& p : ia)
>		for (auto q : p)
>			cout << q << " ";
>	cout << endl;
>
>	for (auto i = 0; i != 3; ++i)
>		for (auto j = 0; j != 4; ++j)
>			cout << ia[i][j] << " ";
>	cout << endl;
>
>	for (auto p = ia; p != ia + 3; ++p)
>		for (auto q = *p; q != *p + 4; ++q)
>			cout << *q << " ";
>	cout << endl;
>
>	return 0;
> }
> ```


# 第四章 表达式
## 4.1 基础
### 4.1.1 基本概念

### 4.1.2 优先级和结合律
#### 练习4.1
表达式 5 + 10 * 20 / 2 的求值结果是多少？
> 105。

#### 练习4.2
根据4.12节中的表，在下述表达式的合理位置添加括号，使得添加括号后运算对象的组合顺序与添加
括号前一致。
```cpp
(a) *vec.begin()
(b) *vec.begin() + 1
```
> ```cpp
> *(vec.begin())
> (*(vec.begin())) + 1
> ``` 

### 4.1.3 求值顺序
#### 练习4.3 
C++语言没有明确规定大多数二元运算符的求值顺序，给编译器优化留下了余地。这种策略实际上是在代码生成效率和程序潜在缺陷之间进行了权衡，你认为这可以接受吗？请说出你的理由。
> 可以接受。`C++`的设计思想是尽可能地“相信”程序员，将效率最大化。然而这种思想却有着潜在的危害，就是无法控制程序员自身引发的错误。因此`Java`的诞生也是必然，`Java`的思想就是尽可能地“不相信”程序员。

## 4.2 算术运算符
#### 练习4.4
在下面的表达式中添加括号，说明其求值过程及最终结果。编写程序编译该（不加括号的）表达式并输出结果验证之前的推断。
```cpp
12 / 3 * 4 + 5 * 15 + 24 % 4 / 2
```
> `((12/3)*4) + (5*15) + ((24%4)/2)`

#### 练习4.5
写出下列表达式的求值结果。
```cpp
-30 * 3 + 21 / 5  // -90+4 = -86
-30 + 3 * 21 / 5  // -30+63/5 = -30+12 = -18
30 / 3 * 21 % 5   // 10*21%5 = 210%5 = 0
-30 / 3 * 21 % 4  // -10*21%4 = -210%4 = -2
```
> -86, -18, 0, -2

#### 练习4.6
写出一条表达式用于确定一个整数是奇数还是偶数。
> ```cpp
> if (i % 2 == 0) 
> {
>
> }
> ```

#### 练习4.7
溢出是何含义？写出三条将导致溢出的表达式。
> 当计算的结果超出该类型所能表示的范围时就会产生溢出。
```cpp
short svalue = 32767; ++svalue; // -32768
unsigned uivalue = 0; --uivalue;  // 4294967295
unsigned short usvalue = 65535; ++usvalue;  // 0
```

## 4.3 逻辑和关系运算符
#### 练习4.8
说明在逻辑与、逻辑或及相等性运算符中运算对象的求值顺序。
> - 逻辑与运算符和逻辑或运算符都是先求左侧运算对象的值再求右侧运算对象的值，当且仅当左侧运算对象无法确定表达式的结果时才会计算右侧运算对象的值。这种策略称为 **短路求值**。
> - 相等性运算符未定义求值顺序。

#### 练习4.9
解释在下面的`if`语句中条件部分的判断过程。
```cpp
const char *cp = "Hello World";
if (cp && *cp)
```
> 首先判断 `cp` ，`cp` 不是一个空指针，因此 `cp` 为真。然后判断 `*cp`，`*cp` 的值是字符`'H'`，非`0`。因此最后的结果为真。

#### 练习4.10
为`while`循环写一个条件，使其从标准输入中读取整数，遇到`42`时停止。
> ```cpp
> int i;
> while(cin >> i && i != 42)
> ```

#### 练习4.11
书写一条表达式用于测试4个值`a`、`b`、`c`、`d`的关系，确保`a`大于`b`、`b`大于`c`、`c`大于`d`。
> `a>b && b>c && c>d`


#### 练习4.12
假设i、j 和k 是三个整数，说明表达式 i != j < k 的含义。
> 这个表达式等价于 `i != (j < k)`。首先得到`j < k`的结果为`true`或`false`，转换为整数值是 1 和 0，然后判断`i`不等于 1 和 0 ，最终的结果为`bool`值。

## 4.4 赋值运算符
#### 练习4.13
在下述语句中，当赋值完成后`i`和`d`的值分别是多少？
```cpp
int i;   double d;
d = i = 3.5; // i = 3, d = 3.0
i = d = 3.5; // d = 3.5, i = 3
```

#### 练习4.14
执行下述 if 语句后将发生什么情况？
```cpp
if (42 = i)   // 编译错误。赋值运算符左侧必须是一个可修改的左值。而字面值是右值。
if (i = 42)   // true.
```

#### 练习4.15
下面的赋值是非法的，为什么？应该如何修改？
```cpp
double dval; int ival; int *pi;
dval = ival = pi = 0;
```
> `p`是指针，不能赋值给`int`，应该改为：
```cpp
dval = ival = 0;
pi = 0;
```

#### 练习4.16
尽管下面的语句合法，但它们实际执行的行为可能和预期并不一样，为什么？应该如何修改？
```cpp
(a)if (p = getPtr() != 0)
(b)if (i = 1024)
```
> 条件判断总是为`true`， 应该改为：
```cpp
if ((p=getPtr()) != 0)
if (i == 1024)
```

## 4.5 递增和递减运算符
#### 练习4.17
说明前置递增运算符和后置递增运算符的区别。
> 前置递增运算符将对象本身作为左值返回，而后置递增运算符将对象原始值的副本作为右值返回。

#### 练习4.18
如果132页那个输出`vector`对象元素的`while`循环使用前置递增运算符，将得到什么结果？
> 将会从第二个元素开始取值，并且最后对`v.end()`进行取值，结果是未定义的。

#### 练习4.19
假设`ptr`的类型是指向`int`的指针、`vec`的类型是`vector<int>`、`ival`的类型是`int`，说明下面的表达式是何含义？如果有表达式不正确，为什么？应该如何修改？
```cpp
(a)ptr != 0 && *ptr++  
(b)ival++ && ival
(c)vec[ival++] <= vec[ival] 
```
> - (a) 判断`ptr`不是一个空指针，并且`ptr`当前指向的元素的值也为真，然后将`ptr`指向下一个元素
> - (b) 判断`ival`的值为真，并且`(ival + 1)`的值也为真
> - (c) 表达式有误。C++并没有规定 `<=` 运算符两边的求值顺序，应该改为 `vec[ival] <= vec[ival+1]`
 
## 4.6 成员访问运算符
#### 练习4.20
假设`iter`的类型是`vector<string>::iterator`, 说明下面的表达式是否合法。如果合法，表达式的含义是什么？如果不合法，错在何处？
```cpp
(a) *iter++;
(b) (*iter)++;
(c) *iter.empty();
(d) iter->empty();
(e) ++*iter;
(f) iter++->empty();
```
> (a)合法。返回迭代器所指向的元素，然后迭代器递增。  
> (b)不合法。因为`vector`元素类型是`string`，没有`++`操作。  
> (c)不合法。这里应该加括号`(*iter).empty()`。  
> (d)合法。判断迭代器当前的元素是否为空。  
> (e)不合法。`string`类型没有`++`操作。  
> (f)合法。判断迭代器当前元素是否为空，然后迭代器递增。

## 4.7 条件运算符
#### 练习4.21
编写一段程序，使用条件运算符从`vector<int>`中找到哪些元素的值是奇数，然后将这些奇数值翻倍。
> ```cpp
> #include <iostream>
> #include <vector>
> using namespace std;
>
> int main()
> {
>    vector<int> ivec{1,4,5,6,235,422,45};
>
>    for (auto i : ivec)
>        cout << ((i % 2 == 1) ? i * 2 : i) << " ";
>    cout << endl;
>
>    return 0;
>    
> }
> ```

#### 练习4.22
本节的示例程序将成绩划分为`high pass`、`pass`和`fail`三种，扩展该程序使其进一步将`60`分到`75`分之间的成绩设定为`low pass`。要求程序包含两个版本：一个版本只使用条件运算符；另一个版本使用1个或多个`if`语句。哪个版本的程序更容易理解呢？为什么？
> 第二个版本容易理解。当条件运算符嵌套层数变多之后，代码的可读性急剧下降。而`if else`的逻辑很清晰。

#### 练习4.23
因为运算符的优先级问题，下面这条表达式无法通过编译。根据4.12节中的表指出它的问题在哪里？应该如何修改？
```cpp
string s = "word";
string pl = s + s[s.size() - 1] == 's' ? "" : "s" ;
```
> 加法运算符的优先级高于条件运算符。因此要改为：
> ```cpp
> string pl = s + (s[s.size() - 1] == 's' ? "" : "s") ;
> ```

#### 练习4.24
本节的示例程序将成绩划分为`high pass`、`pass`、和`fail`三种，它的依据是条件运算符满足右结合律。假如条件运算符满足的是左结合律，求值的过程将是怎样的？

> 如果条件运算符满足的是左结合律。那么
> ```cpp
> finalgrade = (grade > 90) ? "high pass" : (grade < 60) ? "fail" : "pass";
> ```
> 等同于
> ```cpp
> finalgrade = ((grade > 90) ? "high pass" : (grade < 60)) ? "fail" : "pass";
> ```
> 假如此时`grade > 90`，第一个条件表达式的结果是`"high pass"`，而字符串字面值的类型是`const char *`，非空所以为真。因此第二个条件表达式的结果是`"fail"`。这样就出现了自相矛盾的逻辑。

## 4.8 位运算符
#### 练习4.25
如果一台机器上`int`占 32 位、`char`占8位，用的是`Latin-1`字符集，其中字符`'q'`的二进制形式是`01110001`，那么表达式`'q' << 6`的值是什么？
> 首先将`char`类型提升为`int`类型，等同于`00000000 00000000 00000000 01110001 << 6`，结果是`00000000 00000000 00011100 01000000`，转换是十进制是`7232`。

#### 练习4.26
在本节关于测验成绩的例子中，如果使用`unsigned int`作为`quiz1`的类型会发生什么情况？
> 在有的机器上，`unsigned int`类型可能只有 16 位，因此结果是未定义的。

#### 练习4.27
下列表达式的结果是什么？
```cpp
unsigned long ul1 = 3, ul2 = 7;
(a) ul1 & ul2 
(b) ul1 | ul2 
(c) ul1 && ul2
(d) ul1 || ul2 
```

> (a) 3  
> (b) 7  
> (c) true  
> (d) ture  

## 4.9 sizeof运算符
#### 练习4.28
编写一段程序，输出每一种内置类型所占空间的大小。
> ```cpp
> #include <iostream> 
> using namespace std;
>
> int main()
> {
>	cout << "bool:\t\t" << sizeof(bool) << " bytes" << endl << endl;
>
>	cout << "char:\t\t" << sizeof(char) << " bytes" << endl;
>	cout << "wchar_t:\t" << sizeof(wchar_t) << " bytes" << endl;
>	cout << "char16_t:\t" << sizeof(char16_t) << " bytes" << endl;
>	cout << "char32_t:\t" << sizeof(char32_t) << " bytes" << endl << endl;
>
>	cout << "short:\t\t" << sizeof(short) << " bytes" << endl;
>	cout << "int:\t\t" << sizeof(int) << " bytes" << endl;
>	cout << "long:\t\t" << sizeof(long) << " bytes" << endl;
>	cout << "long long:\t" << sizeof(long long) << " bytes" << endl << endl;
>
>	cout << "float:\t\t" << sizeof(float) << " bytes" << endl;
>	cout << "double:\t\t" << sizeof(double) << " bytes" << endl;
>	cout << "long double:\t" << sizeof(long double) << " bytes" << endl << endl;
>
>	return 0;
> }
> ```

#### 练习4.29
推断下面代码的输出结果并说明理由。实际运行这段程序，结果和你想象的一样吗？如不一样，为什么？
```cpp
int x[10];   int *p = x;
cout << sizeof(x)/sizeof(*x) << endl;
cout << sizeof(p)/sizeof(*p) << endl;
```
> 第一个输出结果是 10。第二个结果是未定义。

#### 练习4.30
根据4.12节中的表，在下述表达式的适当位置加上括号，使得加上括号之后的表达式的含义与原来的含义相同。
```cpp
(a) sizeof x + y      
(b) sizeof p->mem[i]  
(c) sizeof a < b     
(d) sizeof f()  
```
> (a) `(sizeof x) + y`
> (b) `sizeof(p->mem[i])`
> (c) `sizeof(a) < b`
> (d) `sizeof(f())`

## 4.10 逗号运算符
#### 练习4.31
本节的程序使用了前置版本的递增运算符和递减运算符，解释为什么要用前置版本而不用后置版本。要想使用后置版本的递增递减运算符需要做哪些改动？使用后置版本重写本节的程序。
> 在4.5节（132页）已经说过了，**除非必须，否则不用递增递减运算符的后置版本**。在这里要使用后者版本的递增递减运算符不需要任何改动。

#### 练习4.32
解释下面这个循环的含义。
```cpp
constexpr int size = 5;
int ia[size] = { 1, 2, 3, 4, 5 };
for (int *ptr = ia, ix = 0;
    ix != size && ptr != ia+size;
    ++ix, ++ptr) { /* ... */ }
```  
> 这个循环在遍历数组`ia`，指针`ptr`和整型`ix`都是起到一个循环计数的功能。

#### 练习4.33
根据4.12节中的表说明下面这条表达式的含义。
```cpp
someValue ? ++x, ++y : --x, --y
```
> 逗号表达式的优先级是最低的。因此这条表达式也等于：
> ```cpp
> (someValue ? ++x, ++y : --x), --y
> ```
> 如果`someValue`的值为真，`x`和`y`的值都自增并返回`y`值，然后丢弃`y`值，`y`递减并返回`y`值。如果`someValue`的值为假，`x`递减并返回`x`值，然后丢弃`x`值，`y`递减并返回`y`值。

## 4.11 类型转换
### 4.11.1 算术转换
#### 练习4.34
根据本节给出的变量定义，说明在下面的表达式中奖发生什么样的类型转换：
```cpp
(a) if (fval)
(b) dval = fval + ival;
(c) dval + ival * cval;
```
需要注意每种运算符遵循的是左结合律还是右结合律。

> (a) `fval`转换为`bool`类型  
> (b) `ival`转换为`float`，相加的结果转换为`double`  
> (c) `cval`转换为`int`，然后相乘的结果转换为`double`

#### 练习4.35
假设有如下的定义：
```cpp
char cval;
int ival;
unsigned int ui;
float fval;
double dval;
```
请回答在下面的表达式中发生了隐式类型转换吗？如果有，指出来。
```cpp
(a) cval = 'a' + 3;
(b) fval = ui - ival * 1.0;
(c) dval = ui * fval;
(d) cval = ival + fval + dval;
```

> (a) `'a'`转换为`int`，然后与`3`相加的结果转换为`char`  
> (b) `ival`转换为`double``ui`转换为`double`，结果转换为`float`  
> (c) `ui`转换为`float`，结果转换为`double`  
> (d) `ival`转换为`float`，与`fval`相加后的结果转换为`double`，最后的结果转换为`char`

### 4.11.3 显示转换
#### 练习4.36
假设`i`是`int`类型，`d`是`double`类型，书写表达式`i*=d`使其执行整数类型的乘法而非浮点类型的乘法。
> ```cpp
> i *= static_cast<int>(d);
> ```

#### 练习4.37
用命名的强制类型转换改写下列旧式的转换语句。
```cpp
int i; double d; const string *ps; char *pc; void *pv;
(a) pv = (void*)ps;
(b) i = int(*pc);
(c) pv = &d;
(d) pc = (char*)pv;
```
> ```cpp
> (a) pv = static_cast<void*>(const_cast<string*>(ps));  
> (b) i = static_cast<int>(*pc);  
> (c) pv = static_cast<void*>(&d);  
> (d) pc = static_cast<char*>(pv);
> ```

#### 练习4.38
说明下面这条表达式的含义。
```cpp
double slope = static_cast<double>(j/i);
```
> 将`j/i`的结果值转换为`double`，然后赋值给`slope`。 


# 第五章 语句
## 5.1 简单语句
#### 练习5.1
什么是空语句？什么时候会用到空语句？
> - 只含义一个单独的分号的语句是空语句。  
> - 如果在程序的某个地方，语法上需要一条语句但是逻辑上不需要，此时应该使用空语句。

#### 练习5.2
什么是块？什么时候会用到块？
> - 用花括号括起来的语句和声明的序列就是块。
> - 如果在程序的某个地方，语法上需要一条语句，而逻辑上需要多条语句，此时应该使用块

#### 练习5.3
使用逗号运算符重写1.4.1节的 while 循环，使它不再需要块，观察改写之后的代码可读性提高了还是降低了。
> ```cpp
> while (val <= 10)
>    sum += val, ++val;
> ```
> 代码的可读性反而降低了。

## 5.2 语句作用域
#### 练习5.4
说明下列例子的含义，如果存在问题，试着修改它。
```cpp
(a) while (string::iterator iter != s.end()) { /* . . . */ }
(b) while (bool status = find(word)) { /* . . . */ }
		if (!status) { /* . . . */ }
```
> (a) 这个循环试图用迭代器遍历`string`，但是变量的定义应该放在循环的外面，目前每次循环都会重新定义一个变量，明显是错误的。  
> (b) 这个循环的`while`和`if`是两个独立的语句，`if`语句中无法访问`status`变量，正确的做法是应该将`if`语句包含在`while`里面。

## 5.3 条件语句
### 5.3.1 if语句
#### 练习5.5
写一段自己的程序，使用`if else`语句实现把数字转换为字母成绩的要求。
> ```cpp
> #include <iostream>
> #include <vector>
> #include <string>
> using std::vector; 
> using std::string; 
> using std::cout; 
> using std::endl; 
>
> int main()
> {
>	vector<string> scores = { "F", "D", "C", "B", "A", "A++" };
>	int g = 0;
>	while (cin >> g)
>	{
>		string letter;
>		if (g < 60)
>			letter = scores[0];
>		else
>		{
>			letter = scores[(g - 50) / 10];
>			if (g != 100)
>				letter += g % 10 > 7 ? "+" : g % 10 < 3 ? "-" : "";
>			cout << letter << endl;
>		}
>	}
>	return 0;
> }
> ```

#### 练习5.6
改写上一题的程序，使用条件运算符代替`if else`语句。
> ```cpp
> #include <iostream>
> #include <vector>
> #include <string>
> using std::vector; 
> using std::string; 
> using std::cout; 
> using std::endl; 
> using std::cin;
>
> int main()
> {
>	vector<string> scores = { "F", "D", "C", "B", "A", "A++" };
>	int grade = 0;
>	while (cin >> grade)
>	{
>		string lettergrade = grade < 60 ? scores[0] : scores[(grade - 50) / 10];
>		lettergrade += (grade == 100 || grade < 60) ? "" : (grade % 10 > 7) ? "+" : (grade % 10 < 3) ? "-" : "";
>		cout << lettergrade << endl;
>	}
>	return 0;
> }
> ```

#### 练习5.7
改写下列代码段中的错误。
```cpp
(a) if (ival1 != ival2) 
		ival1 = ival2
    else 
    	ival1 = ival2 = 0;
(b) if (ival < minval) 
		minval = ival;
    	occurs = 1;
(c) if (int ival = get_value())
    	cout << "ival = " << ival << endl;
    if (!ival)
    	cout << "ival = 0\n";
(d) if (ival = 0)
    	ival = get_value();
```

> (a) `ival1 = ival2` 后面少了分号。  
> (b) 应该用花括号括起来。  
> (c) `if (!ival)` 应该改为 `else`。  
> (d) `if (ival = 0)` 应该改为 `if (ival == 0)`。  

#### 练习5.8
什么是“悬垂`else`”？C++语言是如何处理`else`子句的？
> C++语言规定`else`与它最近的尚未匹配的`if`匹配。

### 5.3.2 switch语句
#### 练习5.9
编写一段程序，使用一系列`if`语句统计从`cin`读入的文本中有多少元音字母。
> ```cpp
> #include <iostream>
> using std::cout; 
> using std::endl; 
> using std::cin;
>
> int main()
> {
>	unsigned aCnt = 0, eCnt = 0, iCnt = 0, oCnt = 0, uCnt = 0;
>	char ch;
>	while (cin >> ch)
>	{
>		if (ch == 'a') ++aCnt;
>		else if (ch == 'e') ++eCnt;
>		else if (ch == 'i') ++iCnt;
>		else if (ch == 'o') ++oCnt;
>		else if (ch == 'u') ++uCnt;
>	}
>	cout << "Number of vowel a: \t" << aCnt << '\n'
>		<< "Number of vowel e: \t" << eCnt << '\n'
>		<< "Number of vowel i: \t" << iCnt << '\n'
>		<< "Number of vowel o: \t" << oCnt << '\n'
>		<< "Number of vowel u: \t" << uCnt << endl;
>	return 0;
> }
> ```

#### 练习5.10
我们之前实现的统计元音字母的程序存在一个问题：如果元音字母以大写形式出现，不会被统计在内。编写一段程序，既统计元音字母的小写形式，也统计元音字母的大写形式，也就是说，新程序遇到`'a'`和`'A'`都应该递增`aCnt`的值，以此类推。
> ```cpp
> #include <iostream>
> using std::cin; 
> using std::cout; 
> using std::endl;
> int main()
> {
>	unsigned aCnt = 0, eCnt = 0, iCnt = 0, oCnt = 0, uCnt = 0;
>	char ch;
>	while (cin >> ch)
>		switch (ch)
>	{
>		case 'a':
>		case 'A':
>			++aCnt;
>			break;
>		case 'e':
>		case 'E':
>			++eCnt;
>			break;
>		case 'i':
>		case 'I':
>			++iCnt;
>			break;
>		case 'o':
>		case 'O':
>			++oCnt;
>			break;
>		case 'u':
>		case 'U':
>			++uCnt;
>			break;
>	}
>	cout << "Number of vowel a(A): \t" << aCnt << '\n'
>		<< "Number of vowel e(E): \t" << eCnt << '\n'
>		<< "Number of vowel i(I): \t" << iCnt << '\n'
>		<< "Number of vowel o(O): \t" << oCnt << '\n'
>		<< "Number of vowel u(U): \t" << uCnt << endl;
>	return 0;
> }
> ```

#### 练习5.11
修改统计元音字母的程序，使其也能统计空格、制表符、和换行符的数量。
> ```cpp
> #include <iostream>
> using std::cin; 
> using std::cout; 
> using std::endl;
>
> int main()
> {
>	unsigned aCnt = 0, eCnt = 0, iCnt = 0, oCnt = 0, uCnt = 0, spaceCnt = 0, tabCnt = 0, newLineCnt = 0;
>	char ch;
>	while (cin >> std::noskipws >> ch)//不忽略空白字符，将其读取
>		switch (ch)
>	{
>		case 'a':
>		case 'A':
>			++aCnt;
>			break;
>		case 'e':
>		case 'E':
>			++eCnt;
>			break;
>		case 'i':
>		case 'I':
>			++iCnt;
>			break;
>		case 'o':
>		case 'O':
>			++oCnt;
>			break;
>		case 'u':
>		case 'U':
>			++uCnt;
>			break;
>		case ' ':
>			++spaceCnt;
>			break;
>		case '\t':
>			++tabCnt;
>			break;
>		case '\n':
>			++newLineCnt;
>			break;
>	}
>	cout << "Number of vowel a(A): \t" << aCnt << '\n'
>		<< "Number of vowel e(E): \t" << eCnt << '\n'
>		<< "Number of vowel i(I): \t" << iCnt << '\n'
>		<< "Number of vowel o(O): \t" << oCnt << '\n'
>		<< "Number of vowel u(U): \t" << uCnt << '\n'
>		<< "Number of space: \t" << spaceCnt << '\n'
>		<< "Number of tab char: \t" << tabCnt << '\n'
>		<< "Number of new line: \t" << newLineCnt << endl;
>	return 0;
> }
> ```

#### 练习5.12
修改统计元音字母的程序，使其能统计含以下两个字符的字符序列的数量： `ff`、`fl`和`fi`。
> ```cpp
> #include <iostream>
> using std::cin; 
> using std::cout; 
> using std::endl;
>
> int main()
> {
>	unsigned aCnt = 0, eCnt = 0, iCnt = 0, oCnt = 0, uCnt = 0, spaceCnt = 0, tabCnt = 0, newLineCnt = 0, ffCnt = 0, flCnt = 0, fiCnt = 0;
>	char ch, prech = '\0';
>	while (cin >> std::noskipws >> ch)
>	{
>		switch (ch)
>		{
>		case 'a':
>		case 'A':
>			++aCnt;
>			break;
>		case 'e':
>		case 'E':
>			++eCnt;
>			break;
>		case 'i':
>			if (prech == 'f') ++fiCnt;
>		case 'I':
>			++iCnt;
>			break;
>		case 'o':
>		case 'O':
>			++oCnt;
>			break;
>		case 'u':
>		case 'U':
>			++uCnt;
>			break;
>		case ' ':
>			++spaceCnt;
>			break;
>		case '\t':
>			++tabCnt;
>			break;
>		case '\n':
>			++newLineCnt;
>			break;
>		case 'f':
>			if (prech == 'f') ++ffCnt;
>			break;
>		case 'l':
>			if (prech == 'f') ++flCnt;
>			break;
>		}
>		prech = ch;
>	}
>	cout << "Number of vowel a(A): \t" << aCnt << '\n'
>		<< "Number of vowel e(E): \t" << eCnt << '\n'
>		<< "Number of vowel i(I): \t" << iCnt << '\n'
>		<< "Number of vowel o(O): \t" << oCnt << '\n'
>		<< "Number of vowel u(U): \t" << uCnt << '\n'
>		<< "Number of space: \t" << spaceCnt << '\n'
>		<< "Number of tab char: \t" << tabCnt << '\n'
>		<< "Number of new line: \t" << newLineCnt << '\n'
>		<< "Number of ff: \t" << ffCnt << '\n'
>		<< "Number of fl: \t" << flCnt << '\n'
>		<< "Number of fi: \t" << fiCnt << endl;
>	return 0;
> }
> ```

#### 练习5.13
下面显示的每个程序都含有一个常见的编码错误，指出错误在哪里，然后修改它们。
```cpp
(a) unsigned aCnt = 0, eCnt = 0, iouCnt = 0;
    char ch = next_text();
    switch (ch) {
        case 'a': aCnt++;
        case 'e': eCnt++;
        default: iouCnt++;
    }
(b) unsigned index = some_value();
    switch (index) {
        case 1:
            int ix = get_value();
            ivec[ ix ] = index;
            break;
        default:
            ix = ivec.size()-1;
            ivec[ ix ] = index;
    }
(c) unsigned evenCnt = 0, oddCnt = 0;
    int digit = get_num() % 10;
    switch (digit) {
        case 1, 3, 5, 7, 9:
            oddcnt++;
            break;
        case 2, 4, 6, 8, 10:
            evencnt++;
            break;
    }
(d) unsigned ival=512, jval=1024, kval=4096;
    unsigned bufsize;
    unsigned swt = get_bufCnt();
    switch(swt) {
        case ival:
            bufsize = ival * sizeof(int);
            break;
        case jval:
            bufsize = jval * sizeof(int);
            break;
        case kval:
            bufsize = kval * sizeof(int);
            break;
    }
```
> (a) 少了`break`语句。应该为：
> ```cpp
>	unsigned aCnt = 0, eCnt = 0, iouCnt = 0;
>   char ch = next_text();
>    switch (ch) {
>    	case 'a': aCnt++; break;
>    	case 'e': eCnt++; break;
>    	default: iouCnt++; break;
>    }
> ```
> (b) 在`default`分支当中，`ix`未定义。应该在外部定义ix。
> ```cpp
>    unsigned index = some_value();
>    int ix;
>    switch (index) {
>        case 1:
>            ix = get_value();
>            ivec[ ix ] = index;
>            break;
>        default:
>            ix = static_cast<int>(ivec.size())-1;
>            ivec[ ix ] = index;
>    }
> ```
> (c)`case`后面应该用冒号而不是逗号。
> ```cpp
>    unsigned evenCnt = 0, oddCnt = 0;
>    int digit = get_num() % 10;
>    switch (digit) {
>        case 1: case 3: case 5: case 7: case 9:
>            oddcnt++;
>            break;
>        case 2: case 4: case 6: case 8: case 0:
>            evencnt++;
>            break;
>    }
> ```
> (d) `case`标签必须是整型常量表达式。
> ```cpp
>    const unsigned ival=512, jval=1024, kval=4096;
>    unsigned bufsize;
>    unsigned swt = get_bufCnt();
>    switch(swt) {
>        case ival:
>            bufsize = ival * sizeof(int);
>            break;
>        case jval:
>            bufsize = jval * sizeof(int);
>            break;
>        case kval:
>            bufsize = kval * sizeof(int);
>            break;
>    }
> ```

## 5.4 迭代语句
### 5.4.1 while语句
#### 练习5.14
编写一段程序，从标准输入中读取若干`string`对象并查找连续重复出现的单词，所谓连续重复出现的意思是：一个单词后面紧跟着这个单词本身。要求记录连续重复出现的最大次数以及对应的单词。如果这样的单词存在，输出重复出现的最大次数；如果不存在，输出一条信息说明任何单词都没有连续出现过。例如：如果输入是：`how now now now brown cow cow`
那么输出应该表明单词`now`连续出现了`3`次。
> ```cpp
> #include <iostream>
> #include <string>
> using std::cout;
> using std::cin; 
> using std::endl; 
> using std::string; 
> using std::pair;
> 
> int main()
> {
>	pair<string, int> max_duplicated;
>	int count = 0;
>	for (string str, prestr; cin >> str; prestr = str)
>	{
>		if (str == prestr) 
>			++count;
>		else 
>			count = 0;
>		if (count > max_duplicated.second) 
>			max_duplicated = { prestr, count };
>	}
>
>	if (max_duplicated.first.empty()) 
>		cout << "There's no duplicated string." << endl;
>	else 
>		cout << "the word " << max_duplicated.first << " occurred " << max_duplicated.second + 1 << " times. " << endl;
>	return 0;
> }
> ```

### 5.4.2 传统的for语句
#### 练习5.15
说明下列循环的含义并改正其中的错误。
```cpp
(a) for (int ix = 0; ix != sz; ++ix) { /* ... */ }
    if (ix != sz)
    	// . . .
(b) int ix;
    for (ix != sz; ++ix) { /* ... */ }
(c) for (int ix = 0; ix != sz; ++ix, ++sz) { /*...*/ }
```
> 应该改为下面这样：
> ```cpp
> (a) int ix;
>    for (ix = 0; ix != sz; ++ix)  { /* ... */ }
>    if (ix != sz)
>    // . . .
> (b) int ix;
>     for (; ix != sz; ++ix) { /* ... */ }
> (c) for (int ix = 0; ix != sz; ++ix) { /*...*/ }
> ```

#### 练习5.16
`while`循环特别适用于那种条件不变、反复执行操作的情况，例如，当未达到文件末尾时不断读取下一个值。`for`循环更像是在按步骤迭代，它的索引值在某个范围内一次变化。根据每种循环的习惯各自编写一段程序，然后分别用另一种循环改写。如果只能使用一种循环，你倾向于哪种？为什么？
> ```cpp
> for (int i = 0; i != size; ++i)
>    // ...
>
> int i = 0;
> while (i != size)
> {
>    // ...
>    ++i;
> }
> ```
> 如果只能用一种循环，我会更倾向使用`for`，因为`for`循环的循环体在括号内更清晰直观。

#### 练习5.17
假设有两个包含整数的`vector`对象，编写一段程序，检验其中一个`vector`对象是否是另一个的前缀。为了实现这一目标，对于两个不等长的`vector`对象，只需挑出长度较短的那个，把它的所有元素和另一个`vector`对象比较即可。例如，如果两个`vector`对象的元素分别是`0、1、1、2`和`0、1、1、2、3、5、8`，则程序的返回结果为真。
> ```cpp
> #include <iostream>
> #include <vector>
> using std::cout; 
> using std::vector;
>
> bool is_prefix(const vector<int>& lhs, const vector<int>& rhs)
> {
>	if (lhs.size() > rhs.size())
>		return is_prefix(rhs, lhs);
>	for (unsigned i = 0; i != lhs.size(); ++i)
>		if (lhs[i] != rhs[i]) 
>			return false;
>	return true;
> }
>
> int main()
> {
>	vector<int> l{ 0, 1, 1, 2 };
>	vector<int> r{ 0, 1, 1, 2, 3, 5, 8 };
>	cout << (is_prefix(r, l) ? "yes\n" : "no\n");
>	return 0;
> }
> ```

### 5.4.3 范围for语句

### 5.4.4 do while语句
#### 练习5.18
说明下列循环的含义并改正其中的错误。
```cpp
(a) do { // 应该添加花括号
        int v1, v2;
        cout << "Please enter two numbers to sum:" ;
        if (cin >> v1 >> v2)
            cout << "Sum is: " << v1 + v2 << endl;
    }while (cin);
(b) int ival;
    do {
        // . . .
    } while (ival = get_response()); // 应该将ival 定义在循环外
(c) int ival = get_response();
    do {
        ival = get_response();
    } while (ival); // 应该将ival 定义在循环外
```

#### 练习5.19
编写一段程序，使用`do while`循环重复地执行下述任务：首先提示用户输入两个`string`对象，然后挑出较短的那个并输出它。
> ```cpp
> #include <iostream>
> #include <string>
> using std::cout;
> using std::cin; 
> using std::endl; 
> using std::string;
>
> int main()
> {
>	string choice;
>	do
>	{
>		cout << "Input two strings: ";
>		string str1, str2;
>		cin >> str1 >> str2;
>		cout << (str1 <= str2 ? str1 : str2)
>			<< " is less than the other. " << "\n\n"
>			<< "More? Enter yes or no: ";
>		cin >> choice;
>	} while (tolower(choice[0]) == 'y');
>	return 0;
> }
> ```

## 5.5 跳转语句
### 5.5.1 break语句
#### 练习5.20
编写一段程序，从标准输入中读取`string`对象的序列直到连续出现两个相同的单词或者所有的单词都读完为止。使用`while`循环一次读取一个单词，当一个单词连续出现两次时使用`break`语句终止循环。输出连续重复出现的单词，或者输出一个消息说明没有任何单词是连续重复出现的。
> ```cpp
> #include <iostream>
> #include <string>
> using std::cout;
> using std::cin; 
> using std::endl; 
> using std::string;
>
> int main()
> {
>	string read, tmp;
>	while (cin >> read)
>		if (read == tmp) 
>			break; 
>		else 
>			tmp = read;
>
>	if (cin.eof())  
>		cout << "no word was repeated." << endl;
>	else            
>		cout << read << " occurs twice in succession." << endl;
>	return 0;
> }
> ```

### 5.5.2 continue语句
#### 练习5.21
修改5.5.1节练习题的程序，使其找到的重复单词必须以大写字母开头。
> ```cpp
> #include <iostream>
> #include <string>
> using namespace std;
>
> int main()
> {
>	string curr, prev;
>	bool twice = false;
>	while (cin >> curr)
>	{
>		if (isupper(curr[0]) && prev == curr)
>		{
>			cout << curr << ": occurs twice in succession." << endl;
>			twice = true;
>			break;
>		}
>		prev = curr;
>	}
>	if (!twice)
>		cout << "no word was repeated." << endl;
>	return 0;
> }
> ```

### 5.5.3 goto语句
#### 练习5.22
本节的最后一个例子跳回到`begin`，其实使用循环能更好的完成该任务，重写这段代码，注意不再使用`goto`语句。
> ```cpp
> for (int sz = get_size(); sz <=0; sz = get_size())
>    ;
> ```

## 5.6 try语句块和异常处理
### 5.6.1 throw表达式

### 5.6.2 try语句块

### 5.6.3 标准异常
#### 练习5.23
编写一段程序，从标准输入读取两个整数，输出第一个数除以第二个数的结果。
> ```cpp
> #include <iostream>
> using std::cin;
> using std::cout;
> using std::endl;
>
> int main()
> {
>	int i, j;
>	cin >> i >> j;
>	cout << i / j << endl;
>
>	return 0;
> }
> ```


#### 练习5.24
修改你的程序，使得当第二个数是`0`时抛出异常。先不要设定`catch`子句，运行程序并真的为除数输入`0`，看看会发生什么？
> ```cpp
> #include <iostream>
> #include <stdexcept>
> using std::cin;
> using std::cout;
> using std::endl;
> using std::runtime_error;
> 
> int main(void)
> {
>	int i, j;
>	cin >> i >> j;
>	if (j == 0)
>		throw runtime_error("divisor is 0");
>	cout << i / j << endl;
>
>	return 0;
> }
> ```


#### 练习5.25
修改上一题的程序，使用`try`语句块去捕获异常。`catch`子句应该为用户输出一条提示信息，询问其是否输入新数并重新执行`try`语句块的内容。
> ```cpp
> #include <iostream>
> #include <stdexcept>
> using std::cin;
> using std::cout; 
> using std::endl; 
> using std::runtime_error;
>
> int main()
> {
>	int i, j;
>	cout << "please input tow numbers: " << endl;
>	while (cin >> i >> j)
>	{
>		try
>		{
>			if (j == 0)
>				throw runtime_error("divisor is 0");
>			cout << i / j << endl;
>		}
>		catch (runtime_error err)
>		{
>			cout << err.what() << "\nTry Again? Enter y or n" << endl;
>			char c;
>			cin >> c;
>			if (c != 'y')
>				break;
>		}
>		cout << "please input tow numbers: " << endl;
>	}
>
>	return 0;
> }
> ```


# 第六章 函数
## 6.1 函数基础
#### 练习6.1
实参和形参的区别的什么？
> 实参是函数调用的实际值，是形参的初始值。

#### 练习6.2
请指出下列函数哪个有错误，为什么？应该如何修改这些错误呢？
```cpp
(a) int f() {
          string s;
          // ...
          return s;
    }
(b) f2(int i) { /* ... */ }
(c) int calc(int v1, int v1)  /* ... */ }
(d) double square (double x)  return x * x; 
```
> 应该改为下面这样：
> ```cpp
> (a) string f() {
>          string s;
>          // ...
>          return s;
>    }
> (b) void f2(int i) { /* ... */ }
> (c) int calc(int v1, int v2) { /* ... */ }
> (d) double square (double x) { return x * x; }
> ```

#### 练习6.3
编写你自己的`fact`函数，上机检查是否正确。
> ```cpp
> #include <iostream>
> int fact(int i)
> {
>	if (i > 1)
>		return 1;
>	else
>		return i * fact(i - 1);
> }
> int main()
> {
>	std::cout << fact(5) << std::endl;
>	return 0;
> }
> ```

#### 练习6.4
编写一个与用户交互的函数，要求用户输入一个数字，计算生成该数字的阶乘。在`main`函数中调用该函数。
> ```cpp
> #include <iostream>
> #include <string>
> using namespace std;
> 
> int fact(int i)
> {
>	if (i > 1)
>		return 1;
>	else
>		return i * fact(i - 1);
> }
> 
> int main(){
>	string const prompt = "Enter a number :\n";
>	for (int i; cout << prompt, cin >> i;)
>	{
>		cout << fact(i) << endl;
>	}
>	return 0;
> }
> ```

#### 练习6.5
编写一个函数输出其实参的绝对值。
> ```cpp
> int abs(int i)
> {
>    return i > 0 ? i : -i;
> }
> ```

### 6.1.1 局部对象
说明形参、局部变量以及局部静态变量的区别。编写一个函数，同时达到这三种形式。
> 形参定义在函数形参列表里面  
> 局部变量定义在代码块里面  
> 局部静态变量在程序的执行路径第一次经过对象定义语句时初始化，并且直到程序终止时才被销毁。

#### 练习6.7
编写一个函数，当它第一次被调用时返回`0`，以后每次被调用返回值加`1`。
> ```cpp
> int ascending()
> {
> 	static int num = 0;
>	return num++;
> }
> ```

### 6.1.2 函数声明
#### 练习6.8
编写一个名为`Chapter6.h`的头文件，令其包含6.1节练习中的函数。
> ```cpp
> int fact(int val);
> int func();
> 
> template <typename T>
> T abs(T i)
> {
>	return i >= 0 ? i : -i;
> }
> ```

### 6.1.3 分离式编译

## 6.2参数传递
### 6.2.1 传值参数
#### 练习6.10
编写一个函数，使用指针形参交换两个整数的值。在代码中调用该函数并输出交换后的结果，以此验证函数的正确性。
> ```cpp
> #include <iostream>
> using std::cout;
> using std::cin;
> using std::endl;
>
> void swap(int* a, int* b)
> {
>	int tmp;
>	tmp = *a;
>	*a = *b;
>	*b = tmp;
> }
>
> int main()
> {
>	int a, b;
>	cout << "Please enter the numbers: \n";
>	cin >> a >> b;
>
>	swap(&a, &b)
>	cout << a << " " << b << endl;
>
>	return 0;
> }
> ```

### 6.2.2 传引用参数
#### 练习6.11]
编写并验证你自己的`reset`函数，使其作用于引用类型的参数。
> ```cpp
> void reset(int &i)
> {
>	i = 0;
> }
> ```

#### 练习6.12
改写6.2.1节练习中的程序，使其引用而非指针交换两个整数的值。你觉得哪种方法更易于使用呢？为什么？
> ```cpp
> void swap(int& a, int& b)
> {
>	int tmp;
>	tmp = a;
>	a = b;
>	b = tmp;
> }
>
> int main()
> {
>	int a, b;
>	cout << "Please enter the numbers: \n";
>	cin >> a >> b;
>
>	swap(a, b)
>	cout << a << " " << b << endl;
>
>	return 0;
> }
> ```
> 引用更好。

#### 练习6.13
假设`T`是某种类型的名字，说明以下两个函数声明的区别：一个是`void f(T)`, 另一个是`void f(&T)`。
> `void f(T)`的参数通过值传递，在函数中`T`是实参的拷贝，改变`T`不会影响到原来的实参。  
> `void f(&T)`的参数通过引用传递，在函数中的`T`是实参的引用，`T`的改变也就是实参的改变。

#### 练习6.14
举一个形参应该是引用类型的例子，再举一个形参不能是引用类型的例子。
> 例如交换两个整数的函数，形参应该是引用
> ```cpp
> void swap(int& lhs, int& rhs)
> {
>	int temp = lhs;
>	lhs = rhs;
>	rhs = temp;
> }
> ```
> 当实参的值是右值时，形参不能为引用类型
> ```cpp
> int add(int a, int b)
> {
>	return a + b;
> }
> ```

#### 练习6.15
说明`find_char`函数中的三个形参为什么是现在的类型，特别说明为什么`s`是常量引用而`occurs`是普通引用？为什么`s`和`occurs`是引用类型而`c`不是？如果令`s`是普通引用会发生什么情况？如果令`occurs`是常量引用会发生什么情况？
> 因为字符串可能很长，因此使用引用避免拷贝；而在函数中我们不希望改变`s`的内容，所以令`s`为常量。  
> `occurs`是要传到函数外部的变量，所以使用引用，`occurs`的值会改变，所以是普通引用。
> 因为我们只需要`c`的值，这个实参可能是右值(右值实参无法用于引用形参)，所以`c`不能用引用类型。
> 如果`s`是普通引用，也可能会意外改变原来字符串的内容。
> `occurs`如果是常量引用，那么意味着不能改变它的值，那也就失去意义了。

### 6.2.3 const形参和实参
#### 练习6.16
下面的这个函数虽然合法，但是不算特别有用。指出它的局限性并设法改善。
```cpp
bool is_empty(string& s) { return s.empty(); }
```
> 局限性在于**常量字符串**和**字符串字面值**无法作为该函数的实参，如果下面这样调用是非法的：
> ```cpp
> const string str;
> bool flag = is_empty(str); //非法
> bool flag = is_empty("hello"); //非法
> ```
> 所以要将这个函数的形参定义为常量引用：
> ```cpp
> bool is_empty(const string& s) { return s.empty(); }
> ```

#### 练习6.17
编写一个函数，判断`string`对象中是否含有大写字母。编写另一个函数，把`string`对象全部改写成小写形式。在这两个函数中你使用的形参类型相同吗？为什么？
> 两个函数的形参不一样。第一个函数使用常量引用，第二个函数使用普通引用。
> ```cpp
> bool any_capital(string const& str)
> {
> 	for (auto ch : str)
> 		if (isupper(ch)) return true;
> 	return false;
> }
> void to_lowercase(string& str)
> {
> 	for (auto& ch : str) ch = tolower(ch);
> }
> ```

#### 练习6.18
为下面的函数编写函数声明，从给定的名字中推测函数具备的功能。
- (a) 名为`compare`的函数，返回布尔值，两个参数都是`matrix`类的引用。 
- (b) 名为`change_val`的函数，返回`vector<int>`的迭代器，有两个参数：一个是`int`，另一个是`vector<int>`的迭代器。
> ```cpp
> (a) bool compare(matrix &m1, matrix &m2);
> (b) vector<int>::iterator change_val(int, vector<int>::iterator);
> ```

#### 练习6.19
假定有如下声明，判断哪个调用合法、哪个调用不合法。对于不合法的函数调用，说明原因。
```cpp
double calc(double);
int count(const string &, char);
int sum(vector<int>::iterator, vector<int>::iterator, int);
vector<int> vec(10);
(a) calc(23.4, 55.1);
(b) count("abcda",'a');
(c) calc(66);
(d) sum(vec.begin(), vec.end(), 3.8);
```
> - (a) 不合法。calc只有一个参数。
> - (b) 合法。
> - (c) 合法。
> - (d) 合法。

#### 练习6.20
引用形参什么时候应该是常量引用？如果形参应该是常量引用，而我们将其设为了普通引用，会发生什么情况？
> 应该尽量将引用形参设为常量引用，除非有明确的目的是为了改变这个引用变量。如果形参应该是常量引用，而我们将其设为了普通引用，那么常量实参将无法作用于普通引用形参。


### 6.2.4 数组形参
#### 练习6.21
编写一个函数，令其接受两个参数：一个是`int`型的数，另一个是`int`指针。函数比较`int`的值和指针所指的值，返回较大的那个。在该函数中指针的类型应该是什么？
> 应该是 `const int *` 类型。
> ```cpp
> #include <iostream>
> using std::cout;
> 
> int larger_one(int i, const int *p)
> {
> 	 return (i > *p) ? i : *p;
> }
> int main()
> {
> 	 int i = 6;
> 	 cout << larger_one(7, &i);
> 	 return 0;
> }
> ```

#### 练习6.22
编写一个函数，令其交换两个`int`指针。
> ```cpp
> #include <iostream>
> #include <string>
> void swap(int*& lft, int*& rht)
> {
>	auto tmp = lft;
>	lft = rht;
>	rht = tmp;
> }
> int main()
> {
>	int i = 42, j = 99;
>	auto lft = &i;
>	auto rht = &j;
>	swap(lft, rht);
>	std::cout << *lft << " " << *rht << std::endl;
>	return 0;
> }
> ```

#### 练习6.23
参考本节介绍的几个`print`函数，根据理解编写你自己的版本。依次调用每个函数使其输入下面定义的`i`和`j`:
```cpp
int i = 0, j[2] = { 0, 1 };
```
> ```cpp
> #include <iostream>
> using std::cout; 
> using std::endl; 
> using std::begin; 
> using std::end;
>
> void print(int i)
> {
>	cout << i << endl;
> }
>
> void print(const int *beg, const int *end)
> {
>	while (beg != end)
>		cout << *beg++ << endl;
> }
>
> void print(const int ia[], size_t size)
> {
>	for (size_t i = 0; i != size; ++i)
>	{
>		cout << ia[i] << endl;
>	}
> }
>
> void print(int (&arr)[2])
> {
>	for (auto i : arr)
>		cout << i << endl;
> }
>
> int main()
> {
>	int i = 0, j[2] = { 0, 1 };
>
>	print(i);
>	print(begin(j), end(j));
>	print(j, end(j) - begin(j));
>	print(j);
>
>	return 0;
> }
> ```

#### 练习6.24
描述下面这个函数的行为。如果代码中存在问题，请指出并改正。
```cpp
void print(const int ia[10])
{
	for (size_t i = 0; i != 10; ++i)
		cout << ia[i] << endl;
}
```
> 当数组作为实参的时候，会被自动转换为指向首元素的指针。因此函数形参接受的是一个指针。如果要让这个代码成功运行，可以将实参改为数组的引用。
> ```cpp
> void print(const int (&ia)[10])
> {
>	for (size_t i = 0; i != 10; ++i)
>		cout << ia[i] << endl;
> }
> ```

### 6.2.5 main：处理命令行选项
#### 练习6.25
编写一个`main`函数，令其接收两个实参。把实参的内容连接成一个`string`对象并输出出来。
> ```cpp
> #include <iostream>
> #include <string>
> using std::cout;
> using std::string;
> using std::endl;
>
> int main(int argc, char const *argv[])
> {
>    string s;
>    for (int i = 1; i != argc; ++i)
>		s += string(argv[i]) + " ";
>    cout << s;
>    return 0;
> }
> ```

#### 练习6.26
编写一个程序，使其接收本节所示的选项；输出传递给`main`函数的实参的内容。
> 同上

### 6.2.6 含有可变形参的函数
#### 练习6.27
编写一个函数，它的参数是`initializer_list<int>`类型的对象，函数的功能是计算列表中所有元素的和。
> ```cpp
> #include <iostream>
> #include <initializer_list>
>
> int sum(std::initializer_list<int> const& il)
> {
>	int sum = 0;
>	for (auto i : il) 
>		sum += i;
>	return sum;
> }
> int main(void)
> {
>	auto il = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
>	std::cout << sum(il) << std::endl;
>
>	return 0;
> }
> ```

#### 练习6.28
在`error_msg`函数的第二个版本中包含`ErrCode`类型的参数，其中循环内的`elem`是什么类型？
> `elem` 是 `const string &` 类型。

#### 练习6.29
在范围`for`循环中使用`initializer_list`对象时，应该将循环控制变量声明成引用类型吗？为什么？
> 应该使用**常量引用**类型。`initializer_list` 对象中的元素都是常量，我们无法修改`initializer_list` 对象中的元素的值。

### 6.3.2 有返回值函数
#### 练习6.30
编译第200页的`str_subrange`函数，看看你的编译器是如何处理函数中的错误的。
> `error: return-statement with no value, in function returning 'bool' [-fpermissive]`

#### 练习6.31
什么情况下返回的引用无效？什么情况下返回常量的引用无效？
> 当返回的引用的对象是局部变量时，返回的引用无效；当我们希望返回的对象被修改时，返回常量的引用无效。

#### 练习6.32

> 下面的函数合法吗？如果合法，说明其功能；如果不合法，修改其中的错误并解释原因。
```cpp
int &get(int *array, int index) { return array[index]; }
int main()
{
    int ia[10];
    for (int i = 0; i != 10; ++i)
        get(ia, i) = i;
}
```
> 合法。`get`函数根据索引取得数组中的元素的引用。

### 6.3.3 返回数组指针
#### 练习6.36
编写一个函数声明，使其返回数组的引用并且该数组包含10个`string`对象。不用使用尾置返回类型、`decltype`或者类型别名。
```cpp
string (&fun())[10];
```

#### 练习6.37
为上一题的函数再写三个声明，一个使用类型别名，另一个使用尾置返回类型，最后一个使用`decltype`关键字。你觉得哪种形式最好？为什么？
```cpp
typedef string str_arr[10];
str_arr& fun();

auto fun()->string(&)[10];

string s[10];
decltype(s)& fun();
```
> 我觉得尾置返回类型最好。

#### 练习6.38
修改`arrPtr`函数，使其返回数组的引用。
> ```cpp
> decltype(odd)& arrPtr(int i)
> {
>    return (i % 2) ? odd : even;
> }
> ```

## 6.4 函数重载
#### 练习6.39 
说明在下面的每组声明中第二条声明语句是何含义。如果有非法的声明，请指出来。
```cpp
(a) int calc(int, int);
    int calc(const int, const int);
(b) int get();
    double get();
(c) int *reset(int *);
    double *reset(double *)
```
> - (a) 非法。因为顶层const 不影响传入函数的对象，所以第二个声明无法与第一个声明区分开来。
> - (b) 非法。对于重载的函数来说，它们应该只有形参的数量和形参的类型不同。返回值与重载无关。
> - (c) 合法。

### 6.5.1 默认实参
#### 练习6.40
下面的哪个声明是错误的？为什么?
```cpp
(a) int ff(int a, int b = 0, int c = 0);
(b) char *init(int ht = 24, int wd, char backgrnd);
```
> (b)的声明是错误的，因为一旦某个形参被赋予了默认值，那么它之后的形参都必须要有默认值。

#### 练习6.41
下面的哪个调用是非法的？为什么？哪个调用虽然合法但显然与程序员的初衷不符？为什么？
```cpp
char *init(int ht, int wd = 80, char bckgrnd = ' ');
(a) init();
(b) init(24,10);
(c) init(14,'*');
```

> - (a) 非法。第一个参数不是默认参数，最少需要一个实参。
> - (b) 合法。
> - (c) 合法，但与初衷不符。字符 `*` 被解释成 `int` 传入到了第二个参数。而初衷是要传给第三个参数。

#### 练习6.42
给`make_plural`函数的第二个形参赋予默认实参`'s'`, 利用新版本的函数输出单词`success`和`failure`的单数和复数形式。
> ```cpp
> #include <iostream>
> #include <string>
> using std::string;
> using std::cout;
> using std::endl;
>
> string make_plural(size_t ctr, const string& word, const string& ending = "s")
> {
>	return (ctr > 1) ? word + ending : word;
> }
>
> int main()
> {
>	cout << "singual: " << make_plural(1, "success", "es") << " "
>		<< make_plural(1, "failure") << endl;
>	cout << "plural : " << make_plural(2, "success", "es") << " "
>		<< make_plural(2, "failure") << endl;
>
>	return 0;
> }
> ```

### 6.5.2 内联函数和constexpr函数
#### 练习6.43 
你会把下面的哪个声明和定义放在头文件？哪个放在源文件中？为什么？
```cpp
(a) inline bool eq(const BigInt&, const BigInt&) { ... }
(b) void putValues(int *arr, int size);
```
> 全部都放进头文件。(a) 是内联函数，(b) 是声明。

#### 练习6.44
将6.22节（第189页）的`isShorter`函数改写成内联函数。
> ```cpp
> inline bool is_shorter(const string &lft, const string &rht) 
> {
>    return lft.size() < rht.size();
> }
> ```

#### 练习6.45
回顾在前面的练习中你编写的那些函数，它们应该是内联函数吗？如果是，将它们改写成内联函数；如果不是，说明原因。


#### 练习6.46
能把`isShorter`函数定义成`constexpr`函数吗？如果能，将它改写成`constexpr`函数；如果不能，说明原因。
> 不能。`constexpr`函数的返回值类型及所有形参都得是字面值类型。

### 6.5.3 调试帮助
#### 练习6.47
改写6.3.2（第205页）练习中使用递归输出`vector`内容的程序，使其有条件地输出与执行过程有关的信息。例如，每次调用时输出`vector`对象的大小。分别在打开和关闭调试器的情况下编译并执行这个程序。
> ```cpp
> #include <iostream>
> #include <vector>
> using namespace std;
> using c_iter = vector<int>::const_iterator;
> #define NDEBUG
>
> void print(c_iter first, c_iter last)
> {
> #ifndef NDEBUG
>	cout << "vector size: " << last - first << endl;
> #endif
> 	if (first == last)
>	{
>		cout << "over!" << endl;
>		return;
>	}
>	cout << *first << " ";
>	print(++first, last);
> }
> 
> int main()
> {
>	vector<int> vec{ 1, 2, 3, 4, 5, 6, 7, 8, 9 };
>	print(vec.cbegin(), vec.cend());
>	return 0;
> }
> ```

#### 练习6.48
说明下面这个循环的含义，他对`assert`的使用合理吗？
```cpp
string s;
while (cin >> s && s != sought) {} //空函数体
assert(cin);
```
> 不合理。从这个程序的意图来看，应该用 
> ```cpp
> assert(s == sought);
> ```

## 6.6 函数匹配
#### 练习6.49 
什么是候选函数？什么是可行函数？
> - 候选函数：与被调用函数同名，并且其声明在调用点可见。
> - 可行函数：形参与实参的数量相等，并且每个实参类型与对应的形参类型相同或者能转换成形参的类型。

#### 练习6.50
已知有第217页对函数`f`的声明，对于下面的每一个调用列出可行函数。其中哪个函数是最佳匹配？如果调用不合法，是因为没有可匹配的函数还是因为调用具有二义性？
```cpp
(a) f(2.56, 42)
(b) f(42)
(c) f(42, 0)
(d) f(2.56, 3.14)
```
> - (a) `void f(int, int);` 和 `void f(double, double = 3.14);` 是可行函数。该调用具有二义性而不合法。
> - (b) `void f(int);` 是可行函数。调用合法。
> - (c) `void f(int, int);` 和 `void f(double, double = 3.14);` 是可行函数。`void f(int, int);` 是最佳匹配。
> - (d) `void f(int, int);` 和 `void f(double, double = 3.14);` 是可行函数。`void f(double, double = 3.14);` 是最佳匹配。

#### 练习6.51
编写函数`f`的4个版本，令其各输出一条可以区分的消息。验证上一个练习的答案，如果你的回答错了，反复研究本节内容直到你弄清自己错在何处。
> ```cpp
> #include <iostream>
> using std::cout;
> using std::endl;
>
> void f()
> {
>	cout << "f()" << endl;
> }
>
> void f(int)
> {
>	cout << "f(int)" << endl;
> }
>
> void f(int, int)
> {
>	cout << "f(int, int)" << endl;
> }
>
> void f(double, double)
> {
>	cout << "f(double, double)" << endl;
> }
>
> int main()
> {
>	//f(2.56, 42);
>	f(42);
>	f(42, 0);
>	f(2.56, 3.14);
>
>	return 0;
> }
> ```

### 6.6.1 实参类型转换
#### 练习6.52
```cpp
void manip(int, int);
double dobj;
```
请指出下列调用中每个类型转换的等级（参见6.6.1节，第219页）
```cpp
(a) manip('a', 'z');
(b) manip(55.4, dobj);
```
> - (a) 第3级。类型提升实现的匹配。
> - (b) 第4级。算术类型转换实现的匹配。

#### 练习6.53
说明下列每组声明中的第二条语句会产生声明影响，并指出哪些不合法（如果有的话）。
```cpp
(a) int calc(int&, int&);
	int calc(const int&, const int&);
(b) int calc(char*, char*)
    int calc(const char*, const char*);
(c) int calc(char*, char*)
    int calc(char* const, char* const);
```
> (c) 不合法。顶层`const`不影响传入函数的对象。

## 6.7 函数指针
#### 练习6.54
编写函数的声明，令其接受两个`int`形参并返回类型也是`int`；然后声明一个`vector`对象，令其元素是指向该函数的指针。
> ```cpp
> int func(int, int);
> vector<decltype(func)*> v;
> ```

#### 练习6.55
编写4个函数，分别对两个`int`值执行加、减、乘、除运算；在上一题创建的`vector`对象中保存指向这些函数的指针。
> ```cpp
> int add(int a, int b) { return a + b; }
> int subtract(int a, int b) { return a - b; }
> int multiply(int a, int b) { return a * b; }
> int divide(int a, int b) { return b != 0 ? a / b : 0; }
>
> v.push_back(add);
> v.push_back(subtract);
> v.push_back(multiply);
> v.push_back(divide);
> ```

#### 练习6.56
调用上述`vector`对象中的每个元素并输出结果。
> ```cpp
> #include <iostream>
> #include <vector>
> using namespace std;
>
> int add(int a, int b) { return a + b; }
> int subtract(int a, int b) { return a - b; }
> int multiply(int a, int b) { return a * b; }
> int divide(int a, int b) { return b != 0 ? a / b : 0; }
> 
> int main()
> {
> 	int func(int, int);
>	vector<decltype(func)*> v;
>	v.push_back(add);
>	v.push_back(subtract);
>	v.push_back(multiply);
>	v.push_back(divide);
>	
>	for (auto i : v)
>	{
>		cout << i(6, 2) << " "; 
>	}
>	cout << endl;
>	return 0;
> }
> ```

# 第七章类
## 7.1 定义抽象数据类型
### 7.1.1 设计Sales_data类
#### 练习7.1
使用2.6.1节定义的`Sales_data`类为1.6节的交易处理程序编写一个新版本。
> ```cpp
> #include <iostream>
> #include <string>
> using std::cin;
> using std::cout; 
> using std::endl; 
> using std::string;
>
> struct Sales_data
> {
>	string bookNo;
>	unsigned units_sold = 0;
>	double revenue = 0.0;
> };
>
> int main()
> {
>	Sales_data total;
>	if (cin >> total.bookNo >> total.units_sold >> total.revenue)
>	{
>		Sales_data trans;
>		while (cin >> trans.bookNo >> trans.units_sold >> trans.revenue)
> 		{
>			if (total.bookNo == trans.bookNo)
>			{
>				total.units_sold += trans.units_sold;
>				total.revenue += trans.revenue;
>			}
>			else
>			{
>				cout << total.bookNo << " " << total.units_sold << " " << total.revenue << endl;
>				total = trans;
>			}
>		}
>		cout << total.bookNo << " " << total.units_sold << " " << total.revenue << endl;
>	}
>	else
>	{
>		std::cerr << "No data?!" << std::endl;
>		return -1;
>	}
>	return 0;
> }
> ```


## 7.1 定义抽象数据类型
#### 练习7.2
曾在2.6.2节的练习（第67页）中编写了一个`Sales_data`类，请向这个类添加`combine`和`isbn`成员。
> ```cpp
> #include <string>
>
> struct Sales_data
> {
>	std::string isbn() const { return bookNo; };
>	Sales_data& combine(const Sales_data&);
>
>	std::string bookNo;
>	unsigned units_sold = 0;
>	double revenue = 0.0;
> };
>
> Sales_data& Sales_data::combine(const Sales_data& rhs)
> {
> 	units_sold += rhs.units_sold;
>	revenue += rhs.revenue;
>	return *this;
> }
> ```

#### 练习7.3
修改7.1.1（第229页）的交易处理程序，令其使用这些成员。
> ```cpp
> #include <string>
> #include <iostream>
> using std::cin; 
> using std::cout; 
> using std::endl;
> using std::string;
> using std::cerr;
> 
> struct Sales_data
> {
>	string isbn() const { return bookNo; };
>	Sales_data& combine(const Sales_data&);
>
>	string bookNo;
>	unsigned units_sold = 0;
>	double revenue = 0.0;
> };
> 
> Sales_data& Sales_data::combine(const Sales_data& rhs)
> {
>	units_sold += rhs.units_sold;
> 	revenue += rhs.revenue;
>	return *this;
> }
> 
> int main()
> {
> 	Sales_data total;
>	if (cin >> total.bookNo >> total.units_sold >> total.revenue)
>	{
>		Sales_data trans;
>		while (cin >> trans.bookNo >> trans.units_sold >> trans.revenue)
>		{
>			if (total.isbn() == trans.isbn())
>				total.combine(trans);
>			else
>			{
>				cout << total.bookNo << " " << total.units_sold << " " << total.revenue << endl;
>				total = trans;
>			}
>		}
>		cout << total.bookNo << " " << total.units_sold << " " << total.revenue << endl;
>	}
>	else
>	{
>		cerr << "No data?!" << endl;
>		return -1;
>	}
>
>	return 0;
> }
> ```

#### 练习7.4
编写一个名为`Person`的类，使其表示人员的姓名和住址。使用`string`对象存放这些元素，接下来的练习将不断充实这个类的其他特征。
> ```cpp
> #include <string>
> using std::string;
>
> class Person{
>   string name;
>   string addr;
> };
> ```

#### 练习7.5
在你的`Person`类中提供一些操作使其能够返回姓名和住址。这些函数是否应该是`const`？请解释原因。
> ```cpp
> #include <string>
> using std::string;
>
> class Person{
>   string name;
>   string addr;
>   auto getname() const -> string const& { return name; }
>   auto getaddr() const -> string const& { return addr; }   
> };
> ```
> 应该是`const`，不论返回姓名还是返回地址，在函数体内都只是读取数据成员的值，而不会做任何改变。

### 7.1.3 定义类相关的非成员函数
#### 练习7.6
对于函数`add`、`read`、`print`定义你自己的版本。
> ```cpp
> #include <string>
> #include <iostream>
> using std::string;
> using std::istream;
> using std::ostream;
> 
> struct Sales_data
> {
>	string const& isbn() const { return bookNo; };
>	Sales_data& combine(const Sales_data&);
>
>	string bookNo;
>	unsigned units_sold = 0;
>	double revenue = 0.0;
> };
>
> Sales_data& Sales_data::combine(const Sales_data& rhs)
> {
>	units_sold += rhs.units_sold;
>	revenue += rhs.revenue;
>	return *this;
> }
>
> istream &read(istream &is, Sales_data &item)
> {
> 	double price = 0;
>	is >> item.bookNo >> item.units_sold >> price;
>	item.revenue = price * item.units_sold;
>	return is;
> }
> 
> ostream &print(ostream &os, const Sales_data &item)
> {
>	os << item.isbn() << " " << item.units_sold << " " << item.revenue;
> 	return os;
> }
>
> Sales_data add(const Sales_data &lhs, const Sales_data &rhs)
> {
> 	Sales_data sum = lhs;
>	sum.combine(rhs);
>	return sum;
> }
> ```

#### 练习7.7
使用这些新函数重写7.1.2（第233页）练习中的交易处理程序。
> ```cpp
> #include <string>
> #include <iostream>
> using std::string;
> using std::istream;
> using std::ostream;
> using std::cerr;
> 
> struct Sales_data
> {
>	string const& isbn() const { return bookNo; };
>	Sales_data& combine(const Sales_data&);
>
>	string bookNo;
>	unsigned units_sold = 0;
>	double revenue = 0.0;
> };
>
> Sales_data& Sales_data::combine(const Sales_data& rhs)
> {
>	units_sold += rhs.units_sold;
>	revenue += rhs.revenue;
>	return *this;
> }
>
> istream &read(istream &is, Sales_data &item)
> {
> 	double price = 0;
>	is >> item.bookNo >> item.units_sold >> price;
>	item.revenue = price * item.units_sold;
>	return is;
> }
> 
> ostream &print(ostream &os, const Sales_data &item)
> {
>	os << item.isbn() << " " << item.units_sold << " " << item.revenue;
> 	return os;
> }
>
> Sales_data add(const Sales_data &lhs, const Sales_data &rhs)
> {
> 	Sales_data sum = lhs;
>	sum.combine(rhs);
>	return sum;
> }
> 
> int main()
> {
>	Sales_data total;
>	if (read(cin, total))
>	{
>		Sales_data trans;
>		while (read(cin, trans))
>		{
>			if (total.isbn() == trans.isbn())
>				total.combine(trans);
>			else
>			{
>				print(cout, total) << endl;
>				total = trans;
>			}
>		}
>		print(cout, total) << endl;
>	}
>	else
>	{
>		cerr << "No data?!" << endl;
>		return -1;
>	}
>
>	return 0;
> }
> ```

#### 练习7.8
为什么`read`函数将其`Sales_data`定义为普通的引用，而`print`将其参数定义为常量引用？
> 因为`read`函数会改变对象的内容，而`print`函数不会。

#### 练习7.9
对于7.1.2（第233页）练习中的代码，添加读取和打印`Person`对象的操作。
> ```cpp
> #include <iostream>
> #inclde <string>
> using std::cout;
> using std::cin;
> using std::endl;
> using std::string;
> using std::istream;
> using std::ostream;
>
> class Person{
>   string name;
>   string addr;
>   auto getname() const -> string const& { return name; }
>   auto getaddr() const -> string const& { return addr; }   
> };
> 
> istream &read(istream &is, Person &person)
> {
>   return is >> person.name >> person.addr;
> }
> 
> ostream &print(ostream &os, const Person &person)
> {
>   return os << person.name << " " << person.addr;
> }
> ```

#### 练习7.10
在下面这条`if`语句中，条件部分的作用是什么？
```cpp
if (read(read(cin, data1), data2))
```
> `if`语句中条件部分的作用是从输入流中读取数据给两个`data`对象。

### 7.1.4 构造函数
