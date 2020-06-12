# C++程序设计模拟试题

>命题：ObjectKaz 
>审题：ObjectKaz 

## 一.判断分析题（每题2分，共20分）
>正确的项打 `√` ；错误的项打 `×` ，并改正错误或解释原因。

1.	具有局部生命期的变量一定具有局部作用域，具有局部作用域的变量一定具有局部生命期。
2.	算术运算符都可以重载为友元或普通函数，所有运算符重载函数都不能有默认参数。
3.	用公有派生类对象 `obj` 的地址初始化基类的引用 `r` ，则 `&r` 和 `&obj` 在数值上可能不同。
4.	`class` 和 `struct` 中，成员的访问权限和继承方式默认为 `private` 。
5.	静态成员函数没有 `this` 指针，不能访问对象中的非公有成员。
6.	若类有 `const int` 类型的非静态成员，且没有用户定义的拷贝赋值操作，则编译器不会生成隐式的拷贝赋值操作。
7.	最派生类是有虚基类的多重继承关系中，最底层的派生类。如 `B` 和 `C` 虚拟继承 `A` ， `D` 继承 `B` 和 `C` ，则 `D` 就是最派生类。
8.	当类A的构造函数声明为 `private` 时，任何函数都无法创建类 `A` 的对象。
9. 	若有 `typedef int *Ptr;` 声明和 `const Ptr p;` 定义，则 `p` 是常量指针。
10.	转换构造函数可以有多个形参，但最多有一个形参没有默认参数。
## 二.简答题（第11-12题每题6分，第13题8分，共20分）
>根据题目要求回答问题。

11.	构造函数什么时候会被调用? 拷贝构造函数和拷贝赋值操作的区别是什么？
12.	简述三种继承方式的区别。
13.	什么是多态性？它有哪些类型？分别在什么时候实现？ 
## 三.读程序写结果（每题6分，共36分）
>阅读程序，写出程序的运行结果。

