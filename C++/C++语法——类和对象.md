# 函数提高

## 函数的默认参数

```c++
int func(int a,int b=10,int c=20)
{
    
}

int main()
{
    func(10);
}
//若函数参数有默认值，则在调用时可以不输入此参数，若输入了实参但形参与实参的值不同，则用实参的值
```

注意：

1、某个位置有默认参数，则从此位置开始后面的参数都要有默认值

2、若函数声明有默认参数，则函数实现不能有默认参数，只能有一个有默认参数



## 函数占位参数

```c++
void func(int a,int)
{
    cout<<"this"<<endl;
}

int main()
{
    func(10,10);
}
//不管形参有没有用到，形参不是默认参数则需要传实参，在这里，a后面的int就是占位参数，需要传实参

void func(int a,int=10)
{
    cout<<"this"<<endl;
}

int main()
{
    func(10);
}
//占位参数可以有默认值，那么调用时可以不传参
```



## 函数重载

作用：可以让函数名相同，提高复用性

条件：

1、同一作用域

2、函数名称相同

3、函数参数类型不同，或者个数不同，或者顺序不同

```c++
//参数个数不同
void func(int a)
{
    cout<<"this"<<endl;
}

void func()
{
    cout<<"this"<<endl;
}

//参数类型不同
void func(double a)
{
    cout<<"this"<<endl;
}

void func(int a)
{
    cout<<"this"<<endl;
}

//参数顺序不同
void func(double a,int b)
{
    cout<<"this"<<endl;
}

void func(int a,double b)
{
    cout<<"this"<<endl;
}

int main()
{
    func(10);
}
//函数返回值不能作为函数重载的条件
```

注意事项：

1、引用作为重载的条件

```c++
void func(int &a)
{
    cout<<"this"<<endl;
}

void func(const int &a)
{
    cout<<"this"<<endl;
}

int main()
{
    int a=10;
    func(a);//调用第一个函数
    func(10);//调用第二个函数
}
```

2、函数重载与默认参数

```c++
void func(int a,int b=10)
{
    cout<<"this"<<endl;
}

void func(int a)
{
    cout<<"this"<<endl;
}

int main()
{
    int a=10;
    func(a);//这种情况会报错，因为可以调用第一个函数也可以调用第二个函数
    func(10,20)//合法，调用的是第一个函数
}
```



# 类和对象

## 一、封装

### 1.1 设计圆类,求圆的周长

```c++
const double PI=3.14;
class Circle
{
//访问权限(此处为公共权限)
public:
    
    //属性——半径
    int m_r;
    //行为——获取圆的周长
    double calculateZC()
    {
        return 2*PI*m_r;
    }
};

int main()
{
    //通过上面定义的圆类创建具体的圆(对象)
    Circle cl;//实例化，通过一个类创造一个对象
    //给圆对象的属性进行赋值
    cl.m_r=10;
    
    //输出圆的周长
    cout<<"圆的周长为:"<<cl.calculateZC()<<endl;
    
    return 0;
}
```

### 1.2 行为给属性赋值

```c++
class Student
{
public:
	//属性
	string m_Name;//姓名
	int m_Id;//学号


	//行为
	void showStudent()            //显示姓名和学号
	{
		cout << "姓名:" << m_Name  << "学号:" << m_Id << endl;
	}
    //给姓名赋值
    void setName(string name)
    {
        m_Name=name;
    }
    //给学号赋值
    void setId(int id)
    {
        m_Id=id;
    }
};

int main()
{
    Student s1;
    s1.setName("张三");
    s1.setId(1);
    return 0;
}
//类中的属性和行为同一称为成员
//属性也称为成员属性/成员变量
//行为也称为成员函数/成员方法
```

### 1.3 封装的访问权限

1、public  公共权限：成员在类内可以访问，类外也可以访问

2、protected  保护权限：类内可以访问，类外不能访问，儿子也可以访问父亲中保护的内容(继承)

3、private  私有权限：类内可以访问，类外不能访问，儿子不可以访问父亲的私有内容(继承)

```c++
class Person
{
    public:
    	string m_Name;
    protected:
    	string m_Car;
    private:
    	int m_Password;
    public:
    	void func()           //类内可以访问
        {
            m_Name="张三";
            m_Car="拖拉机";
            m_Password=123456;
        }
};
```



### 2.1 struct与class的区别

> struct 默认权限为公共
>
> class 默认权限为私有



