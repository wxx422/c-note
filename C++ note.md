## 1、概述

面向对象（Object Oriented Programming）

以对象为基础，以消息或事件驱动对象执行处理的技术。将数据和对数据的操作封装在一起，抽象成类，采用数据抽象和信息隐藏，类之间相互交互，共同构成大型的面向对象系统。

相关概念：

类（Class）：具有相同属性和行为的一组对象。属性和操作的集合。类的对象是实例。

对象（Object）：系统中描述客观事物的实体。

封装（Encapsulation）：将数据和操作封装成一个独立个体，对类外隐藏实现细节。

继承（Inheritance）：对现实世界的模拟。允许在已有类基础上通过增加新特性而派生出新的类。原有的类称为基类（base class），新建立的类称为派生类（derived class）。

多态性（Polymorphism）：同一函数名对应多个具有相似功能的不同函数。相同的调用方式，不同对象收到相同的消息后产生不同的行为。两种形式的多态：静态和动态。

## 2、快速入门

```C++
#include <iostream>
#include <vector>

//局部变量、函数参数在栈中
//A 调用 B，A 将 B 需要的参数入栈、压入 A 中的返回地址、在栈中分配局部变量，弹出返回地址返回到 A 中，分配给 B 的空
//间回收，B 中的局部变量释放
//函数重载
int max(int a, int b);
double max(double a, double b);

int main(int argc, char *argv[])
{
    std::cout<<"Hello World"<<std::endl;
        
    std::vector<int> a;
    a.push_back(10);
    a.push_back(11);
    a.push_back(12);
        
    int i = 0;
    for(i; i < a.size(); ++i)
    {   
            std::cout<<a[i]<<std::endl;
    }   

    //C 风格的字符串
    char str[128] = "Hello, world!";
    char *p = "Hello, World!";
        
    std::string s;
    s = "nihaoshijie";
    s += "!!!";
    std::cout<<s<<std::endl;

    int b = 1;
    int c = 2;
    std::cout<<max(b, c)<<std::endl;

    double d = 1.1;
    double e = 2.2;
    std::cout<<max(d, e)<<std::endl;

    int a = 3;
    int &b = a;
    a++;
    b++;

    return 0;
}

int max(int a, int b)
{
    return (a>b?a:b);
}

double max(double a, double b)
{
    return (a>b?a:b);
}
```

## 5、string

string 是一个类，包括追加、比较等操作。

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string str1 = "nihaoshijie";
    string str2 = "nihao";
    cout << str1.size() << endl;

    int nLines = 0;
    while(getline(cin, str2))
    {   
        if(str2 == "q")
        {   
            break;
        }   
        str1 += str2;
        str1 += "\n";
        nLines++;
    }   
    cout << "total lines" << nLines << endl;
    cout << str1 << endl;
    return 0;
}
```

## 6、vector

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main()
{
    string str;
    vector<string> v;
    while(getline(cin, str))
    {   
        if(str == "q")
        {   
            break;
        }   
        v.push_back(str);
    }    

    int nChars = 0;
    for (int i = 0; i < v.size(); ++i)
    {   
        string s = v[i];
        nChars += s.size();
        cout << i << s << " " << s.size() << endl;
    }   
    
    cout << "total lines:" << v.size() << " " << "total chars" << nChars << endl;
    
    return 0;
}
```

## 7、函数

**引用**

作为函数参数：

1、在函数内部可以修改实参；

2、大型的结构体或对象作为函数参数时，为避免拷贝可以考虑采用指针或者引用 传参。

引用作为函数返回值：

1、函数返回类型，需要在函数名之前加 &；

2、返回引用类型的好处是不产生副本，不需要拷贝；

3、不能返回局部变量的引用。局部变量在函数返回后被销毁。（所以复制构造函数的时候需要把参数定义为引用，否则就是无限循环；返回类对象的时候返回引用，可以避免调用复制构造函数）

**默认参数：**

1、函数声明或定义时，给参数赋一个默认的值；

2、在函数调用时，省略具有默认值的参数。这时可以用默认参数来替代；

3、默认参数必须在参数表最右边。

```c++
#include <iostream>
using namespace std;

void move(int step = 1, int distance = 20);

void func(int i, int j = 10, int k = 20, int l = 30);

int main()
{
    move(2, 40);
    move(2);
    move();

    func(10, 20, 30, 40);
    func(10, 20, 30);
    func(10, 20);
    func(10);
    return 0;
}
```

**函数重载：**

是指在同一作用域内，有一组相同函数名，不同参数列表的函数（参数表形同，返回值不同，这种情况不成立），这组函数称为重载函数。

重载函数通常用来命名一组功能相似的函数，这样做减少了函数名的数量，避免了名字空间的污染，对于程序的可读性有很大的好处。

```c++
#include <iostream>
using namespace std;

int add(int a, int b)
{
    return a + b;
}

float add(float a, float b)
{
    return a + b;
}

double add(double a, double b)
{
    return a + b;
}

int main()
{
    int a = 10;
    int b = 10;
    add(a, b);
    float f1 = 10.1;
    float f2 = 20.2;
    add(f1, f2);
    return 0;
}
```

**函数模板：**

创建一个通用函数，奇函数返回值类型和形参类型不具体指定，用一个虚拟的类型来替代。这个通用的函数称为函数模板。

```c++
template <typename Type1, typename Type2>
```

**例子：**

```C++
#include <iostream>
using namespace std;

template <typename T>

T add(T a, T b)
{
    return a + b;
}

int main()
{
    int a = 10; 
    int b = 20; 
    cout << add(a, b) << endl;

    float f1 = 10.1;
    float f2 = 20.3;
    cout << add(f1, f2) << endl;

    return 0;
}
```

函数模板与函数重载有些类似，但是重载函数内部实现可以完全不同，单模板函数内部实现完全相同。

## 11、构造、析构

构造函数是特殊的成员函数，不需要用户调用，定义对象时被自动执行。构造函数名字与类名相同，无返回类型。构造函数可以重载，即可以有多个构造函数，参数列表不同。不能是 virtual 类型的。

析构函数是特殊的成员函数，执行对象的清理工作，而不是删除对象，在对象生命周期结束时，程序会自动执行析构函数。构造函数和析构函数是由用户定义的，但是是由程序自动调用的。

析构函数没有返回值，没有参数（所以不能重载，只能有一个析构函数）。先执行构造函数，后调用析构函数。一般声明为 virtual 类型。

