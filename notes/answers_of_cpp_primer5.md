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
```c++
#include <iostream>

int main()
{
    std::cout << 2 << "\115\012";
    std::cout << 2 << "\t\115\012";
    return 0;
}
```


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
```c++
int a = 1, b = 2;
int *p1 = &a, *p2 = p1;
//change value of pointer
p1 = &b;
//change the value of the object which pointer pointing at
p2 = b;
```

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

## 2.4 `const`限定符
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

### 2.4.4 `constexpr`和常量表达式
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
> ```cc
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
```c++
#include <iostream>
#include <string>
using std::string;
using std::cout;
using std::cin;
using std::endl;

int main()
{
    string s1,s2;
    getline(cin, s1);
    getline(cin, s2);

    if (s1 == s2)
    {
        cout << "equal!" << endl;
    }
    else 
    {
        cout << ((s1 > s2) ? s1 : s2) << endl;
    }
}
```

```c++
#include <iostream>
#include <string>
using std::string;
using std::cout;
using std::cin;
using std::endl;

int main()
{
    string s1,s2;
    getline(cin, s1);
    getline(cin, s2);

    if (s1.size() == s2.size())
    {
        cout << "equal!" << endl;
    }
    else 
    {
        cout << ((s1.size() > s2.size()) ? s1 : s2) << endl;
    }
}
```


#### 练习3.5
编写一段程序从标准输入中读入多个字符串并将它们连接在一起，输出连接成的大字符串，然后修改上述程序，用空格把输入的多个字符串分隔开来
```c++
#include <iostream>
#include <string>
using std::string;
using std::cout;
using std::cin;
using std::endl;

int main()
{
	string result, s;
	while (getline(cin, s))
	{
		result += s;
	}
	cout << result << endl;

	return 0;
}
```

```c++
#include <iostream>
#include <string>
using std::string;
using std::cout;
using std::cin;
using std::endl;

int main()
{
	string result, s;
	while (getline(cin, s))
	{
		result += s + " ";
	}
	cout << result << endl;

	return 0;
}
```

### 3.2.3 处理string对象中的字符
#### 练习3.6
编写一段程序，使用范围`for`语句将字符串内所有字符用`X`代替。
```cpp
for (auto &x : s)
	{
		x = 'X';
	}

```

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
```cpp
string s, result;
for (auto x : s)
	{
		if (!ispunct(x))
		{
			result += x;
		}
	}
```

#### 练习3.11
下面的范围for语句合法吗？如果合法，c的类型是什么？
```cpp
const string s = "Keep out!";
for(auto &c : s){ /* ... */ }
```

> 要根据for循环中的代码来看是否合法，c是string 对象中字符的引用，s是常量。因此如果for循环中的代码重新给c赋值就会非法，如果不改变c的值，那么合法。


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
```cpp
#include <iostream>
#include <vector>
using std::vector;
using std::cin;
using std::cout;
using std::endl;

int main()
{
	vector<int> v;
	int i;
	while (cin >> i)
	{
		v.push_back(i);
	}
	return 0;
}
```

#### 练习3.15
改写上题程序，不过这次读入的是字符串。
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <cctype>
using std::vector;
using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
	vector<string> v;
	string i;
	while (cin >> i)
	{
		v.push_back(i);
	}
	return 0;
}
```

### 3.3.3 其他vector操作
#### 练习3.16
编写一段程序，把练习3.13中`vector`对象的容量和具体内容输出出来
```cpp
#include <iostream>
#include <string>
#include <cctype>
#include <vector>

using std::cin;
using std::cout;
using std::endl;
using std::vector;
using std::string;

int main()
{
	vector<int> v1;     
	vector<int> v2(10);    
	vector<int> v3(10, 42); 
	vector<int> v4{ 10 };    
	vector<int> v5{ 10, 42 }; 
	vector<string> v6{ 10 };  
	vector<string> v7{ 10, "hi" }; 

	cout << "v1 size :" << v1.size() << endl;
	cout << "v2 size :" << v2.size() << endl;
	cout << "v3 size :" << v3.size() << endl;
	cout << "v4 size :" << v4.size() << endl;
	cout << "v5 size :" << v5.size() << endl;
	cout << "v6 size :" << v6.size() << endl;
	cout << "v7 size :" << v7.size() << endl;

	cout << "v1 content: ";
	for (auto i : v1)
	{
		cout << i << " , ";
	}
	cout << endl;

	cout << "v2 content: ";
	for (auto i : v2)
	{
		cout << i << " , ";
	}
	cout << endl;

	cout << "v3 content: ";
	for (auto i : v3)
	{
		cout << i << " , ";
	}
	cout << endl;

	cout << "v4 content: ";
	for (auto i : v4)
	{
		cout << i << " , ";
	}
	cout << endl;

	cout << "v5 content: ";
	for (auto i : v5)
	{
		cout << i << " , ";
	}
	cout << endl;

	cout << "v6 content: ";
	for (auto i : v6)
	{
		cout << i << " , ";
	}
	cout << endl;

	cout << "v7 content: ";
	for (auto i : v7)
	{
		cout << i << " , ";
	}
	cout << endl;
	return 0;
}
```

