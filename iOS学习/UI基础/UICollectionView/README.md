> 1. collection view: 集合视图
> 2. item: 项目
> 3. cell: 单元格
> 4. supplementary view: 补充视图

UICollectionView类管理数据项的有序集合，并使用可自定义的布局来呈现它们。集合视图\(collection view\)提供与表视图相同的一般功能，除了集合视图能够支持的不仅仅是单列布局。集合视图支持可定制的布局，可用于实现多列网格，平铺布局，圆形布局等。 你甚至可以动态地更改集合视图的布局。

### 概述

**图1** 使用流布局的集合视图
![](/assets/Snip20161103_9.png)

向用户界面添加集合视图时，应用程序的主要任务是管理与该集合视图相关联的数据。集合视图从数据源对象获取其数据，数据源对象是符合UICollectionViewDataSource协议并由应用程序提供的对象。收集视图中的数据被组织成单独的项目\(item\)，然后可以将它们分组成多个部分以用于呈现。项目是要显示的最小数据单位。例如，在照片应用程序中，项目可能是单个图像。集合视图使用单元格\(cell\)在屏幕上显示项目，该单元格是数据源配置和提供的UICollectionViewCell类的实例。

除了它的单元格，集合视图也可以使用其他类型的视图来呈现数据。这些补充视图\(supplementary view\)可以是与单独单元分离但仍传达某种信息的段标题和页脚。对补充视图的支持是可选的，并由收集视图的布局对象定义，它也负责定义这些视图的位置。

除了将其嵌入到用户界面中之外，还可以使用UICollectionView对象的方法来确保项目的可视化呈现符合数据源对象中的顺序。因此，无论何时在集合中添加，删除或重新排列数据，都可以使用此类的方法插入，删除和重新排列相应的单元格。您还可以使用集合视图对象来管理所选项目，但对于此行为，集合视图使用其关联的委托对象。

#### 集合视图和布局对象

与集合视图相关联的一个非常重要的对象是layout对象，它是UICollectionViewLayout类的子类。布局对象负责定义集合视图内的所有单元格和补充视图的组织和位置。虽然它定义了它们的位置，但布局对象实际上并不将该信息应用于相应的视图。因为单元格和补充视图的创建涉及集合视图和数据源对象之间的协调，所以集合视图实际上将布局信息应用于视图。因此，在某种意义上，布局对象像另一个数据源，只提供可视信息而不是项目数据。

通常在创建集合视图时指定布局对象，但也可以动态更改集合视图的布局。 布局对象存储在collectionViewLayout属性中。 设置此属性将直接更新布局，而不会对更改进行动画处理。如果要对更改进行动画处理，则必须调用setCollectionViewLayout:animated:completion:方法。

如果要创建一个交互式转换（由手势识别器或触摸事件驱动）使用startInteractiveTransitionToCollectionViewLayout:completion:方法来更改布局对象。该方法安装一个中间布局对象，其目的是使用您的手势识别器或事件处理代码来跟踪转换进度。当事件处理代码确定转换完成时，它调用finishInteractiveTransition或cancelInteractiveTransition方法来删除中间布局对象并安装预期的目标布局对象。

#### 创建单元格和补充视图

集合视图的数据源对象提供项目的内容和用于呈现该内容的视图。当集合视图首次加载其内容时，它要求其数据源为每个可见项提供视图。为了简化代码的创建过程，集合视图要求您始终将视图取出队列，而不是在代码中显式创建它们。有两种方法用于出队视图。 您使用的视图取决于请求的视图类型：

* 使用dequeueReusableCellWithReuseIdentifier:forIndexPath:获取集合视图中项目的单元格。
* 使用dequeueReusableSupplementaryViewOfKind:withReuseIdentifier:forIndexPath:方法获取布局对象请求的补充视图。

在调用这些方法之一之前，必须告诉集合视图如何创建相应的视图（如果尚不存在）。为此，您必须使用集合视图注册类或nib文件。例如，当注册单元格时，您使用registerClass:forCellWithReuseIdentifier:或registerNib:forCellWithReuseIdentifier:方法。作为注册过程的一部分，您可以指定用于标识目的视图的重用标识符。这是以后视图出列时使用的同一个字符串。