```c++
#include <iostream>
using namespace std;

class Foo
{
public:
    Foo()
    {
        cout << "Foo constructor" << endl;
    }
    Foo(const Foo &foo)
    {
        cout << "Foo copy constructor" << endl;
    }
    ~Foo()
    {
        cout << "Foo deconstructor" << endl;
    }
};

class Bar
{
public:
    Bar()
    {
        cout << "Bar constructor" << endl;
    }
    Bar(const Bar &bar)
    {
        cout << "Bar copy constructor" << endl;
    }
    ~Bar()
    {
        cout << "Bar deconstructor" << endl;
    }
};

class Base
{
public:
    Base()
    {
        cout << "Base constructor" << endl;
    }
    ~Base()
    {
        cout << "Base deconstructor" << endl;
    }
};

class Derived : public Base
{
private:
    Foo m_foo;
    Bar m_bar;
public:
    Derived()
    {
        cout << "Derived constructor" << endl;
    }
    Derived(const Foo &foo, const Bar &bar);
    Derived(const Bar &bar, const Foo &foo);
    ~Derived()
    {
        cout << "Derived deconstructor" << endl;
    }
};

Derived::Derived(const Foo &foo, const Bar &bar) : m_foo(foo), m_bar(bar)
{
    cout << "Derived constructor with argument [Foo foo, Bar bar] passed by reference" <<endl;
}

Derived::Derived(const Bar &bar, const Foo &foo) : m_bar(bar), m_foo(foo)
{
    cout << "Derived constructor with argument [Bar bar, Foo foo] passed by reference" <<endl;
}

int main(int argc, char *argv[])
{
    Foo foo;
    Bar bar;

	cout << endl << "test case 1: " << endl;
    Derived deri_1;
    
    cout << endl << "test case 2: " << endl;
    Derived deri_2(foo, bar);

    cout << endl << "test case 3: " << endl;
    Derived deri_3(bar, foo);

    cout << endl << "test case end" << endl;

    return 0;
}
```

执行结果：

```shell
Foo constructor
Bar constructor

test case 1: 
Base constructor
Foo constructor
Bar constructor
Derived constructor

test case 2: 
Base constructor
Foo copy constructor
Bar copy constructor
Derived constructor with argument [Foo foo, Bar bar] passed by reference

test case 3: 
Base constructor
Foo copy constructor
Bar copy constructor
Derived constructor with argument [Bar bar, Foo foo] passed by reference

test case end

Derived deconstructor
Bar deconstructor
Foo deconstructor
Base deconstructor

Derived deconstructor
Bar deconstructor
Foo deconstructor
Base deconstructor

Derived deconstructor
Bar deconstructor
Foo deconstructor
Base deconstructor

Bar deconstructor
Foo deconstructor
```

解释：

程序 81 行对应结果 1 行；

程序 82 行对应结果 2 行；

程序 85 行对应结果 5-8 行，创建对象 deri_1，首先执行基类  Base 的构造函数，其次执行成员 m_foo, m_bar 的构造函数来构造成员，最后调用自身的构造函数（无参数的）；

程序 88 行对应结果 11-14 行；

程序 91 行对应结果 17-20 行；

最后销毁参数 deri_3, deri_2, deri_1, 析构函数执行顺序相同，与构造对象的顺序相反。C++ 标准规定以对象声明相反的顺序销毁这些对象；

销毁对象 bar, foo。

复制构造函数使用场景：

1、以其他对象作为参数创建新的对象时；

2、类对象（传值）作为函数参数时；

3、类对象作为函数返回值时；

## 13、静态成员

静态数据成员：

以 static 开头。静态数据成员各个对象共有，不属于某个具体的对象，所有对象都可以对他进行引用，读取和修改。若一个对象修改了该静态成员的值，则在其他各个对象中该数据成员值都会修改。

定义类时就为静态数据成员分配空间，不随对象的建立而分配空间（和C的static类似）。

定义完类之后就可以引用。

应用方法：类名::静态成员 或者 对象名.静态成员

在类内的静态数据成员仅仅是该成员的声明（不能在类内进行初始化），同时还需要在类外部进行定义。

静态成员函数：

在生命成员函数时在函数前添加 static 关键字就定义了静态成员函数。

与静态数据成员一样，静态成员函数也是类的一部分。

静态成员函数一般是为了处理静态的数据成员。

与一般成员函数的区别：非静态成员函数有 this 指针，静态成员函数没有 this 指针。因为静态成员函数在未定义类对象时就可以引用，因此静态成员函数不能访问本类中的非静态成员（成员函数和数据成员）。

## 14、const 对象和 const 成员

const 对象：

定义类对象时可以将其指定为 const 对象。定义 const 对象后不能再被修改。const 对象不能调用非 const 类型的成员函数（以免在函数中被执行修改操作）。

const 类名 对象名

类名 const 对象名

const 成员：

1、const 数据成员

在类内部使用 const 关键字来声明 const 数据成员。const 数据成员的值不能被修改。初始化时比较特殊，只能通过初始化列表初始化，不能在构造函数里赋值。

2、初始化列表

构造函数初始化列表以一个冒号开始，接着是以逗号分隔的数据成员列表，每个数据成员后面跟一个放在括号中的初始化式。

```c++
CTime::CTime()
	:m_nNum1(10), m_nNum2(10)
{
	//do something
}
```

3、const 成员函数

const 成员函数只能被 const 对象引用。const 成员函数内可以引用 const 数据成员，也可以引用非 const 数据成员，但不能修改非 const 数据成员的值。const 成员函数不能调用非 const 成员函数。

```c++
int getNum()const;
```

要把 const 放在函数后面，不能放前面，放在前面的含义是返回值是 const int，而不是说函数是 const 的。

## 15、友元

友元可以访问 private 成员。友元只能授予，不能索取，单向，不能传递。

友元函数：

在类体内使用 friend 关键字对友元函数进行声明；

将非成员函数声明为友元；

```c++
friend void func();	//func为非成员函数，不属于任何类
```

将其他类的成员函数声明为友元；

```c++
friend void CTime::getNum();	//getNum为CTime类的成员
```

友元类：

在类体重使用 friend 关键字将某类声明为自己的友元类。

```C++
friend CTime;
```

缺点：面向对象的基本原则包括封装性和信息隐蔽，友元可以访问其他类的私有成员，这是对封装的一个破坏。

