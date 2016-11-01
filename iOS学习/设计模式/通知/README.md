###简介
NSNotificationCenter对象（或简称为通知中心）提供用于在程序内广播信息的机制。NSNotificationCenter对象实质上是一个通知分派表。

###概述
对象可以使用addObserver:selector:name:object:`或`addObserverForName:object:queue:usingBlock:`方法向通知中心注册来接受接收通知（NSNotification对象）。每次调用此方法都会指定一组通知。 因此，可以通过多次调用这些方法让对象为不同通知集注册为观察者。每个运行的Cocoa程序都有一个默认的通知中心。 您通常不创建自己的。 NSNotificationCenter对象只能在单个程序中传递通知。 如果要将通知发布到其他进程或从其他进程接收通知，请使用NSDistributedNotificationCenter的实例。

###NSNotificationCenter
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

###通知注意点
- 通知是有顺序的，一定要先监听再发送
- 接收通知和发布通知在同一个线程，由发布通知所在的线程决定
- 即在哪条线程发布通知，就在哪条线程接收通知


> 提示：

> 如果您的应用程序指定iOS 9.0和更高版本或OS X v10.11及更高版本，则不需要在其释放方法中移除注册观察者。

> 如果您的应用程序指定早期版本，请确保在addObserver:selector:name:object:中指定的观察者或任何对象释放之前调用removeObserver:name:object:。

> 在dealloc方法中调用removeObserver:是安全的。


###NSNotification


