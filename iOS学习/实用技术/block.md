###作用
保存一段代码

###声明
返回值(^block变量名)(参数)
```
void(^block)();
```

###定义
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
###类型
```
// int(^)(NSString *)
int(^block)(NSString *) = ^(NSString *name){
    return 2;
};
```

###调用
```
block();
```

###快捷代码块
inlineBlock