## 16、运算符重载

CTime 重载 + 运算符实现两个 CTime 对象的相加。

首先需要定义一个重载的元素安抚函数，此后在执行被重载的运算符时，系统自动调用该运算符函数。运算符重载实际上是函数的重载。

运算符重载的格式：

返回类型 operator 运算符(参数列表)

```c++
CTime operator+(CTime &time1, CTime &time2)
```

重载的运算符函数可以作为一般的函数，也可以作为类的成员函数。

```c++
CTime CTime::operator+(CTime &time)	//这里不需要两个参数，因为展开之后是 this->opertaor+(time)
```

## 22、继承与派生基础

构造函数不能被继承，派生类的构造函数必须调用基类的构造函数来初始化基类成员。

派生类的构造函数调用顺序如下：

基类的构造函数

成员的构造函数

派生类自身的构造函数

析构顺序与构造顺序相反。

## 23、多态

静态多态：编译时的多态，可以通过函数重载来实现；

动态多态：运行时的多态，通过虚函数来实现。

通过基类的指针或引用指向派生类对象后，调用的均是基类的成员，不能访问派生类的成员。若要访问派生类中相同名字的函数，必须将基类中的同名函数定义为虚函数。基类的指针指向派生类对象后，就可以调用派生类的同名的成员函数。

将基类同名的函数定义为虚函数可以使用 C++ 关键字 virtual 来实现。

在基类成员函数声明前加 virtual 关键字。在派生类重新定义基类中的虚函数时，可以不用关键字 virtual 来修饰这个成员函数。在程序执行过程中，依据指针具体指向哪个类对象，或依据引用那个类对象，才能确定绑定哪个成员函数，实现动态绑定。

注意：

1、当在基类中将成员函数定义为虚函数后，在派生类中定义的虚函数必须与基类中虚函数同名，参数类型、顺序、个数一一对应。

若函数名相同，但参数不同，则属于函数重载，而不是虚函数。

函数名不同，则是不同的成员函数。

2、实现这种动态的多态时，必须使用基类的指针变量，并使该指针指向不同的派生类对象，通过调用指针指向的虚函数实现动态的多态性。通过对象名访问虚函数则不会实现动态多态性。

3、在派生类中没有重新定义虚函数时，与一般成员函数一样，当调用这种派生类的虚函数时，调用基类的虚函数。

4、可以把析构函数定义为虚函数，但是，不能把构造函数定义为虚函数（构造函数不能被继承，每个类调用自己的构造函数）。

5、多态是通过虚函数动态绑定实现。内部是通过虚函数表实现。调用时的执行速度慢。虚函数表是一张表，内部存储很多虚函数的地址。基类对象有一张，子类也有一张。初始时子类继承基类的表，若子类覆盖（重写）了基类的虚函数，则将子类的虚函数表对应项目替换为子类虚函数指针。

纯虚函数：

在基类中仅给出声明，不对虚函数实现定义，而在派生类中实现。纯虚函数在声明后要加 =0（否则编译不通过）

```c++
class <基类名>
{
	virtual <类型> <函数名>(<参数表>)=0;
	//……
};
```

抽象类：

含有纯虚函数的类称为抽象类，只能作为派生类的基类，不能定义对象，但可以定义指针。

在派生类实现纯虚函数后，定义抽象类对象的指针，并指向或引用子类对象。

1、在定义纯虚函数时，不能定义虚函数的实现部分；

2、在没有重新定义纯虚函数之前，不能调用这种函数。

```c++
//Shape.h
#ifndef SHAPE_H
#define SHAPE_H
#include <string>
using std::string;
class IShape
{
public: 
    virtual float GetArea() const = 0;
    virtual const string & GetName() const = 0;
};

#endif
```

```c++
//Circle.h
#ifndef CIRCLE_H
#define CIRCLE_H

#include "Shape.h"

class CCircle : public IShape
{
public:
    CCircle(float radius);
    virtual ~CCircle();
    virtual float GetArea() const;
    virtual const string & GetName()const; //const函数返回引用类型时，引用得是const的
private:
    float m_fRadius;
    string m_sName;
};

#endif
```

```c++
//Circle.cpp
#include "Circle.h"

CCircle::CCircle(float radius)
    :m_sName("CCircle"), m_fRadius(radius)
{
    //m_fRadius = radius;
    //m_sName = "CCircle";
}

CCircle::~CCircle()
{

}

float CCircle::GetArea() const
{
    return 3.14 * m_fRadius * m_fRadius;
}

const string & CCircle::GetName() const
{
    return m_sName;
}
```

```c++
//main.cpp
#include <iostream>
#include "Circle.h"
using namespace std;
int main()
{
    IShape *pShape = NULL;
    pShape = new CCircle(10.1);
    cout << pShape->GetArea() << " " << pShape->GetName() << endl;
    delete pShape;

    return 0;
}
```

## 26、STL 顺序容器

STL 代码分为三类：容器（顺序容器、关联容器、容器适配器）、迭代器和算法。

容器是可以持有其他对象或者指向其他对象的指针，是保存其他对象的对象，还包括了一系列处理其他对象的方法，可以自行扩展，自动地管理内存分配和释放。

顺序容器（如 vector list）：

是一种各元素之间有顺序关系的线性表。顺序式容器的每个元素均有固定的位置，除非用删除或插入的操作改变位置。这个位置和元素本身无关，而和操作时间和地点有关（push_back），顺序性容器不会根据元素的特点排序而是直接保存了元素操作时的逻辑顺序。

关联容器（如 map）：

关联容器是非线性的树结构，各元素之间没有严格的物理上的顺序关系，是以键值的方式来保存数据。可以把关键字和值关联起来保存。

容器适配器（如 stack queue priority_queue）：

适配器是容器的接口，本身不能直接保存元素，内部是调用顺序容器实现。发生了接口转换。

| 标准容器类     | 特点                                         |
| -------------- | -------------------------------------------- |
| 顺序性容器     						                                              ||
| vector         | 从后面快速插入、删除，直接访问任何元素       |
| deque          | 从前面或后面快速插入或删除，直接访问任何元素 |
| list           | 双链表，从任何地方快速插入或删除             |
| 关联容器       							                                              ||
| set            | 快速查找，不允许重复值                       |
| multiset       | 快速查找，允许重复值                         |
| map            | 一对多映射，基于关键字快速查找，不允许重复值 |
| multimap       | 一对多映射，基于关键字快速查找，允许重复值   |
| 容器适配器      												||
| stack          | 后进先出                                     |
| queue          | 先进先出                                     |
| priority_queue | 最高优先级元素总是第一个出列                 |

