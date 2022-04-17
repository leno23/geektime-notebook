### 基本类型

一个角色判断的例子

```js
function initByRole(role){
if(role === 1 || role === 2){
    
}else if(role === 3 || role === 4){

}else if(role === 5){

}else{

}
```

缺点：

1.可读性差：很难记住数字含义

2.可维护性差：硬编码，牵一发而动全身

#### 枚举  

一组有名字的常量集合

例如： 电话簿

```
张三 ---- 13x-xxxx-xxxx
李四 ---- 15x-xxxx-xxxx
```

##### 数字枚举

```tsx

enum Role {
    // 值默认从0开始递增，赋予数字，则后面在这个数字基础上递增
    Repoter,  
    Developer,
    Maintainer,
    Owner,
    Guest,
}
```

编译为js，使用反向映射实现

```js
var Role;
(function (Role){
	Role[Role['Reporter'] = 0] = 'Reporter'
	Role[Role['Developer'] = 1] = 'Developer'
	Role[Role['Maintainer'] = 2] = 'Maintainer'
	Role[Role['Owner'] = 2] = 'Owner'
	Role[Role['Guest'] = 2] = 'Guest'
})(Role || (Role = {}))
```

##### 字符串枚举

```tsx
enum Message{
	Success = '成功',
    Fail='失败了'
}
```

编译后的js，只有成员名称作为key，没有进行反向映射

```tsx
var Message;
(function (Message){
	Role[Role['Success'] = '成功了'
	Role['Fail'] = '失败了'
})(Message || (Message = {}))
```

##### 异构枚举

```tsx
enum Answer{
    N,
    Y='yes'
}
```



#### 枚举成员的分类

```tsx
enum Char{
    a,
    b=Char.a,
    c=1+3,
    D=Math.random(),
    e='123'.length,
    // f  
}
```



