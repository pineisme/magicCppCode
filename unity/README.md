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
- SmoothDamp()  
平滑阻尼  
- AddForce  
添加一个脉冲力，而不是一个持久的力
- 判断是否碰撞
    ```C#
    Collider2D hit = Physics2D.OverlapArea(corner1, corner2);
    platform = hit.GetComponent<MovingPlatform>();
    ```
- Mathf.Approximately(deltaX, 0)  
给定两个浮点数，判断他们是否相似，是返回true
- 四元数quaternion    
使用`Quaternion.euler`方法将旋转角度转换为四元数  
`transform.rotation = Quaternion.LookRotation(movement)`将vector3转化为Quaternion，赋值给旋转，这样就能朝向移动的方向旋转
- 插值lerp 
```C#
Quaternion direction = Quaternion.LookRotation(movement);
			transform.rotation = Quaternion.Lerp(transform.rotation,direction, rotSpeed * Time.deltaTime);
```
- _animator.SetFloat
- lookat  
`transform.lookat(target);`  
- `movement = target.TransformDirection(movement)`将本21地坐标转换为世界坐标;
- Quaternion  
`Quaternion.Euler()`方法将旋转转化为4元数，四元数乘以offset向量得到基于旋转的偏移位置。  
`Quaternion.LookRotation(movment);`将旋转的vector3转换为Quaternion，然后可以再将返回值赋值给transform.rotation  
- CharacterController组件  
`_charController=GetComponent<CharacterController>();`获得组件对象。  
move(movement)方法进行移动。  
`_charController.isGround`可以检查控制器是否在地面上。如果碰撞器的最后一帧与任何东西碰撞，这个值就为true。其实角色在地面上时应该施加一个一个轻微的向下的加速度，使角色被按在地面上。  
`_charController.hight+_charController.radius`
- 光线投射  
    ```C#
    private COntrollerColliderHit _contact;//在函数间储存碰撞数据
    void OnControllerColliderHit(COntrollrColliderHit hit){
        _contact = hit
    ;}//如果控制器在移动中击中碰撞器则调用该回调函数，使得碰撞信息可以再Update中使用
    RaycastHit hit;//保存碰撞数据
    Physice.Raycast(transform.position,Vector3.down,out hit);
    hit.distance;
    _contact.normal;//法向量笔试物体的朝向
    Vector3.Dot(movement,_contact.normal)<0;//如果小于0则说明与移动方向不再一个方向

    - 将movement乘以deltaTime使移动独立于帧数  
    `movement *= Time.deltaTime;`
    - GetCompent()  
    会返回给定对象上依附的组件，如果进行搜索的对象没有显示定义，就假定是`this.gameObject.GetCompent();`  
    `[RequireComponent(typeof(CharacterController))]`会迫害unity确保GameObject有一个传入命令的类型组件，可选的.
    ```
- Animator组件  
    ```C#
    private Animator _animator;
    ...
    _animator=GetCOmponent<Animator>();
    ...
    _animator.SetFloat("Speed", MOvement.sqrMagnitude);//用来设置你再Animator中设置的变量的值，sqrMagnitude指的是向量长度的平方，比直接求向量大小要快，可以用来进行比较等操作  
    if(_contact != null){//防止在没有碰撞信息时进行跳跃
         _animator.SetBool("jumping",true);//set the bool value
    }
    
---
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
普通的值类型不可以为null，普通类型不能为null  
- 数值类型  
支持二进制`var b = 0b1010_1011;`  
`cnosole.writeline(1.0.GetType());`得到类型信息  
`float f = 4.5f; decimal d = -1.3M;`  
`int m = int.MaxValue;`  
使用checked抛出异常，或者unchecked不检查
    ```C#
    int c = checked(a*b);
    checked
    {
        int d = a*b;
    }
    ```
    如果溢出则会抛出异常  

    `float min = float.NegativeInfinity;
    double max = double.PositiveInfinity;`
- float 和double的特殊值  
NaN，例子`double.NaN`不是一个值  
double除以0.0 --> 正无穷
double除以-0.0 --> 负无穷  
-double除以 0.0 --> 负无穷
-double 除以 -0.0 --> 正无穷  
0.0/0.0 --> NaN  
当使用==时，NaN不等于任何值，包括NaN，使用object。Equals（）方法时，两个NaN相等，验证某位是否为NaN，可以使用`float.IsNaN(),double.IsNaN()`  
float and double 是基于2来表示数值的，只有可用2表达的数值才是精准的，大多数带有小数的literal都不会被精确表达出来  
- **char**  
System.Char  
占两个字符，用`'x'`表示 
转意字符`\\`  
- **string**  
逐字字符串使用`@`符号加在字符串前，如`string a = @"\\hello";` 
string 有加法方法，可以将两个字符串连接起来，如果一个不是字符串就会调用它的ToString方法，大两室用+做字符串连接的效率很低，最好使用StringBuilder  
**字符串插值string interpolation**可以在字符串中插入值，如：  
    ```C#
    inyt x-4;Console.WriteLines($"A aquare has {x} sides");
    ```
    任何C#表达式都可以出现在{}内，会调用Tostring或者其等效方法。默认只支持单行，多行则需要在$符号前加@如`string a = @$"ohh";  
    string不支持<>等比较操作，需要使用CompareTo方法，
