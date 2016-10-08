eclipse、Deamwaver、**WebStorm**

### Web3.0

* 主流技术：HTML5+CSS3
  * HTML5亮点：Canvas HTML5音视频 Web存储 Geolocation Workers多线程处理
  * CSS3亮点：设计动画 2D变形 N多新特性


### 网页的组成

* HTML:网页的具体内容和结构
* CSS：网页的样式
* JavaScript：网页的交互效果

### HTML5新增标签

> 新增了27个标签，废弃了16个标签，主要包括结构性标签、级块性标签、行内语义性标签、交互性标签。

* 结构性标签（负责web上下文结构的定义）

  * article    文章主题内容
  * header     标记头部区域内容
  * footer     标记脚步区域内容
  * section    区域章节表述
  * nav        菜单导航，链接导航

* 块级性标签

  * aside
  * figure
  * code
  * dialog

* 行内语义性标签

  * meter 特定范围
  * time
  * progress    进度条
  * video       视频元素
  * audio       音频元素


### css

* 什么是CSS

  * CSS的全称是Cascading Style Sheets，层叠样式表
  * 它用来控制HTML标签的样式

* CSS的编写格式是键值对的形式

  * 冒号:左边是属性名，右边是属性值

  ```css
  color: red
  background-color: blue
  font-size: 20px
  ```

* CSS的3种书写形式

  * 行内样式（内联样式）：直接在标签的style属性中书写

    ```
    <body style="color: red;">
    ```

  * 页内样式：在本网页的style标签中书写

    ```css
    <style>
        body {
            color: red;
        }
        div {
            font-size: 28px;
        }
        p {
            border: 4px solid yellow;
        }
    </style>
    ```

  * 外部样式：在单独的CSS文件中书写，然后在网页中用link标签引用

    ```
    <link rel="stylesheet" href="index.css">
    ```



* CSS的规律

  * 就近原则（相同的）
  * 叠加原则（不同的）

* CSS的两大重点

  * 属性：通过属性的复杂叠加才能做出漂亮的网页
  * 选择器：通过选择器找到对应的标签设置样式

* CSS常用选择器

  * 标签选择器：根据标签名找到标签
  * 类选择器：类能有多个
  * id选择器：id只能有一个，不能重复
  * 并列选择器：逻辑或
  * 复合选择器：逻辑与，标签选择器开头
  * 后代选择器：儿子、孙子...
  * 直接后代选择器：儿子
  * 相邻兄弟选择器
  * 属性选择器
  * 伪类：当你执行某些操作时触发
    ![](/assets/Snip20160930_4.png)
  * 伪元素
    ![](/assets/Snip20160930_6.png)

  > 例子

  ```CSS
  /* 标签选择器 */
  div {
      color: red;
  }

  /* 类选择器 */
  .test {
     color: green;
  }

  /* id选择器 */
  #main {
      font-size: 40px;
  }

  /* 并列选择器 */
  div , .high {
      color: red;
  }

  /* 复合选择器 */
  p.test {
      background-color: yellow;
  }

  /* 后代选择器 */
  div p {
      color: red;
  }

  /* 直接后代选择器 */
  div > a {
      color: green;
  }

  /* 相邻兄弟选择器 */
  div + p {
  }

  /* 属性选择器 */  
  div[name] {
  }

  div[name="jack"] {
  }

  div[name][age] {
  }

  /* 伪类 */
  input:focus {
  }

  <p clss="test">段落</p>
  <div clss="test" name="jack">段落</div>
  <p id="main">段落</p>
  ```

* CSS选择器优先级

  * 相同的类型的选择器遵循：a.就近原则 b.叠加原则
  * 不同类型的类型的选择器遵循：

    * important &gt; 内联 &gt; id &gt; 类 \| 伪类 \| 属性选择 \| 伪元素 &gt; 标签 &gt; 通配符 &gt; 继承

  * 选择器的针对性越强，它的优先级越高

  * 权值：选择器的权值加到一起，大的优先，如果权值相同，后定义的优先
    ![](/assets/Snip20160930_7.png)



* important

  ```CSS
  div { /* 权值：1 */
      color: red !important;
  }
  ```

* 通配符

  ```CSS
  /*
  通配符：
     1、优先级别非常低
     2、性能比较差
  */
  * {
     font-size: 30px;
  }
  ```


### HTML标签的类型

#### 标签类型

* 块级标签

  * 独占一行
  * 能随时设置宽度和高度
  * 比如：div、p、h1、h2、ul、li

* 行内标签（内联标签）

  * 多个行内标签能同时显示在一行
  * 宽度和高度取决于内容的尺寸
  * 比如：span、a、label

* 行内-块级标签（内联-块级标签）

  * 多个行内-块级标签可以显示在同一行
  * 能随时设置宽度和高度
  * 比如：input、button


#### 修改标签的显示类型

* CSS中的display属性能修改标签的显示类型
  * none：隐藏标签
  * block：让标签变为块级标签
  * inline：让标签变为行内标签
  * inline-block：让标签变为行内块级标签


### CSS属性

#### 根据继承性区分

* 可继承属性

  * 父标签的属性值会传递给子标签
  * 一般是文字控制属性

* 不可继承属性

  * 父标签的属性值不会传递给子标签
  * 一般是区块控制属性


#### 常见属性

* 所有标签可继承

  ```
  visibility、cursor
  ```

* 内联标签可继承

  ```
  line-height、color、font、font-family、font-size、font-weight、text-decoration
  ```

* 列表标签可继承

  ```
  list-style
  ```

* 不可继承属性

  ```
  display、margin、border、padding、background
  height、min-height、max-height、width、min-width、max-width
  overflow、position、left、right、top、bottom、z-index
  float、clear
  table-layout、vertical-align
  page-break-after、page-break-before
  unicode-bidi
  ```


### 盒子模型

> content：内容 padding：内边距 border：边框 margin：外边距

* 四个属性

  * 内容（content）
    ![](/assets/Snip20161008_4.png)
  * 填充（padding，内边距）
    ![](/assets/Snip20161008_5.png)
    ![](/assets/Snip20161008_6.png)
  * 边框（border）
    ![](/assets/Snip20161008_7.png)
  * 边界（margin，外边距）
    ![](/assets/Snip20161008_8.png)
    ![](/assets/Snip20161008_9.png)

* 标准的盒子模型
  ![](/assets/Snip20161008_1.png)

* IE盒子模型
  ![](/assets/Snip20161008_2.png)