**vector**

vector 将元素保存在连续的存储空间，相当于数组，因此可以通过下标随机访问，速度快。但在容器中间位置添加和删除元素非常耗时。添加元素有时还需要分配额外的存储空间，拷贝数据到新空间，释放老空间。

在创建一个 vector 后，它会自动在内存中分配一块连续的内存空间进行数据存储，初始空间大小可以预先指定也可以由 vector 默认制定，这个大小即 capacity() 函数的返回值。当存储的数据超过分配的空间时，vector 会重新分配一块内存：

申请一块更大的内存，将原来数据拷贝到新内存中，销毁原来内存中的对象，释放原来的内存空间。

**list**

list 是一个线性链表结构，添加删除节点很快，但访问某个节点的速度很慢，不支持下标运算符。

**deque**

deque 是一种优化了的，对两端元素进行添加和删除操作的顺序容器，允许较为快速的随机访问。采用更多个连续的存储快，并在一个映射结构中保存对这些快机器顺序的跟踪。向 deque 两端添加或删除元素的开销小，不需要重新分配空间，向末端增加元素比 vector 更有效。

<center>
    <image src="./tf.png">
</center>

所有容器都是类模板，要定义某种特殊容器，要再容器类型名后加尖括号，尖括号里提供容器中存放的元素的类型。

```c++
vector<string> svec;
list<int> ilist;
deque<int> items;
```

所有容器都定义了默认构造函数，用于创建指定类型的空容器对象。默认构造函数不带参数。

**容器初始化**

```c++
C<T> c;		//创建一个名为 c 的容器，容器类型为 C，如 vector 或 list，T为容器内元素类型。适用于所有容器；
C c1(c);	//创建容器 c 的副本，c1 和 c 必须具有相同的容器类型和元素类型，适用于所有容器；
C c(b, e);	//创建容器 c，元素是迭代器 b,e 标识范围内的副本，适用于所有容器；
C c(n, t);	//创建容器 c，元素为 n 个值为 t 的值，t 的类型必须是容器 C 的元素类型或者可以转换为该类型，只适用于顺序容器；
C c(n);		//创建具有 n 个初始化元素的容器 c，元素类型为值 n 的类型，只适用于顺序容器。
```

**顺序容器的方法**

1、begin 和 end

返回容器的迭代器，通过迭代器可以访问容器内的元素。

```c++
std::vector<int>::iterator iter = c.begin();
c.begin();
c.end();
c.rbegin();
c.rend();
```

2、添加元素

```c++
c.push_back();		//在容器尾部添加值为 t 的元素，返回 void
c.push_front();		//在容器头部添加值为 t 的元素，返回 void，只适用于 list 和 deque
c.insert(p, t);		//在迭代器 p 指向的元素前面插入值为 t 的元素，返回指向 t 的迭代器
c.insert(p, n, t);	//在迭代器 p 指向的元素前面插入 n 个值为 t 的元素，返回 void
c.insert(p, b, e);	//在迭代器 p 指向的元素前面插入由迭代器 b 和 e 标识范围内的元素，返回 void
```

3、获得容器大小

```c++
c.size();		//返回容器内元素个数，返回类型为 c::size_type
c.max_size();	//返回容器内最多可容纳的元素个数，返回类型为 c::size_type
c.empty();		//测试容器内是否有元素
c.resize(n);	//调整容器大小，使其能容纳 n 个元素
c.resize(n, t);	//调整容器大小，使其能容纳 n 个元素，新添加元素以 t 初始化
```

4、访问容器元素

```c++
c.front();		//返回第一个元素的引用，如果 c 为空，该操作未定义
c.back();		//返回最后一个元素的引用，如果 c 为空，该操作未定义
c[n] at方法	   //返回小标为 n 的元素的引用，n 越界时，该操作未定义，用于 vector 和 deque
```

5、删除元素

```c++
c.erase();		//删除迭代器 p 指向的元素，返回一个指向被删除元素后面的元素的迭代器
c.erase(b, e);	//删除迭代器 b 和 e 标识范围内的元素，返回指向被删除元素段后面的元素的迭代器
c.clear();		//删除容器内的所有元素，返回 void
c.pop_back();	//删除容器的最后一个元素，返回 void
c.pop_front();	//删除容器的第一个元素，返回 void，只适用于 list 和 deque
//特别注意：删除元素可能会使迭代器失效，所以每次操作之后都应该及时更新迭代器
```

6、赋值操作

```c++
c1 = c2;		//删除 c1 所有元素，将 c2 所有元素复制给 c1，c1 和 c2 容器类型和元素类型必须相同
c1.swap(c2);	//交换 c1 和 c2 中所有元素，c1 和 c2 容器类型和元素类型必须相同
c.assign(b, e);	//重新给 c 赋值，内容为 b 和 e 标识范围内的元素，b 和 e 必须不是指向 c 中元素的迭代器
c.assign(n, t);	//将 c 中元素重新设置为 n 个值为 t 的元素
```

## 27、关联容器和容器适配器

map、set、multiset、multimap 是非线性树结构，采用高效的特殊平衡检索二叉树——红黑树。

map：提供 键值 关系的一对一的数据存储能力。键在容器中不可重复，且按一定顺序排列。按链表方式存储，继承了链表的优缺点。

set：一组元素的集合。其中所包含的元素的值是唯一的，且按一定顺序排列。内部通过链表方式组织，插入比 vector 快，查找和尾部添加比 vector 慢。（可以看做是 键值 关系存储，只是 键 没有值，map 的特殊形式）

multiset：多重集合，实现方式和 set 相似，不要求集合中元素唯一，即集合中的同一元素可以出现多次。

multimap：和 map 原理基本相似，允许 键 在容器中不唯一。

特点：

1、内部实现采用非线性二叉树结构——红黑树的结构原理实现；

2、set 和 map 保证了元素的唯一性，multiset 和 multimap 扩展了这一属性，允许元素不唯一；

3、元素是有序的集合，默认在插入时升序排列。

**map:**

可以理解为关联数组，关联的本质在于元素的值与某个特定的键组关联，而与元素位置无关。

