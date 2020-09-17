- `ClampMagnitude`将向量限制在某一个长度如  
    ```csharp
    Vector3.ClampMagnitude(movement, speed);
    ```  
    将movent的大小限制在speed  
- 将向量从local space to world space use `movement = TransformDirection(movement);`  
- culling mask  
    在light中选择使阴影只用于某些对象，culling意味着移除不需要的东西,culling mask 意思是从阴影投射中移除一系列对象  
- 序列化  
    [thispage](https://zhuanlan.zhihu.com/p/76247383)  
- nuget 第三方库保存的网站  
- C#保留关键字如果非要用来当标识符，需要在标识符前加@符号，例如 `class @class` 新建了一个名叫class的类  
- 上下文关键字(contextal keyword)，不是C#保留字  
- conslole.writeline 快捷键cw  
- static 关键字  
    修饰的类内成员被称为静态成员，作用于类型而不是类型实例  
    `static class` 整个类中的所有成员都是静态的，静态类不可以创建实例  
- 类型转换  
    分为隐式转换和显示转换  
    ```C#
    int a = 10;
    long b = a;
    short z = (short) b;<--显式转换，损失精度
    ```
    如果编译器认为转换肯定会失败，则两种转换都会被禁止。  
- 类型分类  
C#中的类型主要有值类型，引用类型，范型类型参数，指针类型。  
值类型包含所有的内置类型和自定义的struct和enum  
引用类型包含所有的class，数组，delegate，interface类型，包括字符串。需要为引用和对象分别单独分配内存，对象所占内存为，字段所占内存总和加额外的管理开销（最少8字节），每个对象的引用还需要额外的4个或者8个字节。  
引用类型：string，object。
两者的区别在于处理内存的方式  
- null  
null 赋给一个引用，表示这个引用不指向任何变量  
普通的值类型不可以为null