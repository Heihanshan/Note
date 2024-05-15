# 引用

## 1、语法

数据类型 &别名=原名

`int &b=a;`

b就是a的别名，a和b的地址是相同的，指向同一片空间

## 2、性质

(1)、引用必须初始化

`int &b;`错

`int &b=a;`对

(2)、引用初始化之后不可再更改

```c++
int &b;
int &b=a;
int c=20;
 &b=c;
```

错

## 3、引用做函数参数

```c++
int mySwap(int &a,int &b)
{
    int temp=a;
    a=b;
    b=temp;
}

int main()
{
    int a=10,b=20;
    mySwap(a,b);
}
//和地址传递一样可以改变实参的值，因为形参是实参的别名，两个变量指向同一块空间，且在函数中不用像地址传递一样解引用参数
```

## 4、引用做函数返回值

```cpp
int &text()
{
    static int a=10;//加了static，a由栈区变为为全局区，由编译器释放
    return a;
}

int main()
{
    int &ref=text();
    cout<<ref<<endl;//输出为10
    text()=1000;
    cout<<ref<<endl;//输出为1000
    return 0;
}
//在这里，引用做函数返回值，返回a的引用，所以函数可以作为左值(text()=1000;)，相当与对a赋值
```

## 5、引用的本质

本质：常量指针

即：`int& ref=a;`为`int* const ref=&a;`

## 6、常量引用

语法：`const int &ref=10;`

说明：编译器用一块临时空间存放10后，再让ref成为临时空间变量的别名，即`int temp=10; const int &ref=temp;`

值不可修改

作用：修饰形参，防止误操作，即在调用函数时在引用形参处加上const后可以保证实参不会改变