map 类定义了 3 种类型，key_type mapped_type value_type。分别表示了键的类型、值的类型、pair 类型，pair 的第一个元素是键，第二个是值。

定义 pair 对象

```c++
pair<T1, T2> p1;	//创建一个空的 pair 对象，两个元素类型分别是 T1 和 T2，值初始化；
pair<T1, T2> p1<v1, v2>;	//创建一个 pair 对象，具有两个元素 v1 和 v2，类型分别是 T1 和 T2；
make_pair(v1, v2);			//以 v1 和 v2 作为值创建一个 pair 对象，元素类型分别是 v1 和 v2 的类型；
p1.first;			//返回键值；
p1.second;			//返回值；
p1 < p2;			//小于运算遵循字典次序；
p1 == p2;			//如果两个 pair 对象的 first 成员和 second 成员依次相等，则两个 pair 对象相等。
```

定义 map 对象：

```c++
map<k, v> m;		//创建一个空的 map 对象 m，其值和键类型分别为 k 和 v;
map<k, v> m(m2);	//创建 m2 的副本 m，m 必须具有和 m2 相同的键类型和值类型
map<k, v> m(b, e);	//创建一个 map 对象 m，存储迭代器 (b, e) 标识范围内的所有元素的副本
```

map 定义的类型：

```c++
map<k, v>::key_type;	//map 容器中，用作索引的键的类型
map<k, v>::mapped_type;	//map 容器中，键所关联的值的类型
map<k, v>::value_type;	//一个 pair 类型，first 元素是 const map<k, v>::key_type 类型，second 元素是 map<k, v>::mapped_type 类型
pair<const map<k, v>::key_type, map<k, v>::mapped_type>
```

添加元素：

```c++
m.insert(e);	//e 为 map 的 value_type 类型的值。如果 e.first 不存在，则添加一个值为 e.second 的值，如果存在，则 m 不变。该操作返回一个 pair 类型的对象，包含一个指向新添加元素的 map 迭代器，以及一个 bool 值，表示插入是否成功。
m.insert(b, e);	//将迭代器 b 和 e 标识区间内所有元素插入到 m 中，所插入元素必须为 m.value_type 类型，返回 void
m.insert(iter, e);	//如果 m 中不存在键 e.first，则在 m 中以 iter 为起点搜索新元素的位置并插入，返回一个指向新添加元素的迭代器
m[1000] = "张三";		//在 map 中查找键为 1000 的元素，如果没有，则插入一个新的键值对，键为 1000， 值为 张三
```

查询元素：

```c++
m.count(k);		//返回 m 中键 k 出现的次数，返回值是 0 或 1；
m.find(k);		//若存在键为 k 的元素，返回指向该元素的迭代器，否则，返回 m.end();
```

删除元素：

```c++
m.erase(k);		//删除 m 中键为 k 的元素，返回值为所删除元素的个数，0 或 1，类型为 size_type;
m.erase(p);		//删除 m 中迭代器 p 指向的元素，p 指向的元素必须存在，返回 void
m.erase(b, e);	//删除 m 中由迭代器 [b,e) 标识范围的元素，[b, e) 必须是有效范围，返回 void
```

**set：**

set 支持 map 的大部分操作，set 容器不支持以下操作：

没有定义 mapped_type，value_type 对应的是 key_type，即元素的类型；

与 map 一样，set 容器中的键也必须唯一，不能修改。

**multiset 和 multimap：**

元素的添加删除：

insert 操作每次都会添加一个元素；

erase 带有一个键参数的该操作将删除拥有该键的所有元素，返回删除的元素个数，带有一个或一对迭代器参数，则只删除指定的元素，返回 void。

查找元素：

```c++
m.count;
m.find();
m.lower_bound(k);	//返回一个指向键不小于 k 的元素的迭代器
m.upper_bound(k);	//返回一个指向键大于 k 的第一个元素的迭代器
m.equal_range(k);	//返回一个 pair 对象，first 成员等价于 m.lower_bound(k); second 成员等价于 m.upper_bound(k)
```

容器适配器是容器的接口，本身不能直接保存元素，它保存元素的机制是调用另一种顺序容器实现。

STL 中包含三种适配器：栈 stack、队列 queue 和 优先级 priority_queue。

默认下 stack 和 queue 基于 deque 容器实现，priority_queue 基于 vector 容器实现。

在创建一个适配器时可以指定具体的实现容器，创建适配器时在第二个参数上指定具体的顺序容器可以覆盖适配器的默认实现。

栈 stack 的特点是先进后出，可以由任一种顺序容器实现，因为这些容器类型结构都可以提供栈的操作，都提供了 push_back、pop_back 和 back 操作。

队列 queue 的特点是先进先出，适配器要求关联的容器必须提供 pop_front 操作，因此不能建立在 vector 容器上。

优先级队列 priority_queue 适配器要求提供随机访问功能，不能建立在 list 容器上。

1、容器适配器通用的操作和类型：

```c++
size_type;			 //一种类型，存储此适配器类型最大对象的长度；
value_type;			//元素类型；
container_type;		//基础容器的类型；
A a;				//创建一个新的容器适配器；
A a(c);				//创建一个新的容器适配器 a，初始化为 c 的副本；
==, !=, <, >, <=, >= //关系操作符
```

2、适配器的初始化：

```c++
stack<int> stk();
stack<int> stk(stk2);
```

3、覆盖基础容器类型：

```c++
stack<int, vector<int> > stk;	//用 vector 实现 stack，注意两个 > 之间有空格，不然会被编译器认为是 右移位运算
```

4、栈适配器操作：

```c++
s.empty();		//返回栈是否为空
s.size();		//返回栈中元素个数
s.pop();		//删除栈顶元素，返回 void
s.top();		//返回栈顶元素，不删除该元素
s.push(item);	//在栈顶压入新元素
```

5、队列和优先级操作：

```c++
q.empty();		//返回是否为空
q.size();		//返回元素个数
q.pop();		//删除队首元素，返回 void
q.front();		//返回队首元素，不删除元素，只适用于队列
q.back();		//返回队尾元素，不删除元素，只适用于队列
q.top();		//返回最高优先级元素，不删除元素，只适用于优先级队列
q.push();		//对于 queue，在队尾压入元素；对于 priority_queue，在基于优先级的适当位置插入一个元素
```

## 28、迭代器和算法

