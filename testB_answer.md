# C++程序设计模拟试题B答案及解析

>命题：ObjectKaz 
>审题：ObjectKaz 

## 一.判断分析题（每题2分，共20分）

> 说明：若指出该命题是错的，但没有改正错误或解释原因，或改正后的命题仍然是错的，则此题不得分。

#### 1.

**[答案]**

错误。静态局部变量具有局部作用域，具有静态生命期。

**[考点]**

作用域、生命期。

#### 2.

**[答案]**

错误。函数调用运算符是不定目运算符，其重载函数可以添加默认参数。

**[解析]**

一般的运算符目数是固定的，不允许默认参数是为了防止用户修改运算符的目数。但函数调用运算符比较特殊，它是不定目运算符，其重载函数可以添加默认参数。

**[考点]**

运算符重载的规则。

#### 3.

**[答案]**

正确。

**[解析]**

当使用派生类对象 `obj`初始化基类引用 `r` 时， `r` 并不是 `obj` 的别名，而是 `obj` 中基类部分的别名。因此，基类引用 `r` 的地址应当是 `obj` 中基类部分的地址。但基类部分的地址是否和派生类部分的地址相同，是不确定的。一般来说，只有第一个非虚基类部分的地址与派生类的地址相同。

**[考点]**

子类型。

#### 4.

**[答案]**

错误。`class` 中，成员的访问权限和继承方式默认为 `private` ；`struct`中，成员的访问权限和继承方式默认为 `public` 。

**[考点]**

`class` 和`struct` 的区别。

#### 5.

**[答案]**

错误。静态成员函数在类作用域内，可以访问非公有成员函数。

**[考点]**

静态成员函数。

#### 6.

**[答案]**

正确。

**[解析]**

编译器在执行默认拷贝赋值操作时，会将对象的成员逐一拷贝。但 `const int` 成员，定义后就不能修改。所以编译器遇到常量非静态数据成员时，编译器不会生成默认拷贝赋值操作。

**[补充]**

除了有用户定义的特殊成员函数外，以下几种情况，编译器也不会生成相应的特殊成员函数：

| **构造函数**                     | **析构函数**                     | **拷贝构造函数**                     | **拷贝赋值操作**                     |
| -------------------------------- | -------------------------------- | ------------------------------------ | ------------------------------------ |
| 非静态数据成员或基类不能正常构造 | 非静态数据成员或基类不能正常析构 | 非静态数据成员或基类不能正常拷贝构造 | 非静态数据成员或基类不能正常拷贝赋值 |
| 非静态数据成员或基类不能正常析构 |                                  | 非静态数据成员或基类不能正常析构     | 非静态数据成员或基类不能正常析构     |
|                                  |                                  |                                      | 某个非静态数据成员是引用类型         |
|                                  |                                  |                                      | 某个非静态数据成员是常量或常量数组   |

数组这个类型比较奇怪，尽管用户不能直接对数组赋值，但是数组是可以拷贝的。大多数情况下，数组名会转换成指向第一个元素的指针右值，这就导致数组名没有办法放到赋值语句的左边了。

数组的可拷贝性可以用下面的代码来测试：
```c++
struct Array{
    int a[5];
    Array(){}
};
Array a;
a.a[1] = 300;
Array b = a;
cout<<b.a[1];
```
**[考点]**

常变量。

#### 7.

**[答案]**

错误。最派生类是含有虚基类的多重继承体系中，负责对虚基类进行初始化的类。

**[考点]**

最派生类。

#### 8.

**[答案]**

错误。成员函数和友元函数可以构造类`A`的对象。

**[考点]**

成员访问限制。

#### 9.

**[答案]**

错误。`p`是指针常量。

**[解析]**

用 `typedef` 声明的别名，声明语句中的 `*` 和 `&` 是类型的一部分；而在定义表达式中，`*` 和 `&` 只是一个修饰符，不是类型的一部分。所以不可将`typedef` 声明的别名看成一个简单的字符串替换。

 `Ptr` 是一个指针类型，`const` 修饰 `Ptr` 表示指针本身是常量，所以 `p` 是指针常量。

