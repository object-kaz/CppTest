# C++程序设计模拟试题A

>命题：ObjectKaz 
>审题：ObjectKaz 

## 一.判断分析题（每题2分，共20分）
>正确的项打 `√` ；错误的项打 `×` ，并改正错误或解释原因。


1.	各个函数通过参数、返回值和全局变量来进行数据联系。
2.	内联函数通过代码的直接展开，避免函数调用时的控制转移，提高了程序运行效率。
3.	若一个类既有纯虚函数，又有普通成员函数，则该类不是抽象类。
4.	静态数据成员必须在类体外初始化；静态成员函数没有 `this` 指针，一定不能访问对象中的非静态成员。
5.	`C++` 为了保留 `C` 的特性，对于 `struct` 声明的类，成员访问权限默认为公有。
6.	若 `B` 和 `C` 虚拟继承 `A` ， `D` 继承 `B` 和 `C` ，则初始化 `D` 类对象时，`A` 类的成员只会初始化一次。
7. 	拷贝赋值运算符只能重载为成员函数；`<<` 和 `>>` 既可以重载为成员函数，也可以重载为友元或普通函数。
8.	函数调用时，传入的参数个数必须与函数定义时参数的个数严格相等 。
9.	转换构造函数和类型转换函数属于特殊的成员函数。
10.	若派生类 `B` 公有继承自 `A`，且 `A` 有`C`类的子对象 `c` ，`B` 类有 `D` 类子对象 `d`。则创建 `B` 类对象时，构造函数调用顺序： `B` 类构造函数 -> `D` 类构造函数 -> `A` 类构造函数 -> `C `类构造函数。
## 二.简答题（共20分）
>根据题目要求回答问题。

11.	（6分）重载和同名覆盖的区别是什么？
12.	（8分）拷贝构造函数和拷贝赋值操作有哪些区别？
13.	（6分）什么是常成员函数？ 常成员函数中的 `this` 指针是什么类型？常成员函数可以被谁调用？
## 三.读程序写结果（每题6分，共36分）
>阅读程序，写出程序的运行结果。

14.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_，第三行是\_\_\_\_\_\_\_\_\_\_。
```c++
#include <iostream>
using namespace std;

class Box
{
private:
    int length_;
    int width_;
    int height_;

public:
	Box(int length,int width,int height) :
	  length_(length),width_(width),height_(height) {}
    
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

int main()
{
    Box b1(1,2,3),b2(4,5,6),b3(b1);
    b1.set_width(3).set_height(4).set_length(5);
	cout<< b1.get_volume() << endl 
		<< b2.get_volume() << endl 
		<< b3.get_volume() << endl;
    return 0;
}
```
15.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_，第三行是\_\_\_\_\_\_\_\_\_\_。               
```c++
#include <iostream>
using namespace std;

template <typename T>
int compare(const T& t1,const T& t2)
{
    if(t1 > t2) 
        return 1;
    else if(t1 < t2) 
        return -1;
    else 
        return 0;
}

template <typename T>
void exchange(T& t1,T& t2)
{
	T temp;
	temp = t1;
	t1 = t2;
	t2 = temp;
}

int main()
{
	int a = 233,b = 666,c = 8848;
	if(compare(a,b) >= 0)
		exchange(a,c);
	else
		exchange(b,c);
	cout << a << endl
		 << b << endl
		 << c << endl;
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
17.	以下程序的运行结果的第一行是\_\_\_\_\_\_\_\_\_\_，第二行是\_\_\_\_\_\_\_\_\_\_。                  
```c++
#include <iostream>
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

struct B : public A
{
    int b_;
    B(int a, int b) : A(a), b_(b)
    {
        cout << "bc";
    }
    void voutput()
    {
        cout << "bv";
    }
    void noutput()
    {
        cout << "bn";
    }
};


int main()
{
    B b(1, 2);
	b.voutput();
	b.noutput();
	cout << endl;
	A &r = b;
	r.voutput();
	r.noutput();
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

	（5）已引入所有标准库头文件，并且已使用命名空间 `std` 。不需要写 `main` 函数。

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

	（3）已引入所有标准库头文件 ，并且已使用命名空间 `std` 。不需要写 `main` 函数。

22.	迭代器是一种可以遍历容器内对象的类，提供了顺序访问容器内对象的一种接口。按照访问顺序分类，迭代器包括正向迭代器和反向迭代器。一般情况下，头迭代器指向容器的第一个元素，尾迭代器指向容器最后一个元素的下一个元素。

	请你设计一个正向迭代器 `Iterator`，用于顺序访问数组中的元素。
	
	（1）使用模板声明 `Iterator`类。
	
	（2）对象构造时，需要传入数组某一个元素的地址。
	
	（3）至少重载 `++`，`--`，`<`，`>`，`*`，`->` 六个运算符，以保证迭代器具有指针的一些功能。其中 `++`，`--`的前后置版本都需要重载。`++` 表示迭代器指向下一个元素，`--` 表示迭代器指向前一个元素，`<` 和 `>` 用于对迭代器指向元素的位置进行比较，`*` 和 `->` 用于访问迭代器指向的元素。
	
	（4）不需要考虑迭代器的内部指针是否有效。
	
	（5）已引入所有标准库头文件 ，并且已使用命名空间 `std` 。不需要写 `main` 函数。
	
	（6）不能使用标准库内置的迭代器。

>**附** 指针成员访问运算符重载为成员函数的原型为 `T *operator ->()` ，返回值为可以进行指针成员访问的指针。 