在对delegate方法中的相应视图出队之后，配置其内容并将其返回到集合视图以供使用。从布局对象获取布局信息后，集合视图将其应用于视图并显示它。

有关实现数据源方法以创建和配置视图的更多信息，请参阅UICollectionViewDataSource。

有关外观和行为配置的详细信息，请参阅 Collection Views。

#### 交互式重新排序项目

集合视图允许您根据用户交互移动项目。通常，集合视图中项目的顺序由数据源定义。如果您支持用户重新排列项目的能力，您可以配置手势识别器来跟踪用户与集合视图项目的交互，并更新该项目的位置。

要开始交互式重新定位项目，请调用集合视图的beginInteractiveMovementForItemAtIndexPath:方法。当您的手势识别器正在跟踪触摸事件时，调用updateInteractiveMovementTargetPosition:方法来报告触摸位置的更改。完成跟踪手势后，调用endInteractiveMovement或cancelInteractiveMovement方法来结束交互并更新集合视图。

在用户交互期间，收集视图会动态地使其布局无效，以反映项目的当前位置。如果不执行任何操作，默认布局行为会为您重新定位项目，但如果需要，您可以自定义布局动画。当交互完成时，使用项目的新位置更新其数据源对象。

UICollectionViewController类提供了一个默认的手势识别器，您可以使用它重新排列其托管集合视图中的项目。要安装此手势识别器，请将集合视图控制器的installsStandardGestureForInteractiveMovement属性设置为YES。

#### Interface Builder属性

**表1** 列出了在Interface Builder中为集合视图配置的属性。

| **属性** | **描述** |
| --- | --- |
| Items | 原型单元格\(prototype cells\)的数量。此属性控制指定数量的原型单元格供您在故事板中配置。集合视图必须总是具有至少一个单元格，并且可以具有用于显示不同类型的内容或以不同方式显示相同内容的多个单元格。 |
| Layout | 要使用的布局对象。使用此控件在UICollectionViewFlowLayout对象和您定义的自定义布局对象之间进行选择。 |

选择流布局\(flow layout\)时，集合视图的大小检查器包含用于配置流布局度量的附加属性。使用这些属性配置单元格的大小，页眉和页脚的大小，单元格之间的最小间距以及单元格每个部分周围的任何边距。有关流布局度量的含义的更多信息，请参阅UICollectionViewFlowLayout。

#### 国际化\(Internationalization\)

集合视图没有其自己的国际化的直接内容。相反，您将集合视图的单元格和可重用视图国际化。有关国际化的详细信息，请参阅 Internationalization and Localization Guide。

#### 辅助功能\(Accessibility\)

集合视图没有自己的内容可访问。如果您的单元格和可重用视图包含标准UIKit控件（如UILabel和UITextField），则可以使这些控件可访问。当集合视图更改其屏幕布局时，它将发布UIAccessibilityLayoutChangedNotification通知。

有关使界面可访问的一般信息，请参阅 Accessibility Programming Guide for iOS。

---

###API
####初始化集合视图
- \- initWithFrame:collectionViewLayout:

####配置集合视图
- delegate
- dataSource
- backgroundView

####创建集合视图单元格

- \- registerClass:forCellWithReuseIdentifier:  注册类以用于创建新的集合视图单元格。
- \- registerNib:forCellWithReuseIdentifier:  注册用于创建新集合视图单元格的nib文件。
- \- registerClass:forSupplementaryViewOfKind:withReuseIdentifier:  注册类以用于为集合视图创建补充视图。
- \- registerNib:forSupplementaryViewOfKind:withReuseIdentifier:  注册一个nib文件，用于为集合视图创建补充视图。
- \- dequeueReusableCellWithReuseIdentifier:forIndexPath:  返回由其标识符定位的可重用单元格对象
- \- dequeueReusableSupplementaryViewOfKind:withReuseIdentifier:forIndexPath:  返回由其标识符和类型定位的可重用补充视图。

####更改布局