14.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_。
```c++
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

class Box
{
private:
    int length_;
    int width_;
    int height_;

public:
    static int total;

    Box(int length, int width, int height) : length_(length), width_(width), height_(height) 
    {
        total++;
    }
    
    Box(const Box &old) : length_(old.length_), width_(old.width_), height_(old.height_) 
    {
        total++;
    }
    
    ~Box()
    {
        total--;
    }
    
    int get_volume() const
    {
        return this->length_ * this->width_ * this->height_;
    }
    
    Box &set_width(int width)
    {
        this->width_ = width;
        return *this;
    }
    
    Box &set_length(int length)
    {
        this->height_ = length;
        return *this;
    }
    
    Box &set_height(int height)
    {
        this->height_ = height;
        return *this;
    }

};

int Box::total = 0;

int main()
{
    Box b1(1,2,3),b2(4,5,6),b3(b1);
    int (Box::*pmf)() const = Box::get_volume;

    b1.set_width(3).set_height(4).set_length(5);
    cout << (b1.*pmf)() << (b2.*pmf)() << (b3.*pmf)() << endl;
    cout << Box::total << endl;
    return 0;
}
```
15.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_。               
```c++
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

template <typename T>
int compare(const T& t1,const T& t2)
{
    if(t1 > t2) 
        return 1;
    if(t1 < t2) 
        return -1;
    else 
        return 0;
}

int compare(const char * const &t1,const char * const &t2)
{
    return strcmp(t1,t2);
}

int main()
{
    int ai[3][3] = {{1,2},{3,6},{4}};
    int *ap[3] = {&ai[0][0],&ai[0][1],&ai[0][2]};
    int (*pa)[3] = ai + 1;
    cout << *ap[0] << *ap[1] << *ap[2] 
         << pa[1][0] << pa[1][1] << pa[1][2] << endl;
    const char *c1 = "Hello";
    const char *c2 = "World";
    string s1(c1),s2(c2);
    cout << compare(30,60) << compare<double>(40,50.8)
         << compare(c1,c2) << compare(s2,s1);

    return 0;
}
```
16.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_，第三行是\_\_\_\_\_\_\_\_\_\_。
```c++
#include <iostream>
using namespace std;

class Box {
private:
    int length_;
    int width_;
    int height_;

public:
    Box() :length_(0),width_(0),height_(0) 
    {
        cout<<"1";
    }

    Box(int length,int width,int height) 
    :length_(length),width_(width),height_(height) 
    {
        cout<<"2";
    }
    
    Box(const Box &old) 
    :length_(old.length_),width_(old.width_),height_(old.height_) 
    {
        cout<<"3";
    }
    
    ~Box()
    {
        cout<<"4";
    }
};

void pass_a_box(Box b) {}

Box return_a_box()
{
    return Box(5,6,7);
}

int main()
{
    Box a(1,2,4),b(3,4,5),c(a),d;
    cout << endl;
    pass_a_box(c);
    return_a_box();
    cout << endl;
    return 0;
}
```
17.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_，第三行是\_\_\_\_\_\_\_\_\_\_。                  
```c++
#include <iostream>
using namespace std;

class Box {
protected:
    int length_;
    int width_;
    int height_;

public:

    Box() :length_(0),width_(0),height_(0) 
    {
        cout<<"1";
    }
    
    Box(int length,int width,int height) 
    :length_(length),width_(width),height_(height) 
    {
        cout<<"2";
    }
    
    Box(const Box &old) 
    :length_(old.length_),width_(old.width_),height_(old.height_) 
    {
        cout<<"3";
    }
    
    ~Box()
    {
        cout<<"4";
    }
    
    int get_volume()
    {
        cout<<"5";
        return this->length_ * this->width_ * this->height_;
    }
    
    int get_volume() const
    {
        cout<<"6";
        return this->length_ * this->width_ * this->height_;
    }
};

class HardBox:public Box {
protected:
    double hardness;

public:

    HardBox(int length,int width,int height,double hardness):
        Box(length,width,height),hardness(hardness)
    {
        cout<<"7";
    }
    
    HardBox(const HardBox &old):
        Box(old),hardness(old.hardness)
    {
        cout<<"8";
    }
    
    ~HardBox()
    {
        cout<<"9";
    }
};

int main()
{
    HardBox hb(5,6,7,1.1);
    hb.get_volume();
    cout << endl;
    const HardBox hb1(hb);
    hb1.get_volume();
    cout << endl;
    return 0;
}
```
18.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_，第三行是\_\_\_\_\_\_\_\_\_\_。
```c++
#include <iostream>
using namespace std;

struct A
{
    int a_;
    A(int a) : a_(a)
    {
        cout << "ac";
    }
    virtual void voutput()
    {
        cout << "av";
    }
    void noutput()
    {
        cout << "an";
    }
};

struct B1 : public A
{
    int b1_;
    B1(int a, int b1) : A(a), b1_(b1)
    {
        cout << "b1c";
    }
    void voutput()
    {
        cout << "b1v";
    }
    void noutput()
    {
        cout << "b1n";
    }
};

struct B2 : public A
{
    int b2_;
    B2(int a, int b2) : A(a), b2_(b2)
    {
        cout << "b2c";
    }
    void voutput()
    {
        cout << "b2v";
    }
    void noutput()
    {
        cout << "b2n";
    }
};

struct C : public B1, public B2
{
    int c_;
    C(int a, int b1, int b2, int c) : A(a), B1(a, b1), B2(a, b2), c_(c)
    {
        cout << "cc";
    }
    void voutput()
    {
        cout << "cv";
    }
    void noutput()
    {
        cout << "cn";
    }
};

int main()
{
    C c1(1, 2, 3, 4);
    cout << endl;
    c1.voutput();
    c1.noutput();
    c1.A::voutput();
    c1.A::noutput();
    cout << endl;
    B1 &r = c1;
    r.voutput();
    r.noutput();
    r.A::voutput();
    r.A::noutput();
    return 0;
}
```
19. 以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_，第三行是\_\_\_\_\_\_\_\_\_\_。
```c++
#include <iostream>
using std::cout;
using std::endl;

class Complex
{
private:
    double real_;
    double imaginary_;

public:
    Complex():real_(0), imaginary_(0)
    {
        cout<<"1";
    }
    Complex(double real) : real_(real), imaginary_(0)
    {
        cout<<"2";
    }
    Complex(double real, double imaginary) : real_(real), imaginary_(imaginary)
    {
        cout<<"3";
    }
    Complex(const Complex &old) :real_(old.real_),imaginary_(old.imaginary_) 
    {
        cout<<"4";
    }
    Complex &operator =(const Complex &old)
    {
        cout<<"5";
        this->real_ = old.real_;
        this->imaginary_ = old.imaginary_;
        return *this;
    }
    ~Complex()
    {
        cout<<"6";
    }
    friend Complex operator +(const Complex &c1,const Complex &c2);
};

Complex operator +(const Complex &c1,const Complex &c2)
{
    cout<<"7";
    return Complex(c1.real_ + c2.real_,c1.imaginary_ + c2.imaginary_);
}

int main()
{
    Complex c1(1,5),c2(5),c3(c2),c4;
    cout<<endl;
    c3 = c1 + c2;
    cout<<endl;
    c4 = 6 + c2;
    cout<<endl;
    return 0;
}
```
## 四.设计与分析题（第20-21题每题6分，第22题12分，共24分）
>根据要求，编写程序。

