UICollectionViewDelegate协议定义了允许您管理集合视图中项目的选择和突出显示以及对这些项目执行操作的方法。 此协议的方法都是可选的。

###概述

此协议的许多方法使用NSIndexPath对象作为参数。 为了支持集合视图，UIKit在NSIndexPath中声明一个类别，使您能够获取表示的项目索引和节索引，并从项目和索引值构造新的索引路径对象。 因为项目位于其部分中，所以通常必须评估节索引号，然后才能通过索引号标识项目。

配置集合视图对象时，将委派对象分配给其委托属性。 有关更多信息，请参阅UICollectionView。

###API

####管理所选单元格
_当您以编程方式设置选择时，不会调用这些方法。_

- \- collectionView:shouldSelectItemAtIndexPath:
  > 询问代理是否应选择指定的项目。

- \- collectionView:didSelectItemAtIndexPath:
  > 告诉委托者选择了指定索引路径上的项目。

- \- collectionView:shouldDeselectItemAtIndexPath:
  > 询问代理是否应取消选择指定的项目。

- \- collectionView:didDeselectItemAtIndexPath:
  > 告诉委托人指定路径上的项目已取消选择。


####管理单元格高亮显示(Highlighting)
_集合视图仅在响应用户交互时调用此方法，如果您以编程方式更改单元格上的突出显示，则不会调用此方法。_


- \- collectionView:shouldHighlightItemAtIndexPath:
  > 询问代理是否应在跟踪期间高亮显示项目。

- \- collectionView:didHighlightItemAtIndexPath:
  > 告诉委托者，指定索引路径处的项目已高亮显示。

- \- collectionView:didUnhighlightItemAtIndexPath:
  > 告诉委托者，高亮显示已从指定索引路径上的项目中删除。

####跟踪视图的添加和删除

- \- collectionView:willDisplayCell：forItemAtIndexPath:
  > 告诉委托人指定的单元格即将显示在集合视图中。

- \- collectionView:willDisplaySupplementaryView:forElementKind:atIndexPath:
  > 告诉代理指定的补充视图即将显示在集合视图中。

- \- collectionView:didEndDisplayingCell:forItemAtIndexPath:
  > 告诉委托者指定的单元格已从集合视图中删除。

- \- collectionView:didEndDisplayingSupplementaryView:forElementOfKind:atIndexPath:
  > 告诉委托者指定的补充视图已从集合视图中删除。

####处理布局更改

- \- collectionView:transitionLayoutForOldLayout:newLayout:(7.0)
  > 要求在指定的布局之间移动时使用的自定义转换布局。

  如果要返回自定义UICollectionViewTransitionLayout对象以在转换期间使用，请实现此方法。转换布局对象允许您在从一个布局转换到下一个布局时自定义单元格和装饰视图的行为。通常，布局之间的转换使得项目直接从它们的当前位置动画到它们的新位置。使用转移布局对象，您可以让对象遵循非线性路径，使用不同的计时算法，或根据传入的触摸事件移动。

  如果您的委托没有实现此方法，则集合视图将创建一个标准的UICollectionViewTransitionLayout对象，并使用该对象来管理转换。

- \- collectionView:targetContentOffsetForProposedContentOffset:(9.0)
  > 使代理有机会自定义布局更改和动画更新的内容偏移量。

  **返回值：**要使用的内容偏移量。如果不实现此方法，则集合视图将使用proposedContentOffset参数中的值。

  在布局更新期间，或者在布局之间转换时，集合视图调用此方法，让您有机会更改建议的内容偏移量，以便在动画结束时使用。如果布局或动画可能导致以不适合您的设计的方式定位项目，则可能返回新值。

  此方法在布局对象的targetContentOffsetForProposedContentOffset: 方法之后调用。在您不想将布局对象子类化以修改内容偏移的情况下实现此方法

- \- collectionView:targetIndexPathForMoveFromItemAtIndexPath:toProposedIndexPath:(9.0)
  > 请求代理移动项目时使用的索引路径。

  **返回值：**要用于项目的索引路径。如果不实现此方法，则集合视图将使用proposedIndexPath参数中的索引路径。

  在交互式移动项目期间，集合视图调用此方法以查看是否要提供与建议路径不同的索引路径。您可以使用此方法来防止用户将项目丢弃在无效位置。例如，您可能会阻止用户删除特定部分中的项目。


####管理单元格的操作

