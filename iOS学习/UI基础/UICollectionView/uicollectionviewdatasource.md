采用UICollectionViewDataSource协议的对象负责提供集合视图所需的数据和视图。 数据源对象表示应用程序的数据模型，并根据需要向集合视图提供信息。 它还处理创建和配置单元格以及由集合视图使用的辅助视图来显示您的数据。

###概述

至少，所有数据源对象必须实现collectionView:numberOfItemsInSection:和collectionView:cellForItemAtIndexPath:方法。这些方法负责返回集合视图中的项目数量以及项目本身。协议的其余方法是可选的，仅当您的集合视图将项目组织为多个部分或为给定部分提供页眉和页脚时才需要。

配置集合视图对象时，将数据源分配给其dataSource属性。有关集合视图如何与其数据源一起使用以呈现内容的更多信息，请参阅UICollectionView。

###API

####获取项目和节指标
- \- collectionView:numberOfItemsInSection:
  > **Required.**向您的数据源对象询问指定部分中的项目数。

- \- numberOfSectionsInCollectionView:
  > 向数据源对象询问集合视图中的节数。

####获取项目的视图

- \- collectionView:cellForItemAtIndexPath:
  > **Required.**请求您的数据源对象与集合视图中指定项目对应的单元格。

- \- collectionView:viewForSupplementaryElementOfKind:atIndexPath:
  > 请求您的数据源对象提供一个补充视图以显示在集合视图中。

####重新排序项目(9.0)

- \- collectionView:canMoveItemAtIndexPath:
  > 询问您的数据源对象是否可以将指定的项目移动到集合视图中的另一个位置。

- \- collectionView:moveItemAtIndexPath:toIndexPath:
  > 告诉您的数据源对象将指定的项目移动到其新位置