**[考点]**

`const` 型数据小结。

#### 10.

**[答案]**

错误。强制类型转换运算符重载函数有返回值，其返回值的类型是由函数名中指定的类型名确定。

**[解析]**

强制类型转换运算符重载函数不能指定返回类型，但不代表它没有返回值，其返回值的类型是由函数名中指定的类型名来确定的。

转换构造函数调用的时候只传入一个参数，并不代表转换构造函数只能有一个形参。转换构造函数是构造函数的一种，可以接受默认参数。这意味着我们可以随意地向转换构造函数添加默认参数，只需保证最多有一个参数不是默认参数就行。

测试代码：
```c++
#include <iostream>
using namespace std;

class Complex
{
public:
    Complex(double r = 0,double i = 0)
    {
        real=r;
        imag=i;
    }
private:
    double real;
    double imag;
};

int main()
{
    Complex c = 5;
    return 0;
}

```

**[考点]**

转换构造函数。

## 二.简答题（第1题8分，第2-3题每题6分，共20分）

#### 11. 

**[答案]**

（2分)构造函数调用时机:（1）定义一个对象 （2）`new` 一个对象

区别：

（2分)（1）拷贝构造函数发生在对象的初始化时期，而拷贝赋值操作发生在对象的初始化后。

（4分，默认参数、有无成员初始化列表、是否有名、返回值各1分)（2）拷贝构造函数属于构造函数，可以有默认参数和成员初始化列表，但无名、且不能指定返回值；拷贝赋值操作属于运算符重载函数，有名，不允许默认参数，没有成员初始化列表，返回值为对象自身的引用。

**[考点]**

构造函数、拷贝构造函数、拷贝赋值操作。

#### 12. 

**[答案]**

（6分)它们的区别体现在派生类中基类成员的权限：

| **继承方式** \\ **基类成员权限** | **私有** | **保护** | **公有** |
| ------------------------------ | -------- | -------- | -------- |
| **私有**                       | 不可访问 | 不可访问 | 不可访问 |
| **保护**                       | 私有     | 保护     | 保护     |
| **公有**                       | 私有     | 保护     | 公有     |

**[考点]**

继承方式。

#### 13. 

**[答案]**

（2分)多态性：不同类的对象收到相同的消息时，得到不同的结果。

（1分)多态性的分为静态多态性和动态多态性。

（2分)静态多态性分为强制多态和重载多态，动态多态性分为类型参数多态和包含多态。

（1分)其中，静态多态性在编译期实现，动态多态性在运行期实现。

**[考点]**

多态性的概念。

## 三.读程序写结果（每题6分，共36分）

#### 14.

**[答案]**

（1）`151206`

（2）`3` 

**[考点]**

成员指针、静态成员。

#### 15. 

**[答案]**

（1）`120400`

（2）`-1-1-11` 

**[考点]**

函数重载、函数模板、字符串对象、理解复杂的指针定义和声明表达式。

#### 16. 

**[答案]**

（1）`2231`

（2）`3424`

（3）`4444` 

**[考点]**

构造函数和析构函数的调用顺序、拷贝构造函数调用时机。

#### 17.

**[答案]**

（1）`275`

（2）`386`

（3）`9494` 

**[考点]**

派生类中构造函数和析构函数。

#### 18.

 **[答案]**

（1）`acb1cb2ccc`

（2）`cvcnavan`

（3）`cvb1navan` 

**[考点]**

虚函数。

#### 19.

**[答案]**

（1）`3241`

（2）`7356`

（3）`273566`

**[考点]**

友元、运算符重载、类型转换。

## 四.设计与分析题（第20-21题每题6分，第22题12分，共24分）

#### 20.

**[参考答案]**

**声明：**

```c++
T &operator [](int index);
const T &operator [](int index) const;
```

**定义：**

