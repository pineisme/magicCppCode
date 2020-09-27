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
- char  
System.Char  
占两个字符，用`'x'`表示 
转意字符`\\`  
- string  
逐字字符串使用`@`符号加在字符串前，如`string a = @"\\hello";`