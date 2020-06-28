# C++程序设计模拟试题A答案及解析

>命题：ObjectKaz 
>审题：ObjectKaz 

## 一.判断分析题（每题2分，共20分）

> 说明：若指出该命题是错的，但没有改正错误或解释原因，或改正后的命题仍然是错的，则此题不得分。

#### 1.

**[答案]**

正确。

#### 2.

**[答案]**

正确。

#### 3.

**[答案]**

错误。只要类有纯虚函数，那么该类就是抽象类。

#### 4.

**[答案]**

错误。可以手动传入对象来访问对象的非静态成员。

#### 5.

**[答案]**

正确。

#### 6.

**[答案]**

正确。

#### 7.

**[答案]**

正确。

**[解析]**

`<<` 和 `>>` 作为流插入/提取运算符时，只能重载为友元或普通函数。

`<<` 和 `>>` 作为位运算符时，可以重载为成员、友元或普通函数。

#### 8.

**[答案]**

错误。函数有默认参数时，传入的参数个数和函数定义时参数个数可以不相同。

#### 9.

**[答案]**

错误。类型转换函数不是特殊的成员函数。

**[解析]**

构造函数、析构函数、拷贝构造函数、拷贝赋值操作称为特殊的成员函数。

#### 10.

**[答案]**

错误。构造函数调用顺序为： `C` 类构造函数 -> `A` 类构造函数 -> `D` 类构造函数 -> `B `类构造函数。

**[解析]**

对象构造的顺序：由小到大

基类部分的构造 --> 非静态数据成员的构造 --> 整个对象的构造。

## 二.简答题（共20分）

#### 11. （6分）

**[参考答案]**

（2分）（1）重载是同一作用域下，多个函数共用一个名字，且可以通过参数和返回值来区分。
（2分）（2）同名覆盖是不同作用域下，内层作用域的名字覆盖外层作用域相同的名字。
（2分）（3）重载仅限于函数和运算符，同名覆盖支持所有标识符。

#### 12. （8分）

**[参考答案]**

（2分）调用时机的区别：拷贝构造函数发生在对象的初始化时期，而拷贝赋值操作发生在对象的初始化后。

（6分，答出三个方面即可）函数本身的区别：拷贝构造函数属于构造函数，可以有默认参数和成员初始化列表，但无名、且不能指定返回值；拷贝赋值操作属于运算符重载函数，有名，不允许默认参数，没有成员初始化列表，返回值为对象自身的引用。

#### 13. （6分）

**[参考答案]**

（2分)由 `const` 修饰符修饰的成员函数叫常成员函数。

（2分)常成员函数中的 `this` 指针是常量指针。（常量指针常量也行）

（2分)常成员函数既可以被 `const` 对象调用，也可以被非 `const` 对象调用。

## 三.读程序写结果（每题6分，共36分）
#### 14. 

**[答案]**

（1）`60`

（2）`120`

（3）`6`

#### 15. 

**[答案]**

（1）`233`

（2）`8848`

（3）`666`

#### 16. 

**[答案]**

（1）`2231`

（2）`3424`

（3）`4444`

#### 17. 

**[答案]**

（1）`601206`

（2）`3`

#### 18. 

**[答案]**

（1）`acbcbvbn`

（2）`bvan`

#### 19.

**[答案]**

（1）`3241`

（2）`7356`

（3）`273566`

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

（3）使用了不允许使用的类，该题得 `0` 分。

（4）有明显的语法错误的，错一处扣1分。相同的语法错误不重复扣分。

（5）没有补全声明，扣2分。

（6）如果在下标访问运算符中进行了指针有效性的判断，加2分。（可以利用异常处理）

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

#### 22. 

**[参考答案]**

```c++
template <typename T>
class Iterator {
private:
	T *ptr_;
public:
	Iterator(T *ptr) : ptr_(ptr) {}

	//前置递增运算符
	Iterator &operator ++()
	{
		this->ptr_++;
		return *this;
	}

	//前置递减运算符
	Iterator &operator --()
	{
		this->ptr_--;
		return *this;
	}

	//后置递增运算符
	Iterator operator ++(int)
	{
		T *old = this->ptr_;
		this->ptr_++;
		return Iterator(old);
	}

	//后置递增运算符
	Iterator operator --(int)
	{
		T *old = this->ptr_;
		this->ptr_--;
		return Iterator(old);
	}

	//解引用运算符
	T &operator *()
	{
		return *this->ptr_;
	}

	//指针成员访问运算符
	T *operator ->()
	{
		return this->ptr_;
	}

	//解引用运算符（可选）
	const T &operator *() const
	{
		return *this->ptr_;
	}

	//指针成员访问运算符（可选）
	const T *operator ->() const
	{
		return this->ptr_;
	}

    //比较函数
	int compare(const Iterator &another) const
	{
		return this->ptr_ - another.ptr_;
	}

	bool operator<(const Iterator &another) const
	{
		return this->compare(another) < 0;
	}

	bool operator>(const Iterator &another) const
	{
		return this->compare(another) > 0;
	}
};

```

**[评分标准]**

根据考生提供的代码能否满足题目要求进行评分。

（1）至少有 `8` 个运算符重载函数和一个构造函数，每缺一个扣 `2` 分。

（2）缺少构造函数，扣 `2` 分。

（3）有明显的语法错误的，错一处扣 `1` 分。相同的语法错误不重复扣分。

（4）使用了不允许使用的类，则该题得 `0` 分。