### 2.2 成员属性设置为私有

```c++
class Person
{
public:
    //设置姓名
    void setName(string name)
    {
        m_Name=name;
    }
    //获取姓名
    string getName()
    {
        return m_Name;
    }
    //获取年龄
    int getAge()
    {
        return m_Age;
    }
    //设置偶像
    void setIdol(string idol)
    {
        m_Idol=idol;
    }
    //设置年龄
    void setAge(int age)
    {
        if(age<0||age>100)
        {
            cout<<"年龄输入有误，更改失败"<<endl;
            return;
        }
        m_Age=age;
    }
    
private:
    string m_Name;//可读可写
    int m_Age=18;//可读，可写，但要求在0-100岁之间
    string m_Idol;//只写
};
int main()
{
    Person p;
    p.setName("张三");
    p.getName();
    p.getAge();
}
//这里我们在私有权限内定义了成员属性，并给出了相关访问要求，然后在公共权限内定义函数来完成相应要求
//在设置年龄处我们在函数内用if语句限制了年龄的更改区间(有效性验证)
```

可以看出我们设置类一般将属性设置为私有，在共有处创建接口函数

### 2.3 类的作用域

1、定义一个Point.h(hpp)文件存放类的声明：`class Point{}`

2、定义一个Point.cpp文件存放类内函数的实现，头文件包含加上#include”Point.h”，在函数名前需要加上类名“Point::”,如`void Point::getX()`

3、在vscode中，主函数文件不仅要包含类的头文件(.h)，还要包含类的实现文件(.cpp)

## 二、对象的初始化和清理

### 1.1 构造函数和析构函数

```c++
//构造函数进行初始化
class Person
{
public:
    //1、构造函数
    //没有返回值，不用写void
	//在类内的公共区域，与类名一致
	//可以有参数，可以重载
	//创建对象时，构造函数会自动调用，且只调用一次
    Preson()
    {
        cout<<"这个是构造函数"<<endl;
    }
    
    //2、析构函数
    //没有返回值，不用写void
    //在类内的公共区域，与类名一致,在名称前加~
    //可以有参数，可以重载
    //对象在销毁前，析构函数会自动调用，且只调用一次
    ~Person()
    {
        cout<<"这个是析构函数"<<endl;
    }
}
//若类不写构造和析构函数，编译器会自动写空实现的构造和析构函数并调用
```

### 1.2 构造函数的分类及调用

#### 1、构造函数的分类

```c++
class Person
{
public:
    //分类
    //1、无参构造函数(默认构造)
    Preson()
    {
        cout<<"这个是构造函数"<<endl;
    }
    //2、有参构造函数
    Preson(int a)
    {
        age=a;
        cout<<"这个是构造函数"<<endl;
    }
    
    //（普通构造函数:上面写过的构造函数都是）
    //3、拷贝构造函数
    Person(const Person &p)
    {
        //将p的所有属性拷贝我身上
        age=p.age;
    }
    
    ~Person()
    {
        cout<<"这个是析构函数"<<endl;
    }
    
    int age;
};
//在这里，有参构造函数可以给成员属性初始化,拷贝构造函数则将同一个类的一个对象的属性的值传给我的类的属性
```

#### 2、类中构造函数的调用

```c++
//此处接上面的分类里的代码
void test01()
{
    //1、括号法
    Person p1;//会调用无参构造函数,不要在p1后面写(),会被识别为函数声明
    Person p2(10);//会调用有参构造函数
    Person p3(p2);//会调用拷贝构造函数
    
    //显示法
    Person p1;//无参
    Person p2=Person(10);//有参
    Person p3=Person(p2);//拷贝
    Person(10);//匿名对象,特点是当前行执行完后系统立即回收匿名对象,也就是执行一次构造和析构函数就结束
    //不要用拷贝构造函数初始化匿名对象，例如：Person(p3);是错误的,会被识别为创建p3对象
    
    //隐式转换法
    Person p4=10;//相当于Person(10);
    Person p5=p4;//拷贝
}
```

### 1.3 拷贝构造函数调用时机

