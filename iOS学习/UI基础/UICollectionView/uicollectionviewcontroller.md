UICollectionViewController类表示其内容由集合视图组成的视图控制器。它实现以下行为：

###概述

- 如果集合视图控制器具有指定的nib文件或从故事板加载，则从相应的nib文件或故事板加载其视图。如果以编程方式创建集合视图控制器，它将自动创建一个新的未配置集合视图对象，您可以使用collectionView属性访问该对象。

- 从故事板或nib文件加载集合视图时，将从nib文件获取集合视图的数据源和委托对象。如果未指定数据源或委派，则集合视图控制器将自身分配给未指定的角色。

- 当集合视图第一次出现时，集合视图控制器重新加载集合视图数据。它还会在每次显示视图时清除当前选择。您可以通过将clearsSelectionOnViewWillAppear属性的值设置为NO来更改此行为。

为您要管理的每个集合视图创建一个UICollectionViewController的自定义子类。 当初始化控制器时，使用initWithCollectionViewLayout:方法，可以指定集合视图应该具有的布局。 因为最初创建的集合视图没有维度或内容，所以集合视图的数据源和委托（通常是集合视图控制器本身）必须提供此信息。

您可以覆盖loadView方法或任何其他父类方法，但如果这样做，请确保在方法的实现中调用super。如果不这样做，则集合视图控制器可能无法执行维护集合视图完整性所需的所有任务。

---

###API

####初始化UICollectionViewController对象

- \- initWithCollectionViewLayout: 
  >初始化集合视图控制器并使用提供的布局配置集合视图。

####获取集合视图

- collectionView
  > 由此视图控制器管理的集合视图对象。

- collectionViewLayout
  > 用于初始化集合视图控制器的布局对象。


####配置集合视图行为

- clearsSelectionOnViewWillAppear
  > 一个布尔值，指示控制器在集合视图显示时是否清除选择。

- installsStandardGestureForInteractiveMovement(9.0)
  > 指示集合视图控制器是否安装标准手势识别器以驱动重新排序过程的布尔值。

####与导航控制器集成

- useLayoutToLayoutNavigationTransitions
  > 一个布尔值，指示集合视图控制器是否与导航控制器协调进行转换。