- **数组**  
 继承于System.Array类  
 声明数组  
    ```C#
    char[] vowels = new char[5];
    char[] vowels= {'a', 'b'}; 
    var vowels = new[] {'a', 'b'};//会隐式转换
    System.Console。WriteLine（vowels.GetType());
    ```  

    数组的长度为vowels.Length属性  
    一旦数组被创建，那么长度就是不可改变的,没有赋值会被赋予默认值  
    如果存的是引用类型则会被默认赋值为Null  
    **矩形数组**  
    `int[,] matrix = new int[3,3];`使用GetLength(维度)方法可以返回指定维度的长度，GetLength（0）表示第一维。  
    二维数组初始化可以使用：
    ```C#
    int[,] matrix2 = new int [,]
    {
        {0,1,2},
        {3,4,5},
        {6,7,8}
    };
    ```
    **交错数组**  
    `int [][] matrix = new int[3][];`  
    内层维度并没有具体指明，可以是任意维度。  
    ```C#
    int [][] matrix = new int [3][];
    for(int i = 0; i< matrix.Length; i++>)
    {
        matrix[i] = new int[i+3];
        for(int j = 0; j < matrix[i].Length; j++)
        {
            //todo
        }
    }
    ```  
    unsafe关键字可以绕过边界检查  
- **Stack和Heap**  
Stack存储本地变量和参数，随着函数的进入和退出，Stack也会随之增大和缩小  
Heap是对象（引用类型的实例）所在的地方，一旦某个对象不再被任何存活的东西所引用，那么它就可以被gc释放了。   
static字段在heap上，会存活到应用程序停止。  
除非使用Unsafe否则C#里无法访问未初始化的内容。  
可以通过default来获得任何类型的默认关键值。  
- **参数**  
按值传送，默认都是按值传递的。相当于复制了一份。  
按值传递引用类型的实参，复制的是引用不是对象。  
按引用传递，使用ref关键字。与cpp中的引用一致，在使用前必须被赋值.。  
    ```C#
    static void foo(ref int p)
    {
        ///
    }
    //when you us foo
    foo(ref x);
    ```
    无论是引用类型还是值类型，都可以使用按值或者按引用传递。  
out 关键字在进入函数前不需要被赋值，但是在离开函数前必须被赋值，常常用于从方法中返回多个值。从C#7开始，可以在嗲用方法时使用out声明临时变量，
    ```C#
    myfunc("hello",out string a, out string b);//no need to declare a and b in a line
    write(a);
    myfunc2("hello", out string a, out _);//使用下划线表示我们不需要这个返回值，弃用discard
    ```
    params修饰符  
    在方法的最后一个参数使用params修饰符，可以接受任意数量的该类型参数
    ```C#
    static int Sum(params int[] ints)
    {
        //
    }
    static void Main()
    {
        int total = Sum(1,2,3,4,5);//use
        // int total = Sum(new int[] {1,2,3,4,5}); 
    }
    ```  
    可选参数  
    从C#4开始，方法，构造函数，索引器都可以声明可选参数，可选参数需要在声明时提供默认值，调用时可以不填写可选的参数。必填参数必须在可选参数前面，params修饰的参数还是放在最后面  
    **命名参数**  
    在调用时可以不按照参数顺序传入  
    ```C#
    void Foo(int x, int y)
    {
        //
    }
    int b=0;
    void Foo2()
    {
        Foo1(x: 1, y: 2);
        Foo1(y: 2, x: 1);
        Foo1(y: --b, x: ++b);//Foo(1,-1);
    }
    ```  
    ref locals  
    ```C#  
    int[] numbers = {1,2,3,4};
    ref int numRef = ref numbers[2];//配合ref return 使用，ref return可以从方法返回ref local
    static String x = "hello";
    static ref String GetX() => ref x;//相当于return ref x;
    public static void Main() {
        ref String xRef = ref GetX();
        xRef = "new";
        Console.WriteLine(x);
    ```
- 处理输入  
    ```C#
    string[] input = Console.ReadLine().Split(' ');
    ```  
- **null操作符**  
`??`操作符,意味着如果操作数不是null，则把它给我，否则给我一个默认值，如果左边的表达式非null，那么??右边的表达式就不会被计算。  
    ```C#
    string s1 = null;
    string s2 = s1 ?? "hello";//s2=hello  
    ```
    null条件操作符（elvis)`?.`  
    ```C#
    System.Text.StringBuilder sb = null;
    string s1 = sb.ToString();//sb是null的话会抛出异常
    string s = sb?.ToString();//不会抛出异常，等于下面这句话
    string s = (sb == null ? null : sb.ToString());
    ```
    最终的表达式必须为可以接受null，如：  
    ```C#
    int length = sb?.ToString().Length;//错误，因为int不能被置为null  
    int? length = sb?.ToString().Length;//正确，转为可空值类型。
    ```
- ***语句***  
object类是C#中所有对象的父类，可以存入任何类型。  
switch的特殊用法：  
    ```C# 
        static void TellMeTheType(object x)
        {
            switch(x)
            {
                case int i:
                    Console.WriteLine("it is a int");
                    Console.WriteLine($"The square of {i} is {i*i});
                    break;
                case string s:
                //
                drefault:
                    Console.WriteLine();
                    break;
            }
        }
        //case bool b when b == true:
            //
            break;
    ```
    case null://可以的写法  
    foreach可以迭代enumerable（可枚举）的对象  
    ```C#
    foreach(char c in "Bear" )
    {
        Consloe.WriteLine(c);
    }
    ```
    **跳转语句**  
    跳转语句准寻try语句的可靠性原则，即为在跳出try块时，在到达跳转目标之前，总会先执行try的finally块，不可以从finally块里面调准到外面,除了throw  
    goto语句，吧执行跳转到另一个label的语句块  
    goto label;  
    ```C#
    startLoop:
        if（ i<= 5）{
            Console。Write（）；
            i++;
            goto startloop;
        }
    ```  
    throw语句，抛出异常  
    
    