```c++
class Person
{
public:
    //无参构造函数(默认构造)
    Preson()
    {
        cout<<"这个是无参构造函数"<<endl;
    }
    //有参构造函数
    Preson(int a)
    {
        age=a;
        cout<<"这个是有参构造函数"<<endl;
    }

    //拷贝构造函数
    Person(const Person &p)
    {
        //将p的所有属性拷贝我身上
        age=p.age;
    }
    
    ~Person()
    {
        cout<<"这个是析构函数"<<endl;
    }
    
    int age;
};

//1、使用已经创建完毕的对象初始化一个新对象
void text01()
{
    Person p1(20);//这里调用默认构造函数
    Person p2(p1);//这里调用的是拷贝构造函数
}
//2、值传递方式给函数参数传值
void doWork(Person p)//因为下面调用时传进来一个类，所以形参创建时会调用拷贝构造函数
{
    ...
}
void text02()
{
    Person p;//这里调用默认构造函数
    doWork(p);
}

//值方式返回局部对象
Person doWork2()
{
    Person p1;//这里调用的是默认构造函数
    return p1;
}
void Text03()
{
    Person p=doWork2();//这里调用的是拷贝构造函数
}
```

### 1.4 构造函数调用规则

```c++
//创建一个类C++编译器会给每个类添加至少3个默认函数(若自己没创建)，分别是默认构造、析构构造、拷贝构造
//1、如果写了有参构造函数，编译器就不再提供无参(默认)构造函数,编译器依然提供拷贝构造函数(若自己没创建).(此时若自己也没提供默认构造函数，则创建对象时需要调用的的话编译器就会报错，例如：Person p;此时需要调用默认构造函数,而Person p(10)则需要调用有参构造函数，不需要调用无参构造函数)
//2、如果写了拷贝构造函数，编译器就不再提供普通构造函数(有参、无参).
//以上是说在我们创建对象时编译器需要调用某个构造函数，而我们没写，编译器也没提供的话就会报错，上面两种是会出现不提供的情况
```

### 1.6 深拷贝与浅拷贝

浅拷贝：简单的赋值拷贝操作，如编译提供的拷贝构造函数中直接等与某值的操作，如`m_Age=p.m_Age; `

深拷贝：在堆区重新申请空间，进行拷贝操作

```c++
class Person
{
public:
    //无参构造函数(默认构造)
    Preson()
    {
        cout<<"这个是无参构造函数"<<endl;
    }
    //有参构造函数
    Preson(int age,int height)
    {
        m_Age=age;
        //开辟int类型空间，用m_Height接收
        m_Height=new int(height);
        cout<<"这个是有参构造函数"<<endl;
    }
    
    //提供拷贝构造函数，编译器不再提供(在编译器提供的拷贝构造函数中执行的是浅拷贝，m_Height会指向相同的地址，当销毁对象时，在栈中会先销毁p2,并调用析构函数释放堆区数据，而销毁p1时会再次调用析构释放空指针导致运行出错，要解决这个问题，需要自己在拷贝构造函数中为p2也开辟空间)
    Person(const Person &p)
    {
        cout<<"拷贝构造函数的调用"<<endl;
        m_Age=p.m_Age;
        //m_Height=p.m_Height 编译器提供的拷贝构造函数中的对这个的属性操作
        //深拷贝操作
        m_Height=new int(*p.m_Height)
    }
    
    
    //析构函数
    ~Person()
    {
        //析构代码，在对象销毁前调用，可用于将堆区数据释放
        if(m_Height)
        {
            delete m_Height;
            m_Height=NULL;
        }
        cout<<"这个是析构函数"<<endl;
    }
    
    int m_Age;
    int *m_Height;
};

int main()
{
    Person p1(18,160);
    Person p2(p1);
}
//如果属性有在堆区开辟的需要自己提供拷贝构造函数开辟空间，防止重复释放空间
```

### 1.7 初始化列表

作用：初始化类属性

```c++
class Person
{
public:
    //传统初始化操作(有参构造函数)
    Person(int a,int b,int c)
    {
        m_a=a;
        m_b=b;
        m_c=c;
    }
    
    //初始化列表初始化属性
    Person():m_a(10),m_b(20),m_c(30)
    {
        
    }
    
    //为了让创建的对象能有不同的属性值，改为以下方式,这样仍需传参
    Person(int a,int b,int c):m_a(a),m_b(b),m_c(c)
    {
        
    }
    
    int m_a;
    int m_b;
    int m_c;
};

int main()
{
    //传统
    Person p(10,20,30);
    //有初始化列表
    Person p;
}
//相比之下传统方式似乎更便捷，但初始化列表效率更高，因为是直接声明一个有初始值的类型，省略了赋值操作，传统的是先声明类再进行赋值操作，且有初始化列表就不用在构造函数内写赋值语句
```

