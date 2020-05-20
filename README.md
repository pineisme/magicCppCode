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