- \- collectionView:shouldShowMenuForItemAtIndexPath:
  > 询问代理是否应该为指定的项目显示操作菜单。

  **返回值：**YES，如果编辑菜单应显示位于项目附近并指向它或NO（如果不应该）。

  如果用户在集合视图中点按保存某个项目，则首先调用此方法（如果已实现）。如果要允许显示编辑菜单，则返回YES。如果不应显示编辑菜单，则返回NO - 例如，如果相应的项目包含不应复制或粘贴的数据，则可能返回NO。

  如果不实现此方法，则默认返回值为NO。

- \- collectionView:canPerformAction:forItemAtIndexPath:withSender:
  > 询问代理，如果它可以对集合视图中的项执行指定的操作。

  **返回值：**如果与操作相对应的命令应出现在编辑菜单中，则为YES，否则为NO。

  此方法在collectionView:shouldShowMenuForItemAtIndexPath:方法之后调用。它允许您从编辑菜单中排除命令。例如，用户可能已经从一个项目复制了一些内容，并且想要将其粘贴到不能接受内容的另一个项目中。在这种情况下，您的方法可能返回NO以防止显示相关命令。

  如果不实现此方法，则默认返回值为NO。


- \- collectionView:performAction:forItemAtIndexPath:withSender:
  > 指示代理对集合视图中的项目执行指定的操作。

  如果用户在编辑菜单中轻击操作，则集合视图会调用此方法。您的实现此方法应该做任何适合的操作。例如，对于复制操作，它应提取相关项目内容并将其写入一般粘贴板或应用程序（私人）粘贴板。

  有关如何执行粘贴板相关操作的信息，请参阅UIPasteboard。

####在集合视图中管理焦点(9.0)

- \- collectionView:canFocusItemAtIndexPath:
  > 询问代理是否可以聚焦在指定索引路径的项目。

  **返回值：**YES，如果项目可以接收聚焦；NO，如果不能。

  您可以使用此方法或单元格的canBecomeFocused方法来控制集合视图中的哪些项目可以接收焦点。焦点引擎首先调用单元格的canBecomeFocused方法，其默认实现延迟到集合视图和此委托方法。

  如果不实现此方法，则关注项目的能力取决于集合视图的项目是否可选。当项目是可选择的时，它们也可以被聚焦，如同该方法返回YES;否则，它们不接收焦点。


- \- indexPathForPreferredFocusedViewInCollectionView:
  > 向代理请求应该关注的单元的索引路径。

  **返回值：**首选单元的索引路径。您指定的索引路径必须对应到集合视图中的有效单元格。

  当焦点即将更改为集合视图时，集合视图必须选择其中的哪些子视图应该接收该焦点。如果集合视图的remembersLastFocusedIndexPath属性设置为YES，则集合视图将返回上次关注的单元格的索引路径。如果remembersLastFocusedIndexPath属性为NO，则集合视图调用此方法，以便您可以指定应接收焦点的单元格。如果不实现此方法，则集合视图返回一个相应的单元格。

  如果您子类化UICollectionView，您还可以通过覆盖preferredFocusedView属性来实现相同的行为，该属性由UIFocusEnvironment协议定义并被所有视图采用。

- \- collectionView:shouldUpdateFocusInContext:
  > 向代理询问是否应该进行重点更改。

  **返回值：**如果焦点更改应该发生，则为YES，如果不应该发生焦点更改为NO。

  在焦点改变可以发生之前，焦点引擎询问所有受影响的视图是否应当发生这样的改变。 作为响应，集合视图调用此方法，让您有机会允许或阻止更改。 返回此方法以防止不应发生的更改。 例如，您可以使用它来确保单元格之间的导航以特定顺序出现。

  如果不实现此方法，则集合视图假定返回值为YES。

  如果您子类化UICollectionView，您还可以通过覆盖shouldUpdateFocusInContext:方法来实现相同的行为，该方法由UIFocusEnvironment协议定义并被所有视图采用。


- \- collectionView:didUpdateFocusInContext:withAnimationCoordinator:
  > 告诉代理发生了焦点更新。

  当发生与焦点相关的更改时，集合视图调用此方法。 您可以使用此方法更新应用程序的状态信息，或动画更改应用程序的视觉外观。

  如果你子类化UICollectionView，你也可以通过覆盖didUpdateFocusInContext:withAnimationCoordinator:方法来实现相同的行为，该方法由UIFocusEnvironment协议定义并被所有视图采用。