### 1.8 类对象作为类的成员

```c++
class Phone
{
public:
    //构造函数
	Phone(string pName)
    {
        m_PName=pName;
    }
    //手机品牌名
    string m_PName;
};

class Person
{
public:
    //构造函数
	Person(string name,string pName):m_Name(name),m_Phone(pName)
    {
        
    }
    
    //人名
    string m_Name;
    //手机(Phone类对象,Person类成员)
    Phone m_Phone;
}

int main()
{
    Person p("张三","华为");
}
//1.在Person的构造函数中，初始化列表时，String类型的pName将值传给了Phone类型的m_Phone，这是因为这里实际进行了Phone m_Phone=pName;也就是隐式转换法初始化对象的操作，所以没问题
//2.在创建对象时，若只创建了Person类对象，同时其他类的对象(m_Phone)作为本类的成员时，会先其他类对象，再创建Person类，释放时先释放本类对象，再释放本类中作为成员的类对象(与构造相反)
```

### 1.9 静态成员

#### 静态成员变量

1、特点
    1、所有对象共享一份数据，即定义Person p1，Person p2时，其中的m_A的值是相同的(不同对象的静态成员调用的是同一地址的值)
    2、编译阶段就分配空间
    3、类内声明，类外初始化操作

2、访问方式
    1、通过对象进行访问
    cout<<p1.m_A<<endl;
    2、通过类名进行访问
    cout<<Person::m_A<<endl;

3、静态成员变量有访问权限

```c++
class Person
{
public:
    //特点
    //1、所有对象共享一份数据，即定义Person p1，Person p2时，其中的m_A的值是相同的(不同对象的静态成员调用的是同一地址的值)
    //2、编译阶段就分配空间
    //3、类内声明，类外初始化操作

	static int m_A;//静态成员变量,类内声明，不能用构造函数初始化列表初始化
    //静态成员变量有访问权限
private:
    static int m_B;
}
int Person::m_A=100;//类外初始化,要告诉是Person作用域下的静态成员，不然就是全局变量
int Person::m_B=100;

int main()
{
    Person p1;
    
    //访问方式
    //1、通过对象进行访问
    cout<<p1.m_A<<endl;
    //2、通过类名进行访问
    cout<<Person::m_A<<endl;
    //cout<<Person::m_B<<endl;这个是错的，外部无法访问到
}

/*静态成员变量需要在类外部进行初始化的原因主要与其存储方式和生命周期有关。静态成员变量不属于任何类的对象实例，而是属于类本身。它们存储在程序的静态存储区,它们的初始化需要在所有对象创建之前完成，这只能在类的作用域之外进行*/
```

#### 静态成员函数

特点：

1、所有对象共享同一个函数

2、静态成员函数只能访问静态成员变量

3、静态成员函数也有访问权限

```c++
class Person
{
public:
    static void func1()
    {
        m_A=100;//静态成员函数可以访问静态成员变量
        m_B=200;//无法访问成员变量，会报错
        cout<<"静态成员函数1的调用"<<endl;
    }
    static int m_A;//静态成员变量
    int m_B;
    
    //静态成员函数也有访问权限
private:
	static void func2()
    {
        cout<<"静态成员函数2的调用"<<endl;
    }
};
int m_A=10;
//调用静态成员函数
void text01()
{
    //1.通过对象访问
    Person.p;
    p.func1();
    //2.通过类名访问
    Person::func1();
}
int main()
{
    text01();
}
```

## 三、C++对象模型和this指针

### 1、成员变量和成员函数分开存储

```c++
//1、空对象内存为1，因为每个空对象也有自己的空间区分占内存的位置
class Person
{
    
};
int main()
{
    Person p;
    cout<<sizeof(p)<<endl;
}
//2、类中仅有m_A及同时有m_A和m_B时结果都为4,说明有非静态成员时则按其大小给对象分配内存，且静态成员不占对象大小
lass Person
{
    int m_A;//非静态成员变量，属于类对象上
    static int m_B;//静态成员变量，不属于类对象上
    //3.加上非静态和静态成员函数结果还是4，都不属于类的对象上
    void func1(){}
    static void func2(){}
}
int Person::m_B=0;
int main()
{
    Person p;
    cout<<sizeof(p)<<endl;
}
```

### 2、this指针的作用

