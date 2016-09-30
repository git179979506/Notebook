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

  ```css
  color: red
  background-color: blue
  font-size: 20px
  ```

  * 冒号:左边是属性名，右边是属性值

* CSS的3种书写形式

  * 行内样式（内联样式）：直接在标签的style属性中书写
    ```
    <body style="color: red;">
    ```

  * 页内样式：在本网页的style标签中书写
    ```
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
  - 外部样式：在单独的CSS文件中书写，然后在网页中用link标签引用
  ```
  <link rel="stylesheet" href="index.css">
  ```

- CSS的规律
  - 就近原则（相同的）
  - 叠加原则（不同的）

- CSS的两大重点
 - 属性：通过属性的复杂叠加才能做出漂亮的网页
 - 选择器：通过选择器找到对应的标签设置样式

- CSS选择器 
  - 标签选择器：根据标签名找到标签
  - 类选择器：
  - id选择器：
  - 并列选择器：逻辑或
  - 复合选择器：逻辑与，标签选择器开头
  - 后代选择器：儿子、孙子...
  - 直接后代选择器：儿子
  - 相邻兄弟选择器
  - 属性选择器
  
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

  <p clss="test">段落</p>
  <div clss="test" name="jack">段落</div>
  <p id="main">段落</p>
  ```
  - 伪类
  ![](Snip20160930_4.png)