```c++
template <typename T>
T &Array<T>::operator [](int index)
{
    return this->start_[index];
}

template <typename T>
const T &Array<T>::operator [](int index) const
{
    return this->start_[index];
}

```

**[评分标准]**

根据考生提供的代码能否满足题目要求进行评分。

（1）下标运算符重载函数没有返回引用，扣1分。

（2）普通对象不能通过下标运算符修改元素的值，或下标运算符重载函数不支持常对象，扣**1**分。

（3）使用了不允许使用的类，扣3分。

（4）有明显的语法错误的，错一处扣1分。相同的语法错误不重复扣分。

（5）没有补全声明，扣2分。

（6）如果在下标访问运算符中进行了指针有效性的判断，加2分。（可以利用异常处理）

**[考点]**

运算符重载。

#### 21. 

**[参考答案]**

```c++
class Shape {
public:
    virtual double get_area() = 0;

};

class Circle :public Shape  {
private:
    double radius_;

public:
    Circle(double radius) : radius_(radius) {}
    
    double get_area()
    {
        return kPi * radius_ * radius_;
    }
};

class Square :public Shape  {
private:
    double a_;

public:
    Square(double a) : a_(a) {}
    
    double get_area()
    {
        return a_ * a_;
    }
};

```

**[评分标准]**

根据考生提供的代码能否满足题目要求进行评分。

（1）若缺少`get_area` 函数，每缺一个扣2分。

（2）若`get_area`不是虚函数，扣2分。

（2）若派生类缺少构造函数，每缺一个扣1分。

（3）`Shape`不是抽象基类，扣2分。

（4）有明显的语法错误的，错一处扣1分。相同的语法错误不重复扣分。

**[考点]**

纯虚函数。

#### 22. 

**[参考答案1]**

```c++
template <typename T>
class AutoPtr {
private:
    T *ptr_;
    //该对象是否有删除空间的权限
    mutable bool priority_;

public:
    AutoPtr(T *ptr = NULL) : ptr_(ptr),priority_(ptr != NULL) {}

    AutoPtr(const AutoPtr &old) : ptr_(old.ptr_),priority_(old.priority_) 
    {
        //关闭原对象的删除权限
        old.priority_ = false;
    }

    AutoPtr &operator=(const AutoPtr &old) 
    {
        //直接替换
        this->ptr_ = old.ptr_;
        this->priority_ = old.priority_;
        //关闭原对象的删除权限
        old.priority_ = false;
    }

    ~AutoPtr()
    {
        //有权限才能删除
        if(this->priority_)
            delete this->ptr_;
    }

    //对于变量的解引用
    T &operator *() const
    {
        return *this->ptr_;
    }

    //对于变量的成员指针访问
    T *operator ->() const
    {
        return this->ptr_;
    }

};
```

**[参考答案2]**

```c++
template <typename T>
class AutoPtr {
private:
    T *ptr_;
    //计数器
    int *counter_;

public:
    AutoPtr(T *ptr = NULL) : ptr_(ptr),counter_(NULL) 
    {
        if(ptr != NULL)
        {
			this->counter_ = new int(1);
        }
    }

	AutoPtr(const AutoPtr& old) : ptr_(old.ptr_),counter_(old.counter_) 
    {
		//old.ptr_不为空，则counter_ 也不为空
        if(old.ptr_ != NULL)
			(*this->counter_)++;
    }

	AutoPtr &operator=(const AutoPtr& old)
	{
		//拷贝赋值时，先需要解除原有绑定
		this->release();

		//覆盖
		this->counter_ = old.counter_;
		this->ptr_ = old.ptr_;
        if(old.ptr_ != NULL)
			(*this->counter_)++;
		return *this;
	}

	//析构
	~AutoPtr()
    { 
		this->release();
    }

	//解除关联
	void release()
	{
		(*this->counter_)--;
        //删除计数器和动态指针
        if(*this->counter_ == 0)
        {
            delete this->counter_;
            delete this->ptr_;
        }  
		this->counter_ = NULL;
		this->ptr_ = NULL;
	}

    T &operator *() const
    {
        return *this->ptr_;
    }

    T *operator ->() const
    {
        return this->ptr_;
    }

};
```