作用：

1、解决名称冲突

2、返回对象本身用*this

```c++
class Person
{
    public:
    Person(int age)
    {
        age=age;
    }
    //这个构造函数会导致主函数的打印会出错，有两个方法解决，第一是让成员变量名称与成员函数的参数不一致，第二是加this指针
    //例如：
    Person(int age)
    {
        //this 指针指向 被调用的成员函数 所属对象(在这里p1在调用，所以指向p1)，谁调用就指向谁
        this->age=age;
    }
    
    Person& PersonAddAge(Person &p)//这里用引用的方式返回调用本函数的对象本身，如果没有&那返回的就是调用本函数的对象的拷贝
    {
        this->age+=p.age;
        
        return *this;//这里返回调用本函数的对象本身
    }
    
    int age;
};

int main()
{
    Person p1(18);
    cout<<"p1的年龄"<<p1.age<<endl;
    Person p2(10);
    Person p3(10);
    p3.PersonAddAge(p2);//把p2的年龄加到p3上
    cout<<"p2的年龄"<<p2.age<<endl;
    //链式编程思想，可以无限往后加
    p3.PersonAddAge(p2).PersonAddAge(p2).PersonAddAge(p2).PersonAddAge(p2);//因为p3.PersonAddAge(p2)返回的是加完p2年龄的p3，所以能在后面再次调用成员函数，一直调用
    return 0;
}
```

### 3、空指针访问成员函数

```c++
//1.空指针可以调用成员函数，但要注意用没有用到this指针
class Person
{
    public:
    void showClassName()
    {
        cout<<"this is Person class"<<endl;
    }
    
    void showClassAge()
    {
        //解决空对象调用问题
        if(this==NULL)
        {
            return;
        }
        cout<<"this is Person's age="<<m_Age<<endl;//这里的属性调用其实默认有个"this->",如果对象为空，调用时this也为空，则程序错误，而showClassName没有属性的调用，不会访问空指针，因此空对象也能正常调用
    }
    
    int m_Age;
};

int main()
{
    Person *p=NULL;
    p->showClassName();
    p->showClassAge();
    
}
```

### 4、const修饰成员函数

```c++
//1.加上const的成员函数称为常函数
//2.常函数内不可以修改成员属性
//3.成员属性声明时加关键字mutable后，在常函数中依然可以修改
//4.声明对象前加const称该对象为常对象
//5.常对象只能调用常函数
class Person()
{
    public:
    //成员函数
    //this 指针的本质是指针常量指针的指向是不可以修改的(调用的过程中始终指向调用的那个对象)
    void showPerson()
    {
        this->m_A=100;//this此处本质：Person *const this;若要指针指向的值也不能修改则为const Person *const this;在这里值可以改
    }
    //常函数，本质上是给this加了个const，即const Person *const this;
    void showPerson()const//在函数尾加
    {
        this->m_A=100;//在这里值不能改，因为在常函数中
        this->m_B=100;//这里不会报错，因为加了关键字mutable
    }
    int m_A;
    mutable int m_B;//特殊变量，即使在常函数中，也可以修改这个值
};
int main()
{
    const Person p;//常对象，属性不能修改，除非属性加mutable
    p.m_A=100;//报错
    p.m_B=100;//不报错
    //常对象只能调用常函数
    p.showPerson();
}
```

## 四、友元

1、关键字：friend

2、可以访问private中的内容或者让private中的某些内容被访问

3、三种实现：

> 全局函数做友元
>
> 类做友元
>
> 成员函数做友元

### 1、全局函数做友元

```c++
知识点：在类内给全局函数加关键字friend后成为友元，便可以访问类的私有内容
//建筑物类
class Building
{
    friend void goodGay(Building *building);
    public:
    //构造函数
    Builing()
    {
        m_SittingRoom="客厅";
        m_BedRoom="卧室";
    }
    string m_SittingRoom;//客厅
    private:
    string m_BedRoom;//bedroom
};
//全局函数
void goodGay(Building &building)
{
    cout<<"goodGay全局函数正在访问："<<building->m_SittingRoom<<endl;
    cout<<"goodGay全局函数正在访问："<<building->m_BedRoom<<endl;//此时无法访问，因为为私有属性,当在类内加了friend void goodGay(Building *building);后便可以访问
}
int main()
{
    Building building;
    goodGay(&building)
}
```

### 2、类做友元





## 、继承

## 、多态

