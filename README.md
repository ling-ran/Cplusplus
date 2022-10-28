# C语言
## 关键字
关键字 |   - |   -   |     -   | -       |    -   |     -    |    -    |
------- | ----- |----- | ------ | ------ |------|---------|--------|
char| short| int| long |float |double| if |else|
return | do| while | for | switch | case | break| continue |
default | goto| sizeof | auto | register | static | extern | unsigned |
signed | typedef| struct | enum | union | void | const | volatile |
-------------------------------------------------------------------------------------------------- 
 -  **register**大量频繁使用的数据，放在寄存器中，提升效率，在数据前加register(可以不加编译器可以识别）
 - **struct**结构体
 - **union**联合体（共用体）
 - **define include**是预处理指令，不是关键词
 - **typedef**
 ```c
 typedef unsigned int un_it
//typedef 顾名思义是类型定义，这里应该理解为类型重命名。
int main()
{
 unsigned int num1 = 1;
 un_it num2 = 1;
 //观察num1和num2,这两个变量的类型是一样的
 return 0;
｝
```
>**static**用来修饰变量和函数的 
> 
1.修饰局部变量   称为静态局部将变量改变局部变量的生命周期，本质上是改变了变量的存储类型。
![static](https://img-blog.csdnimg.cn/a20b1a8782c6457fbdac63ef53e42710.jpeg#pic_center)
```c
//代码1
#include <stdio.h>
void test()
{
    int i = 0;
    i++;
    printf("%d ", i);
}
int main()
{
 int i = 0;
    for(i=0; i<10; i++)
   {
        test();
   }
    return 0;
}
```

2.static修饰局部变量改变了变量的生命周期，让静态局部变量出了作用域依然存在，到程序结束生命周期才结束。
```c
//代码二
 void test()
{
 static修饰局部变量
 static int i = 0;
 i++; 
 printf("%d\n", i);
}
int main()
{
 int i = 0;
 for (i = 0; i < 10; i++)
 {
  test();
 }
 return 0;
}
```
3.修饰函数-称为静态函数
```c
三.//代码1
int g_val = 2018;
//test.c
int main()
{
    printf("%d\n", g_val);
    return 0;
}
//代码2
static int g_val = 2018;
//test.c
int main()
{
    printf("%d\n", g_val);
    return 0;
}
```
>代码1正常，代码2在编译的时候会出现连接性错误。
结论：
一个全局变量被static修饰，使得这个全局变量只能在本源文件内使用，不能在其他源文件内使用

 ## 数据类型
- C语言中有四大数据类型，分为基本类型、构造类型、指针类型、空类型
       
>**整型常量** 
- 十进制的整数
- 八进制的整数，以0开头。例如：0123也就是十进制83
- 十六进制整数，以0x开头。例如：0x123就是10进制291
- 二进制整数，0b开头。例如：0b0010就是10进制2
>**实型常量**

1.小数形式
- 单精度小数，以字母f或F结尾。例如：1.0f、1.01f
- 双精度小数，十进制小数形式，3.14
- 默认双精度
- 可以没有整数位只有小数位。例如：.3、6f

2.指数形式
- 以幂的形式表示 ，以字母E或e后跟一个10为底的指数
- 1.23×10^5用C语言表示就是1.23e5或1.23E5
- 字母E后面必须为整数
- 字母E前后必须要有数字
- E前后不能有空格

>字符常量
- 用单引号括起来'a'  'b'  'c'
- 字符常量的单引号中只能有一个字符
- 特殊情况：如果是转义字符，单引号中可以有两个字符。'\n'、'\t'

>字符串常量
- 字符型常量都是用双引号括起来的。例如:"a"、"abc"、"lnj"
- 系统会自动在字符串常量的末尾加一个字符’\0’作为字符串结束标志 
>自定义常量
------------------------------------------------------------------------------------------
## 变量
变量名的命名的规范
变量名属于标识符,所以必须严格遵守标识符的命名原则
### 定义变量
- 格式1: 变量类型 变量名称
- 任何变量在使用之前，必须先进行定义, 只有定义了变量才会分配存储空间, 才有空间存储数据
- 用来约束变量所存放数据的类型。一旦给变量指明了类型，那么这个变量就只能存储这种类型的数据
- 内存空间极其有限,不同类型的变量占用不同大小的存储空间
- 存储数据的空间对于我们没有任何意义, 我们需要的是空间中存储的值，只有有了名称, 我们才能获取到空间中的值

```c
int a;
float b;
char arr;
```
- 格式2:变量类型 变量名称,变量名称
- 连续定义, 多个变量之间用逗号(,)号隔开
```c
int a,b,c;
```
--------------------------------------------------------------
###  使用变量
 - 在C语言中用 = 来给变量赋值
```c
int value;
value = 1;//赋值
```
> 这里的 = 不同于数学里的“相等”，而是**赋值运算符**，是将右边赋值给左边
> 赋值的时候左边必须是变量，（10 = b)错误
> **在代码中适当加入空格方便阅读**
--------------------------------------------------------------------------------------------
### 变量的初始化
 - 在C语言中变量的第一次赋值，成为变量的“初始化”
 - 初始化两种形式
   - 先定义，后初始化
   - int value; value = 998; // 初始化
   -  定义时同时初始化
   - int a = 10; int b = 4, c = 2;

- 不初始化时变量内储存什么？
  - 随机数
  - 系统正在用的一些数据
  - 上次程序分配的存储空间,存数一些 内容,“垃圾”
--------------------------------------------------------------------------------------
### 修改变量
- 多次赋值即可，每次会覆盖原来的值
```c
int i = 10;
i = 20; // 修改变量的值
```
### 变量之间的值传递
- 可以将一个变量存储的值赋值给另一个变量
```c
int a = 10;
int b = a; // 相当于把a中存储的10拷贝了一份给b
```
-----------------------------------------------------------------------------------------
### 变量的作用域
- C语言中所有变量都有自己的作用域
- 变量定义的位置不同,其作用域也不同
- 按照作用域的范围可分为两种, 即局部变量和全局变量
## 变量内存分析
### 内存存储细节
- 字节和地址
  - 每一个小格子代表一个字节
  - 每个字节都有自己的内存地址
  - 内存地址是连续的

![内存](https://img-blog.csdnimg.cn/9564a2a841e74f4dbfafbcf1365b78a3.png#pic_center)
- 内存模型
  - 内存模型是线性的
  - 对于32位机而言，最大的内存地址是2^32次方bit(4294967296)4GB
  - 对于 64 机而言，最大的内存地址是2^64次方bit(18446744073709552000)(171亿GB)

  ![内存地址](https://img-blog.csdnimg.cn/370b2b63116b431cae49c897ca9512f7.jpeg#pic_center)
------------------------------------------------------------------------------------------
### CPU内存读写细节
- **CPU读取内存**
   - 存储单元的地址（地址信息）
   - 器件的选择，读或写（控制信息）
   -  读写的数据 （数据信息）
1. 通过地址总线找到存储单元的地址
- 地址总线: 地址总线宽度决定了CPU可以访问的物理地址空间(寻址能力)
- 例如: 地址总线的宽度是1位, 那么表示可以访问 0 和 1的内存
- 例如: 地址总线的位数是2位, 那么表示可以访问 00、01、10、11的内存  
2. 通过控制总线发送内存读写指令
- 数据总线: 数据总线的位数决定CPU单次通信能交换的信息数量
- 例如: 数据总线:的宽度是1位, 那么一次可以传输1位二进制数据
- 例如: 地址总线的位数是2位,那么一次可以传输2位二进制数据
3. 通过数据总线传输需要读写的数据
>控制总线: 用来传送各种控制信号
- 写入流程
  - CPU 通过地址线将找到地址为 FFFFFFFB 的内存
  - CPU 通过控制线发出内存写入命令，选中存储器芯片，并通知它，要其写入数据。
  - CPU 通过数据线将数据 8 送入内存 FFFFFFFB 单元中
![写入流程](https://img-blog.csdnimg.cn/a79b93c4741544eba2e2e8dc6ae90fd7.jpeg#pic_center)
- 读取流程
  - CPU 通过地址线将找到地址为 FFFFFFFB 的内存
  - CPU 通过控制线发出内存读取命令，选中存储器芯片，并通知它，将要从中读取数据
  - 存储器将 FFFFFFFB 号单元中的数据 8 通过数据线送入 CPU寄存器中![读取流程](https://img-blog.csdnimg.cn/7306cfc1008e4c0b9a24b4d183401cc3.jpeg#pic_center)
 - 变量存储原则
   - 先分配字节地址大内存，然后分配字节地址小的内存（内存寻址是从大到小）
   - 变量的首地址,是变量所占存储空间字节地址(最小的那个地址 )
   - 低位保存在低地址字节上,高位保存在高地址字节上 

```c
10的二进制: 0b00000000 00000000 00000000 00001010
           高字节←                        →低字节
```
-----------------------------------------------------------------------------------------------------------------------
### char类型内存存储细节
- char类型基本概念
  - char是C语言中比较灵活的一种数据类型，称为“字符型”
  - char类型变量占1个字节存储空间，共8位
  - 除单个字符以外, C语言的的转义字符也可以利用char类型存储
  
字符 | 意义  
------ | ------ 
   \b   |  退格(BS)当前位置向后回退一个字符  
   \r    |   回车(CR),将当前位置移至本行开头
   \n    |  换行(LF),将当前位置移至下一行开头
   \t     |  水平制表(HT),跳到下一个 TAB 位置
   \0    |  用于表示字符串的结束标记
   \      |   代表一个反斜线字符 \
   \\"     |   代表一个双引号字符"
   \\'      |   代表一个单引号字符’
    - char型数据存储原理
     - 计算机只能识别0和1, 所以char类型存储数据并不是存储一个字符, 而是将字符转换为0和1之后再存储
     - 存储字符类型时需要将字符转换为0和1, 为了统一, 就制定了ASCII表
     - ASCII表中定义了每一个字符对应的整数
![ASCII码表](https://img-blog.csdnimg.cn/84532f46e99b419081d0536930364d37.png#pic_center)

```c
char ch1 = 'a'; 
printf("%i\n", ch1); // 97
//使用ASCII码就可以代表字符
char ch2 = 97;
printf("%c\n", ch2); // a
```
- char型注意事项
  - char类型占一个字节, 一个中文字符占3字节(unicode表),所有char不可以存储中文
  - 除转义字符以外, 不支持多个字符
```c
char ch = 'ab'; // 错误写法

```
  - char类型存储字符时会先查找对应的ASCII码值, 存储的是ASCII值, 所以字符6和数字6存储的内容不同
 ```c
char ch1 = '6'; // 存储的是ASCII码 64
char ch2 = 6; //  存储的是数字 6
```
# 函数
## printf函数
- printf函数称之为格式输出函数,方法名称的最后一个字母f表示format。其功能是按照用户指定的格式,把指定的数据输出到屏幕上

- 格式**printf("格式控制字符串",输出项列表 );**
- 例如:**printf("a = %d, b = %d",a, b);**
---------------------------------------------------------------------------------------------------
- 格式控制字符串
- 形式: %[标志][输出宽度][.精度][长度]类型
---------------------------------------------------------------------------------
- 格式: printf("a = %类型", a);
- 类型字符串用以表示输出数据的类型, 其格式符和意义如下所示

类型 | 含义
------ | --------
d      | 有符号10进制整型
i       |有符号10进制整型
u    |无符号10进制整型
o     |无符号8进制整型
x    |无符号16进制整型
X    |无符号16进制整型
f     |单、双精度浮点数(默认保留6位小数)
E / e    |以指数形式输出单、双精度浮点数
g / G   |以最短输出宽度,输出单、双精度浮点数
c      |字符
s     |字符串
p     |地址

```c
#include <stdio.h>
int main()
{
    int a = 10;
    int b = -10;
    float c = 6.6f;
    double d = 3.1415926;
    double e = 10.10;
    char f = 'a';
    // 有符号整数(可以输出负数)
    printf("a = %d\n", a); // 10
    printf("a = %i\n", a); // 10

    // 无符号整数(不可以输出负数)
    printf("a = %u\n", a); // 10
    printf("b = %u\n", b); // 429496786

    // 无符号八进制整数(不可以输出负数)
    printf("a = %o\n", a); // 12
    printf("b = %o\n", b); // 37777777766

    // 无符号十六进制整数(不可以输出负数)
    printf("a = %x\n", a); // a
    printf("b = %x\n", b); // fffffff6

    // 无符号十六进制整数(不可以输出负数)
    printf("a = %X\n", a); // A
    printf("b = %X\n", b); // FFFFFFF6

    // 单、双精度浮点数(默认保留6位小数)
    printf("c = %f\n", c); // 6.600000
    printf("d = %lf\n", d); // 3.141593

    // 以指数形式输出单、双精度浮点数
    printf("e = %e\n", e); // 1.010000e+001
    printf("e = %E\n", e); // 1.010000E+001
    
    // 以最短输出宽度,输出单、双精度浮点数
    printf("e = %g\n", e); // 10.1
    printf("e = %G\n", e); // 10.1
    
    // 输出字符
    printf("f = %c\n", f); // a
}
```
----------------------------------------------------------------------
- 宽度格式：**格式: printf("a = %[宽度]类型", a);**
- 用十进制整数来指定输出的宽度, 如果实际位数多于指定宽度,则按照实际位数输出, 如果实际位数少于指定宽度则以空格补位

```c
#include <stdio.h>
int main()
{
    // 实际位数小于指定宽度
    int a = 1;
    printf("a =|%d|\n", a); // |1|
    printf("a =|%5d|\n", a); // |    1|
    // 实际位数大于指定宽度
    int b = 1234567;
    printf("b =|%d|\n", b); // |1234567|
    printf("b =|%5d|\n", b); // |1234567|
}
```
----------------------------------------------------------------------------
- 标志  格式: printf("a = %[标志][宽度]类型", a);

字符  | 意义
-------|----------
  \-     |左对齐, 默认右对齐
  \+     |当输出值为正数时,在输出值前面加上一个+号, 默认不显示
  0      |右对齐时, 用0填充宽度.(默认用空格填充)
空格|输出值为正数时,在输出值前面加上空格, 为负数时加上负号
\#   |对c、s、d、u类型无影响
\#  |对o类型, 在输出时加前缀o
\#  |对x类型,在输出时加前缀0x









  
  
  
  
  
  






>打印100到200的素数过程优化  
>首先偶数都可以省去，每次加2
>不必把从2到i的数全部试一遍，只需到\sqrt{2}就可以
```c
#include"stdio.h"
#include"math.h"
int main()//100到200的素数
{
	int i = 0;
	int count = 0;
	for (i = 100; i <= 200; i++)//因为每个偶数都可以省去，可以优化为i+=2
	{
		int n = 0;
		for (n = 2; n <= i ; n++)//n<=sqrt(i)开平方函数
		{
			if (i % n == 0)
				break;
		}
		if (i == n)
		{
			printf("%d ", i);
			count++;
		}
	}
	printf("\n%d", count);
	return 0;
}
```

>用二分法查找数组里的值
```c
#include"stdio.h"
int main()
{
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int k = 7;//要查找的数字，在数组中找k（7）的值
	int sz = sizeof(arr) / sizeof(arr[0]);//算数组的元素个数

	int left = 0;
	int right = sz - 1;

	while (left <= right)//二分法
	{
		int mid = (left + right) / 2;
		if (arr[mid] < k)
		{
			left = mid + 1;
		}
		else if (arr[mid] > k)
		{
			right = mid - 1;
		}
		else
		{
			printf("找到，下标为：%d\n", mid);
			break;
		}
	}
	if (left > right)
	{
		printf("找不到\n");
	}
	return 0;
}
```
指针
32位系统最多支持4G内存
十六进制Hexadecimal
1 2 ……10  11  12  13  14  15
1 2……A    B    C    D    E    F
指针就是地址
32位是4个字节 64位是8个字节

结构体.成员变量   就能找到结构体当中的成员

int main()
{
 int arr[10] = { 0 };
 printf("%d\n", sizeof(arr));
 int b = sizeof(arr) / sizeof(arr[0]);
 printf("%d\n", b);
 return 0;
}

加~输出反码
int main()
{
 int a = 1;
 printf("%d\n", ~a);
 return 0;
}
整数在内存存储的是补码
一个整数二进制表示有两种原码反码补码
正整数原码补码反码都相同
补码＝反码＋1
正数32位最高位0负数0 

```c
include <stdlib.h>
#include <stdio.h>

void quicksort(int *arr,unsigned int len)
{
  if (len<2) return;  // 数组的元素小于2个就不用排序了。

  int itmp=arr[0];  // 选取最左边的数作为中心轴。
  int ileft=0;      // 左下标。
  int iright=len-1; // 右下标。
  int imoving=2;    // 当前应该移动的下标，1-左下标；2-右下标。

  while (ileft<iright)
  {
    if (imoving==2) // 移动右下标的情况。
    {
      // 如果右下标位置元素的值大于等于中心轴，继续移动右下标。
      if (arr[iright]>=itmp) { iright--; continue; }
      
      // 如果右下标位置元素的值小于中心轴，把它填到左下标的坑中。
      arr[ileft]=arr[iright];
      ileft++;    // 左下标向右移动。
      imoving=1;  // 下次循环将移动左下标。
      continue;
    }

    if (imoving==1) // 移动左下标的情况。
    {
      // 如果左下标位置元素的值小等于中心轴，继续移动左下标。
      if (arr[ileft]<=itmp) { ileft++; continue; }

      // 如果左下标位置元素的值大于中心轴，把它填到右下标的坑中。
      arr[iright]=arr[ileft];
      iright--;   // 右下标向左移动。
      imoving=2;  // 下次循环将移动右下标。
      continue;
    }
  }

  // 如果循环结束，左右下标重合，把中心轴的值填进去。
  arr[ileft]=itmp;

  quicksort(arr,ileft);             // 对中心轴左边的序列进行排序。
  quicksort(arr+ileft+1,len-ileft-1); // 对中心轴右边的序列进行排序。
}

int main(int argc,char *argv[])
{
  int arr[]={44,3,38,5,47,15,36,26,27,2,46,4,19,50,48};
  int len=sizeof(arr)/sizeof(int);

  quicksort(arr,len);   // 调用插入排序函数对数组排序。

  // 显示排序结果。
  int yy; for (yy=0;yy<len;yy++) printf("%2d ",arr[yy]); printf("\n");

  // system("pause");  // widnows下的C启用本行代码。

  return 0;
  ```