迭代器是连接容器和算法的桥梁，提供对一个容器中对象的访问方法。如同一个指针。事实上，C++ 指针也是一种迭代器，但是迭代器不仅仅是指针。

迭代器是一种检查容器内元素并遍历元素的数据类型。标准库为每一种标准容器定义了一种迭代器类型。提供了比下标操作**更通用化**的方法：所有标准库容器都定义了相应的迭代器类型，而只有少数容器（vector、deque、map）支持下标操作。对容器操作时推荐使用迭代器。

**iterator 类型**

```c++
vector<int>::iterator iter;
list<string>::iterator iter2;
```

**beging 和 end 操作**

每种容器都定义了 begin 和 end 的函数，用于返回迭代器。如果容器中有元素的话，由 begin 返回的迭代器指向第一个元素：

```c++
vector<int>::iterator iter = ivec.begin();
vector<int>::iterator iter2 = ivec.end();	//end 操作返回的迭代器指向 ivec 的末端元素的下一个，被称为超出末端迭代器
```

**自增和解引用运算**

迭代器类型定义了一些操作来获取迭代器所指向的元素，迭代器类型可以使用解引用操作符（*）来访问迭代器所指向的元素：

```c++
*iter = 0;		//注意 end 方法的返回值不能解引用
```

**迭代器支持的其他方法**

比较：== 或 != 操作符来比较两个迭代器，若指向同一个元素，则相等，否则不相等。

**使用迭代器遍历容器**

```c++
for(vector<string>::iterator iter = svec.begin(); iter != svec.end(); ++iter)
{
	std::cout << *iter << std << endl;
}
```

**const_iterator**

只能读取容器内元素，不能改变容器元素内容。

**const 的 iterator**

迭代器是 const 的，而非它指向的内容

```c++
vector<int> nums(10);
const vector<int>::iterator cit = nums.begin();	
*cit = 1;
```

**迭代器的算数操作**

除了依次移动迭代器的一个元素的增量操作外，vector 迭代器（list 不支持随机访问，所以不支持这些算数操作）也支持其他的算数操作。包括：

```c++
iter + n ;		//返回指向后面 n 个位置元素的迭代器
iter - n;
iter1 - iter2;	//返回距离，可正可负
vector<int>::iterator mid = ivec.being() + ivec.size() / 2;	//指向中间位置元素的迭代器
```

**迭代器失效**

任何改变 vector 长度的操作都会使已存在的迭代器失效。

例如，在调用 push_back 之后，就不能再信赖指向 vector 的迭代器的值了。因为他们可能失效了，这时需要重新为迭代器赋值。

```c++
for(iter = v.begin(); iter != v.end(); ++iter)
{
    if(*iter == 20)
    {
        v.push_back(30);	//改变容器长度，erase 也是一样的
        iter = v.begin();
    }
}
```

**算法**

容器中提供的方法是有限的，因此 STL 提供了算法对容器进行各种操作。这些算法是独立于容器的，可以适用于不同类型的容器和不同类型的元素。

顺序容器只提供了很少的操作，如增加删除、访问元素，获得第一个元素或结束位置之后的迭代器。

但是不支持比如查找特定元素、替换和删除一个特定值，排序等。

因此 STL 中定义了一组泛型算法。所谓泛型就是可以用于不同类型的元素和多种容器类型。实现了一些经典算法的公共接口，如排序和搜索。

大部分的算法都定义在 algorithm 头文件中，numeric 文件钟定了一组处理数值的泛型算法。

这些算法并不直接操作容器，而是通过迭代器来进行操作。所以说迭代器是算法和容器的桥梁。

通常情况下算法会遍历迭代器范围内的元素，对每个元素进行处理。

如查找 vector 中是否包含特定值，可以调用标准库算法 find。

```c++
vector<int>::iterator iter = find(vec.begin(), vec.end(), 20);
if(iter != vec.end())
{
	//do something
}
```

传递给 find 的前两个参数表示元素范围的迭代器，第三个参数是用来搜索的值。

如果不存在这个值，find 会返回第二个迭代器。[ ) 左闭右开

可以使用 find 在任何容器中查找。因为指针是一种特殊的迭代器，所以也可以在 find 上使用指针。

```c++
int array[] = {10, 20, 30, 40, 50, 60};
int *p = find(array, array + 6, 0);
if(p != array + 6)
{
    //搜索成功
}
```

容器、迭代器和算法都是通过模板类来实现的，由于 find 并不依赖于容器，仅通过迭代器访问容器中的元素，所以通用。

但是算法依赖于元素提供的一些操作，比如 find，需要依赖于元素提供的 == 操作符，完成每个元素与指定值的比较。其他算法可能需要元素类型支持 < 运算符。

**只读算法**

一些算法只读取某个范围的元素，不改变元素。find 就是这样的算法。

另一个就是 accumulate 算法，用于对迭代器范围（左闭右开）求和。第三个参数是和的初始值。

```c++
int sum = accumulate(vec.begin(), vec.end(), 0);
```

第三个参数作为初始值，元素类型必须与第三个参数类型匹配，必须支持元素类型与第三个参数类型相加。

如 string 类支持 + 运算符。可以使用 accumulate 将容器中的 string 元素连接起来：

```c++
string sum = accumulate(vec.begin(), vec.end(), string(""));//第三个参数不能写成 “”，因为 const char * 上没有定义 + 运算符
```

**修改容器元素的算法**

一些算法会修改容器重元素的值。但算法永远不会修改容器的长度。

如 fill 算法用来填充迭代器指定的范围的值。

```c++
fill(vec.begin(), vec.end(), 0);
```

将所有元素置为 0。

**重排容器元素的算法**

某些算法会改变容器中元素顺序，如 sort，会重新排序容器中元素，使用 < 运算符来实现。

sort 接收两个迭代器，表示要排序的范围。

```c++
sort(vec.begin(), vec.end());
```

**向算法传递函数**

谓词是一个可调用的表达式，返回结果是可以被用作条件的值。标准类使用谓词分为两类：一元谓词和二元谓词。

一元谓词只接受一个参数，二元谓词接受两个参数。

接收谓词参数的算法会对容器中的元素调用谓词，元素类型必须能够转换为谓词参数的类型。

```c++
bool isShorter(int a, int b)
{
    return a < b;
}
sort(vec.begin(), vec.end(), isShorter);	//降序排列 vector 中的元素
```

count_if 用来统计满足谓词的元素个数：

