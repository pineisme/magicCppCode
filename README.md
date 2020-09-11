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

- algorithm头文件  
    找到最大值：
    ```cpp
    auto p=std::max_element(arr.begin(),arr.end());
    ```
    返回值p是迭代器

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
    在为vector初始化时最好先
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
