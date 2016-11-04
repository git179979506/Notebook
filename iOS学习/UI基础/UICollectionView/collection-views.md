集合视图使用标准或自定义布局显示数据项的有序集合。与表视图类似，集合视图从您的自定义数据源对象获取数据，并使用单元格，布局和补充视图的组合显示它。集合视图可以在网格中或您设计的自定义布局中显示项目。无论您选择的布局样式如何，集合视图最适合显示非分层的有序数据项。

**Purpose.**集合视图允许用户：
- 查看可变大小项目的目录，可选择分为多个章节
- 添加到、重新排列和编辑项目集合
- 从频繁更改的项目显示中选择

**Configuration.**在Interface Builder中的Attributes Inspector的“集合视图”部分中配置集合视图。有些配置不能通过Attributes Inspector进行，因此必须以编程方式进行。 如果您愿意，也可以以编程方式设置其他配置。

![](/assets/Snip20161104_10.png)

####集合视图的内容

单元格是您的集合视图的主要内容。单元格的工作是为您的数据源对象显示单个项目的内容。每个单元格必须是UICollectionViewCell类的实例，您可以根据需要呈现您的内容。单元对象为管理自己的选择和高亮状态提供了固有的支持，虽然一些自定义代码必须被写入以实际应用高亮到单元格。UICollectionViewCell对象是您用于主要数据项的特定类型的可重用视图。

为了管理数据的可视化呈现，集合视图使用许多相关类，例如UICollectionViewController，UICollectionViewDataSource，UICollectionViewDelegate，UICollectionReusableView，UICollectionViewCell，UICollectionViewLayout和UICollectionViewLayoutAttributes。

集合视图强制在呈现的数据和用于呈现的视觉元素之间的严格分离。 您的应用程序是通过自定义数据源对象管理数据负责。 （要了解如何创建这些对象，请参阅Designing Your Data Objects。）您的应用程序还提供用于呈现数据的视图对象。 集合视图接受您的视图，并且在布局对象的帮助下，指定放置和其他视觉属性 — 完成在屏幕上显示它们的所有工作。



