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