#### 练习3.17
从`cin`读入一组词并把它们存入一个`vector`对象，然后设法把所有词都改为大写形式。输出改变后的结果，每个词占一行。
```cpp
#include <iostream>
#include <string>
#include <cctype>
#include <vector>

using std::cin;
using std::cout;
using std::endl;
using std::vector;
using std::string;

int main()
{
	vector<string> v;
	string s;

	while (cin >> s)
	{
		v.push_back(s);
	}

	for (auto &str : v)
	{
		for (auto &c : str)
		{
			c = toupper(c);
		}
	}

	for (auto i : v)
	{
		cout << i << endl;
	}
	return 0;
}
```

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
第一种方式最好。

#### 练习3.20
读入一组整数并把他们存入一个`vector`对象，将每对相邻整数的和输出出来。改写你的程序，这次要求先输出第一个和最后一个元素的和，接着输入第二个和倒数第二个元素的和，以此类推。
```cpp
#include <iostream>
#include <vector>

using std::cout;
using std::cin;
using std::endl;
using std::vector;

int main()
{
    //question 1
    vector<int> ivec;
    int i;
    while (cin >> i)
    {
        ivec.push_back(i);
    }

    for (int i = 0; i < ivec.size() - 1; i++)
    {
        cout << ivec[i] + ivec[i + 1] << endl;
    }

    //question 2
    int m = 0;
    int n = ivec.size() - 1;
    while (n > m)
    {
        cout << ivec[m] + ivec[n] << endl;
        ++m;
        --n;
    }
    return 0;
    
}
```

## 3.4 迭代器介绍
### 3.4.1 使用迭代器
#### 练习3.21
请使用迭代器重做 **练习3.16**
```cpp
#include <iostream>
#include <string>
#include <iterator>
#include <vector>

using std::cout;
using std::string;
using std::endl;
using std::vector;

void print(const vector<int>& vec)
{
    cout << "size: " << vec.size() << endl 
        << " content :";
    for (auto it = vec.begin(); it !=  vec.end(); ++it)
    {
        cout << *it << (it != vec.end() - 1 ? ", " : "");
    }
    cout << endl;
    
}

void print(const vector<string>& vec)
{
    cout << "size: " << vec.size() << endl 
        << " content :";
    for (auto it = vec.begin(); it !=  vec.end(); ++it)
    {
        cout << *it << (it != vec.end() - 1 ? ", " : "");
    }
    cout << endl;
}

int main()
{
    vector<int> v1;     
	vector<int> v2(10);    
	vector<int> v3(10, 42); 
	vector<int> v4{ 10 };    
	vector<int> v5{ 10, 42 }; 
	vector<string> v6{ 10 };  
	vector<string> v7{ 10, "hi" }; 

    print(v1);
    print(v2);
    print(v3);
    print(v4);
    print(v5);
    print(v6);
    print(v7);

    return 0;
}
```

#### 练习3.22
修改之前那个输出text第一段的程序，首先把text的第一段全部改成大写形式，然后输出它。
```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    vector<string> text;
    text.push_back("aaaaaaaaaa aaaaaaaaa aaaaaa");
	text.push_back("");
	text.push_back("bbbbbbbbbbbbbb bbbbbbbbbbb bbbbbbbbbbbbb");

    for (auto it = text.begin(); it != text.end() && !it->empty(); ++it)
    {
        for (auto &c : *it)
        {
            if (isalpha(c)) c = toupper(c);
        }
    }

    for (auto it : text)
    {
        cout << it << endl;
    }
    
    return 0;
    
}
```

#### 练习3.23
编写一段程序，创建一个含有10个整数的`vector`对象，然后使用迭代器将所有的元素都变成原来的两倍，输出`vector`对象的内容，检验程序是否正确。
```cpp
#include <iostream>
#include <vector>
#include <iterator>

using namespace std;

int main()
{
    vector<int> ivec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
    for (auto it = ivec.begin(); it != ivec.end(); ++it)
    {
        *it  = *it * 2;
        cout << *it << endl;
    }
    return 0;
}
```


### 3.4.1 迭代器运算
#### 练习3.24 
请使用迭代器重做练习3.20
```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int main()
{
    vector<int> ivec;
    int i;
    while (cin >> i)
    {
        ivec.push_back(i);
    }
    
    for (auto it = ivec.begin(); it != ivec.end() - 1; it++)
    {
        cout << *it + *(it + 1) << endl;
    }

    cout << "---------------------------------" << endl;

	auto it1 = ivec.begin();
	auto it2 = ivec.end() - 1;
	while (it1 < it2)
	{
		cout << *it1 + *it2 << endl;
		++it1;
		--it2;
	}
	return 0;
}
```

#### 练习3.25 
3.3.3节划分分数段的程序是使用下标运算符实现的，请利用迭代器改写该程序实现完全相同的功能。
```cpp
#include <vector>
#include <iostream>

using namespace std;

int main()
{
	vector<unsigned> scores(11, 0);
	unsigned grade;
	while (cin >> grade)
	{
		if (grade <= 100)
			++*(scores.begin() + grade / 10);
	}

	for (auto s : scores)
		cout << s << " ";
	cout << endl;

	return 0;
}
```

#### 练习3.26
在100页的二分搜索程序中，为什么用的是 mid = beg + (end - beg) / 2, 而非 mid = (beg + end) / 2 ; ?
> 因为迭代器支持的运算只有 `-` ，而没有 `+` 。`end - beg` 意思是相距若干个元素，将之除以`2`然后与`beg`相加，表示将`beg`移动到一半的位置。
