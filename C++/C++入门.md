[TOC]

# 一、C++初识

## 1、注释

> 1、单行注释：//
> 2、多行注释：/*      */

## 2、常量

> 1、#define宏常量：`#define 常量名 常量值 `
>
> 2、const修饰的变量：`const 数据类型 常量名=常量值`

## 3、关键字

> char、int、class、long、float……



# 二、数据类型

## 1、整形

短整型：short   整形：int   长整型：long   长长整形：long long

## 2、sizeof

作用：统计数据类型所占内存大小

语法：`sizeof(数据类型/变量)`

## 3、浮点型

单精度：float（4字节）

双精度：double（8字节）

`float f3=3e2//3*10^2`

`float f1=3e-2//3*0.1^2`

## 4、字符型

`char ch='a'//只能有一个字符，占用一个字节`

## 5、转义字符

\n 换行、\t 水平制表符……

作用：表示一些不能显示出来的ASCII字符

## 6、字符串类型

1、C语言风格：char 变量名[]=“字符串值”

2、C++风格：string 变量名=“字符串值”

`string`类提供了大量的成员函数来操作字符串，包括但不限于：

- `size()` 和 `length()`：返回字符串的长度。
- `empty()`：检查字符串是否为空。
- `append()` 和 `+=`：在字符串末尾添加字符或另一个字符串。
- `insert()`：在指定位置插入字符或字符串。
- `erase()`：删除指定位置的字符或子串。
- `replace()`：替换指定位置的字符或子串。
- `substr()`：获取子串。
- `find()`：查找子串或字符的位置。
- `compare()`：比较两个字符串。
- `c_str()`：返回一个指向以空字符结尾的字符数组的指针，该数组的内容与字符串相同。

### 3. 字符串元素访问

你可以通过下标操作符`[]`或`at()`成员函数来访问字符串中的单个字符：

```cpp
std::string s = "Hello";  
char c1 = s[0]; // 访问第一个字符，结果为'H'  
char c2 = s.at(1); // 访问第二个字符，结果为'e'
```

注意，使用`at()`成员函数时，如果下标越界，它会抛出`std::out_of_range`异常，而`[]`操作符则不会。

### 4. 字符串比较

你可以直接使用比较操作符（如`==`、`!=`、`<`、`<=`、`>`、`>=`）来比较两个`string`对象。

### 5. 字符串流

C++的`<sstream>`库提供了字符串流的功能，使得你可以方便地将字符串与其他数据类型进行转换。

### 6. 可变性和效率

C++的`string`类型是可变的，意味着你可以随时修改字符串的内容，而不需要担心内存管理的问题。同时，`string`类型的实现通常也是高效的，会在需要时自动调整内部缓冲区的大小。

## 7、布尔类型bool

> true —真（1）
>
> false —假（0）

`bool flag=true;`

`bool flag=false;`

`//占用一个字节`

## 8、数据的输入

`cin >>变量名`

既通过键盘输入值后赋值给变量



# 三、运算符

## 1、算术运算符

### (1)、++：

前置递加，如++a; 含义为先让变量+1，再进行表达式运算

后置递加，如a++; 含义为先进行表达式运算，再让变量加1

### (2)、––:

前置递加，如––a; 含义为先让变量–1，再进行表达式运算

后置递加，如a––; 含义为先进行表达式运算，再让变量减1

## 2、赋值运算符

+=：如a=5;若a+=1;则a=6,既a+1=6:

减、乘、除、模类似；

## 3、比较运算符

有==、!=、<、>、<=、>=等；

## 4、逻辑运算符

！：非

&&：与

||：或



# 四、程序流程结构

## 1、选择结构

### （1)、if语句

```c++
if()
{

}
else
{

}
```

多条件if语句

```c++
if()
{

}
else if()
{

}
else
{

}
```

嵌套if语句

```c++
if()
{
    if()
    {
        
    }
    else if()
    {
        
    }
    else
    {
        
    }
}
else
{
    
}
```

### (2)、三目运算符

语法：`表达式1？表达式2:表达式3`

含义：1真则执行2，否则执行3

### (3）、switch语句

```c++
switch()
{
    case 1:;break;
    case 2:;break;
    default:;
        break;
}
```



## 2、循环结构

### (1)、while语句

```c++
while()
{
    
}
```

### (2)、dowhile语句

```c++
do
{
    
}while();
```

案例：判断是否为水仙花数

```c++
#include<iostream>
#include<string>
#include<stdlib.h>
using namespace std;

int main(){
    int num=100;
    int i = 0;
    do
    {
        int a = num % 10;
        int b = num / 10 % 10;
        int c = num / 100;
        if(a*a*a+b*b*b+c*c*c==num)
        {
            i++;
            cout << num << endl;
        }
        num++;
    } while (num < 1000);
    cout <<"have" << i << "flower"<< endl;
    return 0;
}
```

### (3)、for循环

```c++
for( ; ; )
{
    
}
```

案例：

```c++
int num = 1;
    int i = 0;
    for (num=1; num<=100; num++)
    {
        int num1 = num % 10;
        int num2 = num / 10 ;
        if (num1 == 7||num2 == 7||num % 7 == 0)
        {
            cout << "knock table" << endl;
            i++;
        }
        else
        {
            cout << num << endl;
        }
        
    }
    //统计打印了多少个“敲桌子“
    cout << i << endl;
```

