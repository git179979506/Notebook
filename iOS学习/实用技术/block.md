###基础
####作用
保存一段代码

####声明
返回值(^block变量名)(参数)
```
void(^block)();
```

####定义
三种方式 = ^(参数){};
```
// 第一种
void(^block)() = ^{

};

// 第二种
// 如果没有参数，参数可以隐藏；
// 如果有参数，必须要写参数，而且必须有参数变量名
void(^block)(int) = ^(int a){

};

// 第三种
// block返回可以省略，不管有没有返回值，都可以省略
int(^block)() = ^int{
    return 2;
};
```
####类型
```
// int(^)(NSString *)
int(^block)(NSString *) = ^(NSString *name){
    return 2;
};
```

####调用
```
block();
```

####快捷代码块
inlineBlock

####定义block属性
怎么声明block，就怎么定义成属性
```
@property (nonatomic, strong) void(^block)();
```

---

###开发中的使用场景
1. 保存代码：保存代码到模型中
2. 传值
3. block做参数

---

###block的内存管理
> block存放位置：只要block没有引用外部局部变量，block放在全局区

####MRC
1. 只要block引用外部局部变量，block放在`栈`里面
2. block只能使用copy，不能使用retain，使用retain修饰block还是在栈里

####ARC
1. 只要block引用外部局部变量，block放在`堆`里面
2. block使用strong修饰，最好不要使用copy

####扩展

1. block是不是一个对象？答：是。使用'%@'log

2. 如何判断当前文件是MRC，还是ARC
  - dealloc 能否调用super，只有MRC才能调用super
  - 能否使用retain、release，如果能用就是MRC

3. ARC管理原则：只有一个对象没有被强指针修饰就会被销毁，默认局部变量对象都是强指针，存放到堆里

4. MRC管理常识：
  - MRC么有strong、weak，局部变量对象就是相当于基本数据类型
  - MRC给成员属性赋值，一定要使用set方法，不能直接访问下划线成员属性

---

###block造成的循环引用
> 扩展
- 引发原因：引用构成闭环
- 引发的问题：闭环中的对象都不会销毁，造成内存泄漏

1. 原因：block会对里面所有的强指针变量强引用
2. 解决方法:使用__weak修饰
  - 自己的弱指针：`__weak typeof(self) weakSelf = self`
3. 解决block内延时操作时，期间block引用的对象被销毁的问题
  - 解决方法：`__strong typeof(weakSelf) strongSelf = weakSelf`

###block的变量传递
1. 如果是局部变量，block是值传递
2. 如果是静态变量、全局变量、__block修饰的变量，block是指针传递

> 文档查询
working开头的是讲原理

