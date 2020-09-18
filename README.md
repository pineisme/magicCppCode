####Those are the  magic cpp codes collected by me 
- about ?: 
    ```cpp
    (i & 01 ? odd : even).push_back(thing);
    ```
    odd and even all continer

- 关于initializer_list 
    包含在头文件<initializer_list>中，在使用时需要规定传入数据的类型如:
    ```cpp
    myclass(std::initializer_list<int> list);
    ```
    此时，类的构造可以用花括号的 方法构造：
    ```cpp
    myclass a={1,2,3,4};
    ```
- A a;  
    std::cout << typeid(a).name();  // 可以在编译时确定a的类型为A  
    空对象占用一个字节，因为需要在内存中确定a的位置  
    typeid(decltype(a_rb)).name(); // decltype产生的是编译时即可确定的声明类型，因此为A
typeid(a_rb).name()；  // 由于a_rb是多态类型的glvalue，typeid在运行时计算，因此为B
- algorithm头文件  
    找到最大值：
    ```cpp
    auto p=std::max_element(arr.begin(),arr.end());
    return *p;
    auto p = std::::min_element(s.begin(),s.end());
    ```
    返回值p是迭代器,返回值需要加上*  
      
    ```cpp
    sort(s.begin(),s.end(),less<int>());
    sort(s.begin(),s.end(),greater<int>());
    ```
    注意end必须在你想呀排序的最后一个位置之后


- 快排的基本格式
    ```cpp
    while(front<rear>){
        int mid = (front+rear)>>1;
        if(k[mid]<target){
            front= mid+1;
        }
        else rear=mid;
    }
    return front;
    ```
    需要注意的是

- 容器的emplace插入  
    普通的push和insert操作都是传递元素类型对象本身，而emplace_front()和emplace_back()将参数传递给元素类型的构造函数，如：
    ```cpp
    //C用来保存myclass对象
    c.emplace_back("966",12);//传递给构造函数,且必须与构造函数相匹配
    c.push_back(myclass("966",12));
    ```
- list双向链表  
    list可以高效地在内部增加删除元素
    list有特殊的remove(p)操作，移除和参数匹配地元素
    remove_if(p),p可以是函数或则lambda表达式,也可是同类型的元素
    unique()可以移除连续重复的元素只保留一个，unique()可不接受参数，也可接收一个二元断言，true被认为是相等的。
    sort()也分为有参数和无参数。默认从小到大
- deque双端队列  
    deque只在首位插入较快