**[解析]**

首先，我们应当弄清题目让我们设计什么样的类：
+	我们需要定义一个 `AutoPtr` 的**模板类**。

+	没有明文规定有哪些数据成员，但初步确定内部有个指针 `ptr_` ，类型为 `T *`。

+	初步确定有构造函数、析构函数、解引用运算符重载函数、指针成员访问运算符重载函数。其中两个重载函数要支持常对象。

再来考虑“对象析构时内部指针不会被重复删除”。这个问题我们首先可以想到通过某个数据成员的值来判断该不该删除。最简单的一种就是 `bool` 值了，只要某个数据成员的值为假，咱就不删除它。这意味着我们需要添加一个数据成员 `priority_` 。

然后就是什么时候该设置 `priority_` 为假了。如果对象构造的时候传入了空指针，那 `priority_` 肯定是假了。再考虑下拷贝的情况。为了保证不会重复删除，我们只能让其中一个对象来完成动态内存的删除。那么该关掉哪个对象的权限呢？理论上都可以。上面的**参考答案1**的代码采用的是关掉原对象的权限的方法。为了保证可以关闭常对象的删除权限，这里置 `priority_` 需要加上 `mutable` 修饰符。

接下来考虑“不需要考虑用户直接用同一指针构造或赋值多个 `AutoPtr` 对象导致的重复删除问题” 。从之前的分析可以发现，如果用户直接用同一指针构造或赋值多个 `AutoPtr` 对象，那么同一个指针被传入了多个对象。这也会带来麻烦的问题，由于这些操作绕过了对象之间的通信，所以出现的重复删除的问题是没有办法避免的。

实际上，C++标准库中的 `auto_ptr` 类大概就是这样实现的。

但是这种实现办法存在问题，在拷贝操作中，若后对象比原对象先析构，那么剩余的对象的内部指针就指向了已经释放的空间。（题目并没要求）正因为这个问题，`auto_ptr` 类在C++17标准中被砍掉了。

为了避免这个问题，我们可以改用计数器 `counter` 来判断是否删除动态对象。这个 `counter` 需要是动态内存，因为它会被所有指向同一片内存区域的 `AutoPtr` 共享。为什么不将 `counter`设置为静态成员呢？因为同一个模板实例产生的对象，内部指针也不一定是相同的。每拷贝一个 `AutoPtr` ，`counter` 就加`1`。当 `AutoPtr` 析构的时候，`counter` 就减 `1`。直到 `counter`为`0`的时候，才析构动态空间和计数器。这样，就可以确保在最后一个 `AutoPtr` 析构的时候，才会删除动态内存。上面的 **参考答案2**的代码采用的是这种方法。

C++11标准定义了新的智能指针 `unique_ptr` 、 `shared_ptr` 和 `weak_ptr` ，来帮助程序员管理动态内存。而 **参考答案2** 可以算是 `shared_ptr` 类的浅层实现原理。

**[评分标准]**

根据考生提供的代码能否满足题目要求进行评分。

（1）没有声明成模板类，扣2分。

（2）在类内部拷贝对象接管的动态内存空间，扣2分。

（3）至少需要构造函数、析构函数、解引用运算符重载函数和指针成员访问运算符重载函数。每缺一个函数，扣2.5分。

（4）有明显的语法错误的，错一处扣1分。相同的语法错误不重复扣分。如果将指针成员访问运算符重载为友元或普通函数，扣2分。

（5）若定义了解引用运算符重载函数和指针成员访问运算符重载函数，但常对象不能解引用或进行指针成员访问的，扣2分。

（6）如果在解引用或指针成员访问运算符中进行了指针有效性的判断，加2分。（可以利用异常处理）

（7）考虑了作用域的问题，加2分。

（8）使用了不允许使用的类，扣6分。

**[考点]**

综合能力。