20.	下面是一个数组类的声明，请在声明空缺处补充下标运算符重载的声明，并实现下标运算符重载函数。

	（1）下标运算符重载函数既支持普通对象，也支持常对象，需要返回左值。可以定义多个下标运算符重载函数。

	（2）可不考虑数组越界的情况。

	（3）对于普通对象，要求可以通过下标来修改数组元素的值。

	（4）下标运算符重载函数的定义在类体外。

	（5）已引入头文件 `iostream` ，并且已使用命名空间 `std` 。不需要写 `main` 函数。

	（6）只能使用数组，不允许使用C++标准库中的容器。

```c++
template <typename T>
class Array{
private:
    T* start_;
    int length_;
public:
    /*构造函数*/
    Array();
    Array(int length);
    Array(const Array& old);
    /*赋值函数*/
    Array& operator=(const Array& old);
    /*析构函数*/
    ~Array();
    /*获取数组大小*/
    int length() const;
    /*清空数组*/
    void clean();
    /*数组访问*/
___________________________
};
```
21.	尝试实现抽象基类 `Shape` ，和由它派生出的 `Circle` (圆形)和 `Square` (正方形)。

	（1）每个类有一个 `get_area` 虚函数，来计算面积。派生类还需要定义构造函数，来传入数据。

	（2）已定义 `double` 型常量 `kPi = 3.14159` 。

	（3）已引入头文件 `iostream` ，并且已使用命名空间 `std` 。不需要写 `main` 函数。

22.	C++提供了 `new` 和 `delete` 运算符用于动态内存分配，但有时我们会忘记释放内存，在这种情况下就会产生内存泄漏；有时在尚有指针引用内存的情况下我们就释放了它，在这种情况下就会产生引用非法内存的指针。正确地控制动态内存的生命期，实际上是一件很困难的事情。
	为了解决动态内存分配带来的问题，请你设计一个智能指针类 `AutoPtr` ，来帮助程序员控制单个动态空间的生命期。

	（1）需要使用模板来声明类。

	（2）构造函数需要有一个指针形参（用于接收 `new` 表达式返回的指针。由于不同类构造函数的参数个数和类型都不确定，不能在内部使用 `new` ），当用户未传入参数时，应当把形参设置为 `NULL` 。其中动态分配的内存是单个空间，不是连续空间，且不需要考虑用户传入的指针是否在堆区。 

	（3）`AutoPtr` 类需要重载解引用运算符 `*` 和指针成员访问运算符 `->` ，以保证该类具有指针的基本功能。这些函数应当考虑常对象的情况，但可不考虑内部指针是否有效。重载函数可以定义多个。

	（4）你应当确定一个条件，保证 `AutoPtr` 对象在相互初始化或赋值后，对象析构时内部指针不会被重复删除。不需要考虑用户直接用同一指针构造或赋值多个 `AutoPtr` 对象导致的重复删除问题。不允许拷贝 `AutoPtr` 对象接管的动态内存空间（考虑到效率和有些对象无法拷贝的问题），但是对象内部可以创建动态空间用于存储其他数据。

	（5）已引入头文件 `iostream` ，并且已使用命名空间 `std` 。不需要写 `main` 函数。

>**附** 指针成员访问运算符重载为成员函数的原型为 `T *operator ->()` ，返回值为可以进行指针成员访问的指针。 
