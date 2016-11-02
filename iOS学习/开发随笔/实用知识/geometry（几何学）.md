###frame和bounds、center
使用bounds和center结合定位会更精准

- frame:描述`视图(可视范围)`在其superview的坐标系中的位置和大小。
  ```
  此矩形在其父视图的坐标系中定义视图的大小和位置。
  在布局操作期间使用此矩形来确定视图的大小和位置。
  设置此属性将相应地更改center属性指定的点和bounds矩形中的大小。 
  frame矩形的坐标总是以点指定。
  ```

- bounds:描述`视图(可视范围)`在其自身坐标系中的位置和大小。
  ```
  在屏幕上，bounds矩形表示视图的可见部分与其frame矩形相同。
  默认情况下，bounds矩形的原点设置为（0，0），但您可以更改此值以显示视图的不同部分。
  bounds矩形的大小(size)与frame矩形的大小相关联，因此对一个矩形的更改会影响另一个。
  更改bounds的大小会相对于其中心点(center)增大或缩小视图。边界矩形的坐标总是以点指定。

  更改frame矩形会自动重新显示接收器，而不调用drawRect:方法。 
  如果想要在frame矩形更改时调用drawRect:方法，请将contentMode属性设置为UIViewContentModeRedraw。

  对此属性的更改可以进行动画处理。

  默认边界原点是（0,0），大小与frame矩形的大小相同。

  更改frame矩形会自动重新显示接收器，而不调用drawRect:方法。
  如果想要在框架矩形更改时调用drawRect:方法，请将contentMode属性设置为UIViewContentModeRedraw。

  对此属性的更改可以进行动画处理。 
  但是，如果transform属性包含非identity变换，则frame属性的值是未定义的，不应该修改。 
  在这种情况下，您可以使用center属性重新定位视图，然后使用bounds属性调整大小。
  ```
  > __警告__
  >
  > 如果transform属性不是identity变换，那么此属性的值是未定义的，因此应该被忽略。