```c++
bool operate(int a)
{
    return a < 60;
}
int nCount = count_if(vec.begin(), vec.end(), operate);
```

**算法的一般形式**

除了参数之外，算法有自己的命名和重载规范。

一些算法使用重载形式来传递谓词，unique 用来重新整理给定的序列，将相邻重复元素删除。

```c++
unique(vec.begin(), vec.end());	//使用 == 比较元素
unique(vec.begin(), vec.end(), compare);	//使用 compare 比较元素
```

***_if版本算法**

接受一个值的算法通常有另一个不同名的版本，该版本接受一个谓词代替元素的值。

```c++
find(beg, end, val);
find_if(beg, end, 谓词);
```

## 29、STL 实例

**vector**

```c++
#include <iostream>
#include <vector>
#include <algorithm>

void display(std::vector<int> &vec)
{
    for(std::vector<int>::iterator iter = vec.begin(); iter != vec.end(); ++iter)
    {   
        std::cout << *iter << "\t";
    }   
    std::cout << std::endl;
}

bool operate(int a)
{
    return a > 60; 
}

bool isBigger(int a, int b)
{
    return a > b;
}

int main()
{
    int array[] = {10, 20, 30, 40, 50, 60, 70};
    std::vector<int> vec(array, array + 6); 
    display(vec);
    
    std::cout << count_if(vec.begin(), vec.end(), operate) << std::endl;
    
    sort(vec.begin(), vec.end(), isBigger);
    display(vec);

    for(std::vector<int>::iterator iter = vec.begin(); iter != vec.end(); ++iter)
    {   
        if(*iter < 30) 
        {   
            vec.erase(iter);
            iter = vec.begin();
        }   
    }
    
    display(vec);
    return 0;
}
```

运行结果：

```shell
10	20	30	40	50	60	
0
60	50	40	30	20	10	
60	50	40	30
```

**map**

```c++
#include <iostream>
#include <map>
#include <string>
using namespace std;

void display(map<int, string> &m) 
{
    for(map<int, string>::iterator iter = m.begin(); iter != m.end(); ++iter)
    {   
        cout << iter->first << ", " << iter->second << endl;
    }   
}

int main()
{
    map<int, string> m;
    m.insert(make_pair(1000, "zhangsan"));
    m.insert(pair<int, string>(1001, "lisi"));
    m[1002] = "zhaowu";
    display(m);

    if(m.count(1000))
    {   
        m[1000] = "zhangsansan";
    }   
    display(m);

    return 0;
}
```

运行结果：

```shell
1000, zhangsan
1001, lisi
1002, zhaowu
1000, zhangsansan
1001, lisi
1002, zhaowu
```

**stack**

```c++
#include <iostream>
#include <stack>
#include <string>
#include <list>

using namespace std;

int main()
{
    stack<int> s;
    stack<string, list<string> > s2; 
    
    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);

    s2.push("hello world!");
    s2.push("nihao shijie!");

    while(!s.empty())
    {   
        cout << s.top() << "\t";
        s.pop();
    }   
    cout << endl;

    cout << "s2 size:" << s2.size() << endl;
    while(!s2.empty())
    {   
        cout << s2.top() << "\t";
        s2.pop();
    }   
    cout << endl;

    return 0;
}
```

执行结果：

```shell
40	30	20	10	
s2 size:2
nihao shijie!	hello world!
```

## 10、派生类构造函数

```c++
派生类名 (派生类构造函数参数表) : 基类构造函数(基类构造函数参数表)
{
	函数体
}
```

1、完成对象所占内存的开辟，由系统在调用构造函数时自动完成；

2、调用积累的构造函数完成基类成员的初始化；

3、如果派生类中含有对象成员、const 成员或引用成员，则必须在初始化表中完成初始化；

4、派生类构造函数体执行。

```c++
#include <iostream>
using namespace std;

class A
{
private:
    int x;
public:
    A(int xp) 
    {   
        x = xp; 
        cout << "A 构造函数被执行" << endl;
    }   
};

class B
{
public:
    B() 
    {   
        cout << "B 的构造函数被执行" << endl;
    }   
};

class C : public A
{
private:
    int y;
    B b;
public:
    C(int xp, int yp):A(xp), b()
    {   
        y = yp; 
        cout << "C 的构造函数被执行" << endl;
    }   
};

int main()
{
    C expc(1, 2); 
    return 0;
}
```

## 12、重载、覆盖和隐藏

**重载：**

1、同一作用域内（比如同一个类）；

2、函数名相同；

3、参数不同（个数，类型）;

4、virtual 关键字可有可无。

```c++
#include <iostream>

using namespace std;

class A
{
public:
    virtual int fun();
    void fun(int);
    void fun(double, double);
};

int A::fun()
{
    cout << " 111 " << endl;
}

void A::fun(int a)
{
    cout << " 222 " << endl;
}

void A::fun(double a, double b)
{
    cout << " 333 " << endl;
}

int main()
{
    A a;
    a.fun();
    a.fun(1);
    a.fun(1.1, 2.2);
    return 0;
}
```

结果：

```shell
 111 
 222 
 333 
```

**覆盖**

1、不同范围（分别位于派生类和基类中）；

2、同名函数；

2、参数相同；

4、基类函数必须是虚函数（virtual）；

```c++
#include <iostream>

using namespace std;

class A
{
public:
    virtual void fun1(int, int);
    virtual int fun2(char *);
};

void A::fun1(int a, int b)
{
    cout << " A fun1 " << endl;
}

int A::fun2(char *a)
{
    cout << " A fun2 " << endl;
    return 0;
}

class B: public A
{
public:
    virtual void fun1(int, int);
};

void B::fun1(int a, int b)
{
    cout << " B fun1 " << endl;
}

class C: public B
{
public:
    virtual int fun2(char *); 
};

int C::fun2(char *a) 
{
    cout << " C fun2 " << endl;
    return 0;
}

int main()
{
    A *p = NULL;
    A a;
    B b;
    C c;
    p = &a;
    p->fun1(1, 2);
    p->fun2("test");
    p = &b;
    p->fun1(1, 2);
    p->fun2("test");
    p = &c;
    p->fun1(1, 2);
    p->fun2("test");
    return 0;
}
```

结果：

```shell
 A fun1 
 A fun2 
 B fun1 
 A fun2 
 B fun1 
 C fun2 
```

B 覆盖了基类 A 的 fun1 方法，C 覆盖了基类 B 的 fun2 方法。