- vector  
    在为vector初始化时最好先定好大小，避免扩容时候重复拷贝。  
    使用vector初始化二维数组方法
    ```cpp
    vector<vector<int>> f(n + 1, vector<int>(26));
- lambda表达式
    ```cpp
    []() {}
    //[=]从外部捕获的变量=为值捕获,[&]表示按引用，[= ,&b]默认全部按值，b用引用，反之亦然
    //[]捕获值，（）函数参数，{}函数体
    []() mutable ->T {}
    //T is returnn type, in some situation can be ommitted
    //If a lambda is marked mutable, it is allowed to mutata the values taht have been capture by value.
    auto mid = [&] { return v.begin() + v.size() / 2; };
    for (auto curr = v.begin(); curr != mid(); ++curr)
    //注意for循环中的mid必须加圆括号，可以理解为mid其实是一个函数
    ```
    [这里关于lambda讲得很好 from stackoverflow](https://stackoverflow.com/questions/7627098/what-is-a-lambda-expression-in-c11?r=SearchResults)

- static关键字  
    在类外的static关键字表明该函数和变量只能在该翻译单元（该文件内）内被找到，不能被其他文件使用，如果其他文件需要使用，则需要加extern关键字
    在类内使用static关键字：
    static此时的变量被所有的类试题共用，他不属于任何一实体。在类内声明在类外定义，在类内定义static变量 只有枚举和float可以使用const static flaot = 1;
        
    使用 static与全局变量的优势，静态成员没有进入全局命名空间，不会产生命名冲突，可以实现信息隐藏，静态成员变量可以试试private的

    静态成员函数为类服务而不是某一个具体的类，因为不属于某一个类，所以没有this指针，所以他无法调用不是静态成员的变量，静态成员函数之间可以相互访问。

- 继承   
    public 意为着，父类中的public和private的成员到子类中依然为public and private.
    protected means at the sub-class, the public and private members become protected.
    private means at the sub-class, the public and private members become private.

- 类相关
    嵌套类可以访问外围类的私有和保护的静态成员
- 虚函数  
    [这篇博客讲的好](https://blog.csdn.net/hackbuteer1/article/details/7558868)
    编译器会根据虚表意识到有共同的基类成员

- explict  
    禁止通过等于＝符号对对象进行初始化，防止隐式类型转换

- static_cast,dynamic_cast,reinterpret_cast,const_cast  
    **static_cast**在编译期进行转换，无法安全监测  
    **dynamic_cast**在运行时对实际类型进行检测，如果是指针的话不能转换时返回nullptr值。  
    基类指针（引用）转换成派生类指针（引用）使用dynamic_cast更安全
    派生类和基类智能指针之间的转换可以用`std::dynamic_pointer_cast` and `std::static_pointer_cast`  
    `const_cast` can change const pointer or refrence to nonconst  
    when complier not allow you use `static_cast`, but you can ensure this behaviour is safe,you can use `static_cast`

- reverse()函数可以翻转容器  
    `reverse(s.begin(),s.end())`
- 指定小数输出精度  
    `cout<<setprecision(3)<<fixed<<a/b<<endl;`或者C代码`printf("%.指定的位数lf\n",要输出的数);`  
- functional  
    std:function为一个多态函数包装器
    在C语言中，使用函数指针可以让函数指针指向参数类型相同，返回值类型也相同的函数，通过函数指针实现多态  
    `typedef int (*func)();`  
    指向无参数输入，返回值为Int的函数.  
    `std::function<void()> func(&print1);`  
    `func=&print2`;  
    `std::function<int(int)> f=target`  
    store a lambda:  
    `function<void()> f = [](){do_something;};`  
    store bind result:  
    `std::function<void()> f_display_31337 = std::bind(print_num, 31337);`  
    
    当func被赋予了一个重载了()的对象时，可以向调用该函数一样使用该对象
    ```cpp
    class a{
        void operator()(){
            ...
        }
    }
    a A;
    func=A;
    func();<--can be used as a function
    ```
    实现function功能有两种方式，一种是通过类的多态即虚表来达到多态，一种是通过C语言的函数指针来实现。  
- bind()函数适配器  
    他接受一个函数，生成一个函数来改变原来函数的参数列表，比如减少原来函数的参数个数，或者顺序，以满足新的需求。
    ```cpp
    #include<functional>
    using namespace std::placeholders;<--占位符
    ```
    `bind(函数名，arg_list);`arg_list为用逗号分割的原来函数的参数列表，里面可能包含占位符`_n`代表新的函数里的参数位置。`_1` 代表这个参数在原函数中为第一个参数。
    ```cpp
    double devide(double x, double y){
        return x/y;
    }
    auto one_bind = std::bind(devide, 2, 10);<--- 0.5;
    auto two_bind = std::bind(devide, _1, 2);<--- two_bind(10)  = 5
    auto three_bind = std:bind(devide, _2, _1);<--- three(10,2) = 0.2
    auto four_bind = std:bind<int>(devide, _1, _2);<--- 指定返回类型为Int four_bind(10, 3) = 0.3
    ```
    `bind(..., bind(...), ...)`bind 可以嵌套  
- assert  
assert(表达式)；如果表达式为假则打印错误信息并且退出
- thread  
    
- ifstream  
 用`ifstream input {name};`替换`FILE* input = fopen(name, "r");`
- 静态断言  
`static_assert` 用于在编译器检查，如果表达式为真，不作任何事情，如果为否，抛出编译错误就是提示字符串。常用与模板中
`static_assert(常量表达式，提示字符串);`  
- 枚举enum  
枚举力的值必须要在编译器可知
- 模板  
模板实参不能腿短返回类型，必须显示指定  
```cpp
template <typename T, typename U, typename RT>
RT max(T a, U b){
    return a>b?a:b;
}
cout<<::max<int,double, double>(1,3.1);
---默认情况下，返回参数由第一个模板参数确定
template <typename T,typename U>
T max(T a, U b){
    return a>b?a:b;
}
cout<<::max(1,3.1);
----
template <typename RT, typename T, typename U>
RT max(T a, U b) {
  return b < a ? a : b;
}

::max<double>(1, 3.14);  // OK：返回类型为 double，返回 3.14
//---C++14 can use atuto as return type
template <typename T, typename U>
auto max(T a, U b) {
  return b < a ? a : b;
}
//if you only support C++11 you need to add ->
template <typename T, typename U>
auto max(T a, U b) -> decltype(b < a ? a : b) {
  return b < a ? a : b;
}
```
使用std::common_type获取模板参数类型都能隐式转换到的类型，在C++14中你可以这么写
```cpp
#include <type_traits>

template <typename T, typename U, typename RT = std::common_type_t<T, U>>
RT max(T a, U b) {
  return b < a ? a : b;
}
```
有时候你的模板参数必须是一个引用，但是你的返回值不能是一个引用，可以使用std::decay去掉引用修饰符等，退化到基本的类型。
```cpp
#include <type_traits>

template<typename T, typename U, typename RT = std::decay_t<decltype(true ? T() : U())>>
RT max(T a, U b) {
  return b < a ? a : b;
}
```
在模板中使用constexpr：  
```cpp
constexpr auto fact(uint64_t n){
    if(n ==1 ){
        return n;
    }
    return n*fact(n-1);
}
constexpr auto i = ::fact(10);
```
可以在编译器获得i的值，需要注意constexpr在递归很多层时可能失败。  
如果类模板有static数据成员，每种实例化类型都会实例化static数据成员。static成员函数和数据成员只被同类型共享。