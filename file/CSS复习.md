### CSS 复习

- CSS 盒子模型

  - 答：css 盒子模型包括 IE 盒子模型（怪异盒模型）以及 W3C 标准盒子模型 盒子模型从外到内包括 `margin`+ `boeder`+ `padding ` +`content`

    区别:在于宽度的计算不同 W3C 标准盒子模型 `width`指的是`content`的宽度 但是 IE 盒子模型 width 指的是 ` content + padding +border`

    在 css3 中引入了`box-sizing`的属性 一般情况下 `box-sizing：content-box ` [标准盒子模型] `box-sizing:border-box`表示 IE 盒子模型;

- link 标签和 import 标签的区别

  - 答：`link` 标签是 HTML 属性没有兼容性 `@import`是 css3 提出的需要兼容 IE5 以上的；

    当页面被加载时，link 会同时被加载 但是`@import` 引用的 css 需要页面加载完才加载 ；

    `link`方式样式的权重高于`@import`

- BFC [块级格式化上下文用于清除浮动造成的高度塌陷]

  - 答：高度塌陷:当所有的子元素浮动的时候，且父元素没有设置高度，这时候父元素就会产生高度塌陷;position 为 fixed 和 absolute;

  清除浮动的方式：

  - 给父元素单独定义高度 优点：快速简单代码少 缺点：无法实现响应式布局
  - 给父元素定义`overflow:hidden;zoom:1`(针对 ie6 的兼容) 优点：快速简单代码少 缺点：超出部分会被隐藏 布局需要注意
  - 父元素定义`overflow:auto`优点 简单代码少 兼容性好 缺点：当内部宽高超出父级 div 会出现滚动条
  - 在浮动元素后面添加一个空标签 `clear:both;height:0;overflow:hidden` 优点 简单代码少 兼容性好 缺点：增加了一个空标签 不利于页面优化
  - 给塌陷的元素添加 after 伪元素【万能清除法】

  ```
    father:after{
      Content:"随便";
      Clear:both;
      display:block;
      height:0;
      overflow:hidden;
      visibility:hidden
    }
  ```

- 子元素如何在父元素中居中

  - 水平居中：
    - 答：子父元素宽度固定，子元素设置`margin：0 auto` 并且子元素不能设置浮动 否则居中失效
    - 子父元素宽度固定，父元素设置`text-align:center`子元素设置`display:inline-block` 并且子元素不能设置浮动，否则居中失效
  - 水平垂直居中

    - 父元素设置弹性盒子，
      ```
        display:flex;
        justify-content:center;
        align-ltem:center;
      ```
    - 子元素相对于父元素绝对定位，子元素`top,left`的值为 50%，`transform:translate(-50%,-50%)`

      ```
      .son{
        position:absolute;
        top:50%;
        left:50%;
        transform:translate(-50%,-50%)
      }
      ```

    - 子元素相对于父元素绝对定位,子元素的上下左右都为 0，然后设置子元素的 margin 为 0 auto

      ```
      .son{
        position:absolute;
        left:0;
        right:0;
        top:0;
        bottom:0;
        margin:auto
      }
      ```

- html5 新增的语义化标签优点以及有哪些语义化标签

  - 答：优点：提升可访问性 有利于 SEO 结构清晰 有利于维护

  - `nav section header main footer aside video Hgroup`

- 定位的属性值有什么区别

  - `relative` 相对定位 不脱离文档流 相对于元素本身定位
  - `absolute` 绝对定位 脱离文档流 相对于离最近的父元素是 relative 的元素定位
  - `fixed` 固定定位 脱离文档流 相对于浏览器本身定位
  - `static` 默认定位 元素出现在正常的流中

- `px rem em` 的区别

  - `px` 绝对长度单位，像素 px 是相对于显示器屏幕分辨率来说的
  - `em` 相对长度单位 相对于当前对象内文本的字体尺寸
    - em 的值并不是固定的
    - em 会继承父级元素的字体大小 （参考的是父元素的`font-size`）
    - em 中所有的字体都是相对于父元素的大小决定的
  - `rem` 相对于 HTML 根元素的`font-size`
    - `1em =1rem = 16px `在 body 中加入 font-size：62.5%这样直接就是原来的 px 数值除以 10 加上 em 就可以

- Css 选择器有哪些，哪些属性可以继承，优先级如何计算？Css3 新增的伪类有哪些？
  - 选择器：元素选择器，id 选择器，类选择器， \*通配符选择器，后代选择器 -伪类选择器 `a:link|visited|hover|active`|