**隐藏：**

1、不同范围（派生类和基类）；

2、同名函数；

再满足以下任一条件：

3.1、参数相同时，基类函数不是虚函数；

3.2、参数不同时，基类函数无论是否是虚函数都会被隐藏（参数不同，编译出来的函数地址就不是同一个）。

```c++
#include <iostream>
using namespace std;

class A
{
public:
    void fun(int xp);
    virtual void fun2(int, int);
};

void A::fun(int xp)
{
    cout << "A fun(int)" <<endl;
}

void A::fun2(int a, int b)
{
    cout << "A fun2(int, int)" << endl;
}

class B: public A
{
public:
    void fun(int xp);
    void fun(char *s);
    void fun2(int, char *); 
};

void B::fun(int xp) 
{
    cout << "B fun(int)" <<endl;
}

void B::fun(char *s) 
{
    cout << "B fun(char *)" << endl;
}

void B::fun2(int a, char *str)
{
    cout << "B fun2(int, char *)" << endl;
}

int main()
{
    A a; 
    B b;
    A *p = NULL;
    p = &a;
    p->fun(1);
    p->fun2(1, 2);
    p = &b; 
    p->fun(1);
    //p->fun("test");       //这句话编译不通过，p 没有参数是字符串的 fun 方法
    //p->fun2(1, "test");   //这句话编译不通过，p 没有第二个参数是字符串的 fun2 方法
 
    B *pp = &b;
    pp->fun(1);
    pp->fun("test");
    pp->fun2(1, "test");

    return 0;
}  
```

结果：

```shell
A fun(int)
A fun2(int, int)
A fun(int)
B fun(int)
B fun(char *)
B fun2(int, char *)
```

## 13、虚函数

```c++
#include <iostream>
using namespace std;

class base
{
public:
    void disp()
    {
        cout<<"Hello, base"<<endl;
    }
};

class child1: public base
{
public:
	//派生类 child1 中定义的 disp 函数将 base 类中定义的 disp 函数隐藏
	void disp()
    {   
		cout<<"Hello, child1"<<endl;
	}   
};

class child2: public base
{
public:
	//派生类 child2 中定义的 disp 函数将 base 类中定义的 disp 函数隐藏
    void disp()
    {   
    	cout<<"Hello, child2"<<endl;
    }   
};

void display(base *p) 
{
    p->disp();
}

int main(int argc, char *argv[])
{
    base *p = NULL;
    base obj_base;
    obj_base.disp();
    p = &obj_base;
    p->disp();

    child1 *p_child1 = NULL;
    child1 obj_child1;
    obj_child1.disp();
    p_child1 = &obj_child1;
    p_child1->disp();

    child2 *p_child2 = NULL;
    child2 obj_child2;
    obj_child2.disp();
    p_child2 = &obj_child2;
    p_child2->disp();

    //使用 obj_child1 地址为 p 赋值
    p = &obj_child1;
    p->disp();

    p = &obj_child2;
    p->disp();

    display(&obj_base);
    display(&obj_child1);
    display(&obj_child2);

    return 0;
}
```

执行结果：

```shell
Hello, base
Hello, base
Hello, child1
Hello, child1
Hello, child2
Hello, child2
Hello, base
Hello, base
Hello, base
Hello, base
Hello, base
```

解释：没有virtual关键字，调用的是指针类型的类的对应函数

```c++
#include <iostream>
using namespace std;

class base
{
public:
    virtual void disp()
    {
        cout << "Hello, base" << endl;
    }
};

class child1: public base
{
public:
	void disp()
    {   
		cout << "Hello, child1" << endl;
	}   
};

class child2: public base
{
public:
    void disp()
    {   
    	cout << "Hello, child2" << endl;
    }   
};

void display(base *p) 
{
    p->disp();
}

int main(int argc, char *argv[])
{
    base *p = NULL;
    base obj_base;
    obj_base.disp();
    p = &obj_base;
    p->disp();

    child1 *p_child1 = NULL;
    child1 obj_child1;
    obj_child1.disp();
    p_child1 = &obj_child1;
    p_child1->disp();

    child2 *p_child2 = NULL;
    child2 obj_child2;
    obj_child2.disp();
    p_child2 = &obj_child2;
    p_child2->disp();

    //使用 obj_child1 地址为 p 赋值
    p = &obj_child1;
    p->disp();

    p = &obj_child2;
    p->disp();

    display(&obj_base);
    display(&obj_child1);
    display(&obj_child2);

    return 0;
}
```

执行结果：

```shell
Hello, base
Hello, base
Hello, child1
Hello, child1
Hello, child2
Hello, child2
Hello, child1
Hello, child2
Hello, base
Hello, child1
Hello, child2
```

解释：有 virtual 关键字，调用的是指针指向类型的对应函数。

## 17、类模板

```c++
#include <iostream>

using namespace std;
//类模板声明和模板类实现要放在同一个文件中
template <class T, int num>
class Stack
{
private:
    T sz[num];
    int point;
public:
    Stack();
    bool isEmpty();
    bool isFull();
    bool push(const T &);
    bool pop(T &);
};

template <class T, int num>
Stack<T, num>::Stack()
{
    point = 0;
}

template <class T, int num>
bool Stack<T, num>::isEmpty()
{
    return point == 0;
}

template <class T, int num>
bool Stack<T, num>::isFull()
{
    return point == num;
}

template <class T, int num>
bool Stack<T, num>::push(const T &obt)
{
    if(isFull())
    {
		return false;
    }
    else
    {
        sz[point] = obt;
        ++point;
        return true;
    }
}

template <class T, int num>
bool Stack<T, num>::pop(T &obt)
{
    if(isEmpty())
    {
        return false;
    }
    else
    {
        --point;
        obt = sz[point];
        return true;
    }
}

int main()
{
    Stack<int, 10> st;
    cout << "st 为空？" << st.isEmpty() << endl;

    st.push(5);
    cout << "st 为空？" << st.isEmpty() << endl;

    for(int i = 0; i < 10; ++i)
    {
        st.push(i);
    }

    cout << "st 满?" << st.isFull() << endl;

    int ret;
    while(st.pop(ret))
    {
        cout << ret << "\t";
    }
    cout << endl;

    return 0;
}
```

结果：

```shell
st 为空？1
st 为空？0
st 满?1
8	7	6	5	4	3	2	1	0	5
```

