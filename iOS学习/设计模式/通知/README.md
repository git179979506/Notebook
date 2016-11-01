###NSNotificationCenter
####简介
NSNotificationCenter对象（或简称为通知中心）提供用于在程序内广播信息的机制。NSNotificationCenter对象实质上是一个通知分派表。

####概述
对象可以使用addObserver:selector:name:object:`或`addObserverForName:object:queue:usingBlock:`方法向通知中心注册来接受接收通知（NSNotification对象）。每次调用此方法都会指定一组通知。 因此，可以通过多次调用这些方法让对象为不同通知集注册为观察者。每个运行的Cocoa程序都有一个默认的通知中心。 您通常不创建自己的。 NSNotificationCenter对象只能在单个程序中传递通知。 如果要将通知发布到其他进程或从其他进程接收通知，请使用NSDistributedNotificationCenter的实例。

####获取通知中心
- defaultCenter

####监听通知
- [\- addObserverForName:object:queue:usingBlock:](./监听者管理.md#m1)
- \- addObserver:selector:name:object:

####移除监听者
- \- removeObserver:
- \- removeObserver:name:object:

####发布通知
- \- postNotification:
- \- postNotificationName:object:
- \- postNotificationName:object:userInfo:

####通知注意点
- 通知是有顺序的，一定要先监听再发送
- 接收通知和发布通知在同一个线程，由发布通知所在的线程决定
- 即在哪条线程发布通知，就在哪条线程接收通知


> 提示：

> 如果您的应用程序指定iOS 9.0和更高版本或OS X v10.11及更高版本，则不需要在其释放方法中移除注册观察者。

> 如果您的应用程序指定早期版本，请确保在addObserver:selector:name:object:中指定的观察者或任何对象释放之前调用removeObserver:name:object:。

> 在dealloc方法中调用removeObserver:是安全的。



###NSNotification
####简介
NSNotification对象封装信息，以便可以通过NSNotificationCenter对象将其广播到其他对象。 NSNotification对象（称为通知）包含名称，对象和可选字典。 名称是标识通知的标记。 对象是通知的海报想要发送给该通知的观察者的任何对象（通常，它是发布通知的对象）。 字典存储其他相关对象（如果有）。 NSNotification对象是不可变对象。

####概述
您可以使用类方法notificationWithName:object:或notificationWithName:object:userInfo:创建通知对象。但是，通常不会直接创建自己的通知。 NSNotificationCenter的方法postNotificationName:object:和postNotificationName:object:userInfo:允许您方便地发布通知，而不首先创建它。

> Note

> Swift覆盖到Foundation框架提供了Notification结构体，它桥接到NSNotification类。 Notification值类型提供与NSNotification引用类型相同的功能，并且两者可以在与Objective-C API交互的Swift代码中互换使用。这种行为类似于Swift如何将标准字符串，数字和集合类型桥接到其相应的Foundation类。

#####对象比较(Object Comparison)
使用针对本地通知的指针相等来比较通知的对象。分布式通知使用字符串作为它们的对象，并且使用isEqual来比较这些字符串：因为指针相等在超过进程边界上没有意义。

#####创建子类
您可以子类化NSNotification来包含通知名称，对象和字典之外的信息。 这些额外的数据必须在通知者和观察者之间达成一致。
NSNotification是一个没有实例变量的类集群。 因此，您必须子类化NSNotification并覆盖基本方法name，object和userInfo。 你可以选择你喜欢的任何指定的初始化器，但确保初始化器不调用[super init]。 NSNotification不意味着直接实例化，它的init方法引发一个异常。

####创建通知
- \+ notificationWithName:object:
- \+ notificationWithName:object:userInfo: 
- \- initWithName:object:userInfo:

####获取通知信息
- name
  - 通常，您可以使用此属性查看在接收通知时要处理的通知类型。 
  - 通知名称可以是任何字符串。为避免名称冲突，您可能需要使用特定于应用程序的前缀。

- object
  - 这通常是发布此通知的对象。 它可能为nil。
  - 通常，您可以使用此方法来查找通知在接收通知时适用的对象。

- userInfo
  - 可能是nil。
  - 用户信息字典存储接收通知的对象可能使用的任何其他对象。


####相关文档
Notification Programming Topics