- collectionViewLayout 用于组织收集的视图项目的布局。
- \- setCollectionViewLayout:animated: 更改集合视图的布局，并选择性地对更改进行动画处理。
- \- setCollectionViewLayout:animated:completion: 更改集合视图的布局，并在动画完成时通知您。
- \- startInteractiveTransitionToCollectionViewLayout:completion: 使用交互式转场效果更改集合视图的当前布局。
- \- finishInteractiveTransition 通过安装预期的目标布局，指示集合视图完成交互式转换。
- \- cancelInteractiveTransition 指示集合视图中止交互式转换并返回到其原始布局对象。

####重新载入内容

- \- reloadData 重新加载集合视图的所有数据。
- \- reloadSections: 在集合视图的指定部分重新加载数据。
- \- reloadItemsAtIndexPaths: 仅重新装入指定索引路径中的项目。

####获取集合视图的状态

- numberOfSections 返回集合视图显示的节数。
- \- numberOfItemsInSection: 返回指定节中的项目数。
- visibleCells 返回集合视图当前显示的可见单元格数组。

####插入、移动和删除项目

- \- insertItemsAtIndexPaths: 在指定的索引路径插入新项目。
- \- moveItemAtIndexPath:toIndexPath: 在集合视图中将项目从一个位置移动到另一个位置。
- \- deleteItemsAtIndexPaths: 删除指定索引路径中的项目。

####插入、移动和删除节

- \- insertSections: 在指定的索引处插入新节。
- \- moveSection:toSection: 将集合视图中的一个部分从一个位置移动到另一个位置。
- \- deleteSections: 删除指定索引处的节。

####交互式重新排序项目（9.0）

- \- beginInteractiveMovementForItemAtIndexPath: 在指定的索引路径启动项目的交互式移动。
- \- updateInteractiveMovementTargetPosition: 更新集合视图边界内项目的位置。
- \- endInteractiveMovement 结束交互式移动跟踪，并将目标项目移动到其新位置。
- \- cancelInteractiveMovement 结束交互式移动跟踪，并将目标项目返回到其原始位置。

####管理选择

- allowsSelection 一个布尔值，指示用户是否可以在集合视图中选择项目。
- allowsMultipleSelection 布尔值，用于确定用户是否可以在集合视图中选择多个项目。
- indexPathsForSelectedItems 所选项目的索引路径。(10.0)
- \- selectItemAtIndexPath:animated:scrollPosition: 在指定的索引路径中选择项目，并可选择将其滚动到视图。
- \- deselectItemAtIndexPath:animated: 取消选择指定索引处的项目。

####Managing Focus (10.0)

- remembersLastFocusedIndexPath 一个布尔值，指示集合视图是否自动将焦点分配给最后焦点索引路径上的项目。

####在集合视图中定位项目和视图

- \- indexPathForItemAtPoint: 返回集合视图中指定点处项目的索引路径。
- indexPathsForVisibleItems 集合视图中可见项目的数组。
- \- indexPathForCell: 返回指定单元格的索引路径。
- \- cellForItemAtIndexPath: 返回指定索引路径处的可见单元格对象。
- \- indexPathsForVisibleSupplementaryElementsOfKind: 返回指定类型的所有可见辅助视图的索引路径。(9.0)
- \- supplementaryViewForElementKind:atIndexPath: 返回指定索引路径的补充视图。(9.0)
- \- visibilitySupplementaryViewsOfKind: 返回指定类型的可见辅助视图的数组。(9.0)

####获取布局信息

- \- layoutAttributesForItemAtIndexPath: 返回指定索引路径下项目的布局信息。
- \- layoutAttributesForSupplementaryElementOfKind:atIndexPath: 返回指定补充视图的布局信息。

####将项滚动到视图
- \- scrollToItemAtIndexPath:atScrollPosition:animated: 滚动收集视图内容，直到指定的项目可见。

####动画对集合视图的多个更改
- \- performBatchUpdates:completion: 以组形式动画多次插入，删除，重新加载和移动操作。

####常量

- UICollectionViewScrollPosition 指示如何将项滚动到集合视图的可见部分的常量。
- UICollectionViewLayoutInteractiveTransitionCompletion 在集合视图的交互式转换结束时调用的完成block。