### (4)、嵌套循环

```c++
for( ; ; )
{
    for( ; ; )
    {
    
    }
}
```

案例：乘法口诀表

```c++
int i = 0;
    int j = 0;
    for (i = 1; i < 10;i++)
    {
        for (j = 1; j < i+1;j++)
        {
            int c = j * i;
            cout << j<< "*"<<i<< "="<< c<<"\t" ;
            // cout << "||";
        }
        cout << endl;
    }
```

## 3、跳转语句

### (1)、break语句

1）、Switch语句中

2）、循环语句中

3）、嵌套循环语句中

### (2)、continue语句

作用：跳过本次循环未执行部分执行下一循环 

### (3)、go to语句

语法：goto 标记；



# 五、数组

## 1、一维数组

### (1)、定义

数据类型 数组名[数组长度]={值1、值2、……};

### (2)、数组名

1）、可以获取整个数组占用空间大小（sizeof(arr)）

2）、可以通过数组名获取数组首地址

### (3)、案例

1）五只小猪称重

```c++
int arr[5] = {300, 350, 200, 400, 250};
int i = 0;
int max = arr[0];
for (i = 1; i < 5; i++)
{
  if(arr[i]>max)
  {
      max = arr[i];
  }
}
cout << max << endl;
```

2)冒泡排序

```c++
    int temp=0;
    int arr[9] = {2,4,0,5,7,1,3,8,9};
    for (int i = 0; i < 9-1;i++)
    {
        for (int j = 0; j<9-i-1;j++)
        {
            if (arr[j] > arr[j + 1])
            {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }    
    }
    for (int i = 0; i < 9;i++)
    {
        cout << arr[i] << " ";
    }
//排序总轮数=元素个数-1
//每轮对比次数=元素个数-排序轮数-1
```

## 2、二维数组

### (1)、定义与数组名

与一维相似



# 六、函数

## (1)、函数调用

```c++
int Add()
{
    
}
int main()
{
    int sum=Add();
}
```

## (2)、值传递

形参发生改变不会影响实参



# 七、指针

## (1)、定义和使用

```c++
int a=10;
//定义
int *p;
//记录
p=&a;
//使用，修改数据。*:解引用操作符，代表找到指向的数据
*p=1000;
```

## (2)、指针所占内存空间

32位占4字节

64位占8字节

## (3)、空指针和野指针

空指针：`int *p=NULL;`

用于指针变量初始化，不能访问

野指针：`int *p=(int*)0x1100`(指向非法地址)

## (4)、const修饰指针

1）：常量指针

`const int *p=&a;`指向可以修改，但指针指向的值不能修改

例：`* p=20;//错误 p=&b;//正确`

2）：指针常量

`int * const p=&a;`指针指向不可以改，指针指向的值可以改

3）：`const int * const p=&a;`都不能改

## (5)、指针与数组

利用指针访问数组元素

```c++
int mian()
{
    int arr[]={1,2,3,4,5,6,7,8,9};
    int *p=arr;
    for(int i=0;i<10;i++)
    {
        cout<<*p<<endl;
        p++;
    }
    return 0;
}
```

## (6)、指针与函数

地址传递

```c++
void swap(int *p1,int *p2)
{
    
}
int mian()
{
    swap(&a,&b);
}
//值传递不改变实参
//地址传递会改变实参
```

## (7)、指针、函数、数组配合案例

```c++
void MP(int *arr,int se)
{
    for (int i = 0; i < se - 1; i++)
    {
        for(int j=0;j<se-1-i;j++)
        {
            if(arr[j]>arr[j+1])
            {
                int temp = 0;
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
int main()
{
    int arr[] = {4, 3, 6, 9, 1, 2, 10, 8, 7, 5};
    int se = sizeof(arr) / sizeof(arr[0]);
    MP(arr,se);
    for (int i = 0; i < se; i++)
    {
        cout << arr[i] << " ";
    }
    return 0;
}
```



# 八、结构体

## (1)、结构体赋值

```c++
struct student
{
    string name;
    int age;
    int score;
};
int main()
{
    //第一种
    struct student s;
    s.name="某某";
    s.age=12;
    s.score=100;
    //第二种
    struct student s={"某某",12,100};
}
```



## (2)、结构体数组

```c++
//定义
struct student
{
    string name;
    int age;
    int score;
};
int main()
{
    //结构体数组
    struct student arr[3]=
    {
        {"张三"，12,12};
        {...};
        {...};
    }
};
//赋值
arr[2].name="李四"；
    ....
    //遍历
    for(int=0;i<3;i++)
    {
        cout<<arr[i].name;
    }
```

## (3)、结构体指针

```c++
 //定义
struct student
{
    string name;
    int age;
    int score;
};
int main()
{
    //创建变量
    struct student s={"张三"，12,12};
    //指针
    struct student *p=&s;
    //打印
    cout<<p->name;
    return 0;
}
```

## (4)、结构体传参

```c++
struct student
{
    string name;
    int age;
    int score;
};
//值传递
void printstu(struct student s)
{
    cout<<s.name;
};
//地址传递
void printstu(struct student *p)
{
    cout<<p->name;
};
int main()
{
    //创建变量
    struct student s;
    s.name="张三"；
    s.age=12;
    printstu(s);
    printstu(&s);
    return 0;
}
```

