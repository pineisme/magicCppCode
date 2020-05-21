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
- 
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
