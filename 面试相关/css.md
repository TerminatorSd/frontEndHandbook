# Knowledge of css


> ### 天生inline-block 元素
- \<input>、\<img>、\<button>、\<textarea>、\<label>
> ### 常见的行内及块级元素
- 块级元素：div、p、h1、form、ul、li
- 行内元素：span、a、label、input、img、strong、em
> ### rgba()和opacity的透明效果的区别
- opacity 默认继承
- rgba() 默认不继承
- IE9 以下都不支持

> ### px、em、rem 的区别
- px 为固定长度单位
- em 为父元素的font-size 大小
- rem 为根元素的font-size 大小

> ### reset css 和normalize.css
- reset css 是指我们为了消除浏览器默认样式而在项目中引入的全局css
- normalize.css 是reset css 的一种，它提供了一套合理的默认样式值

> ### Css 盒模型
- Css 盒模型分为两种：IE 盒模型和W3C 盒模型，两者的区别在于IE 盒模型的content 包含了padding 和border，而W3C 的content 不包含padding 和border
- 使用doctype 声明可以让浏览器以标准模式（W3C）解释盒模型
- Css3 新增box-sizing 属性，开发者可以通过这个来控制盒模型的表现

> ### Css3 新特性
- 阴影、圆角边框、边框图片、backgound 新属性、渐变、transform、过渡、动画、多列布局、媒体查询等，下面这个链接总结的很详细
- https://segmentfault.com/a/1190000010780991#articleHeader41

> ### Css 引入方式link 和@import 的区别
- link 是html 的标签 ，而@import 是css 的标签，link除了调用css外还可以有其他作用譬如声明页面链接属性，声明目录，rss等
- link支持使用Javascript控制DOM去改变样式；而@import不支持
- link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持
- 当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，而@import引用的CSS会等到页面全部被下载完再被加载。

> ### Css hack
- Css 定义p 标签，字体在IE6 下为黑色，IE7 下为红色，其他为绿色
```css
p {
    color: green;
    *color: red;
    _color: black;
}
```

> ### 关于层叠上下文
结合张鑫旭的《CSS 世界》来理解三个概念：层叠上下文、层叠水平、层叠顺序。
- 假设全国的学生要进行一个排名，每个学生的排名受两个因素影响：该学生所在的学校排名和他在自己学校里的排名。
    - 层叠顺序：全国的高校进行排名以后得到的一个排名结果就是层叠顺序
    - 层叠上下文：每一所高校都是一个层叠上下文
    - 层叠水平：一所高校中学生的排名就是层叠水平，层叠水平只在相同的高校内是有效的，跨高校是无效的，比如说华南理工大学的第50 名和清华大学的第100 名对比是无效的
    - 综上，排在最前面的元素应该是层叠顺序最靠前的层叠上下文中层叠水平最高的元素。
- 创建层叠上下文的方式
    - 页面根元素天生具有层叠上下文，称之为“根层叠上下文”
    - z-index值为数值的定位元素的传统层叠上下文
    - 其他CSS3属性(flex、opacity、transform 等）

> ### 关于块级格式化上下文（BFC）
##### (1) BFC 是什么？
全称是块级格式化上下文，相当于Css 的结界，结界内外互不干扰。
##### (2) 有什么用？
- 消除margin 合并
- 清除浮动
- 消除多列布局bug
##### (3) 怎么形成BFC？
- 根元素
- float属性不为none
- position为absolute或fixed
- display为inline-block, table-cell, table-caption, - flex, inline-flex
- overflow不为visible
##### (4) Ref
- https://mp.weixin.qq.com/s/msPO-fLlg6YqBUgE6xuYQw

##### (5) 问题
- float 为什么是bfc？

> ### 雪碧图的优缺点
- 优点：减少http 请求，调高页面加载速度，提升用户体验
- 缺点：
    - 宽屏高分辨率下可能出现背景断裂
    - 制作和改动麻烦

> ### display: none 和visible: hidden 的区别
- display: none 不占据物理空间
- display: none 会影响网站SEO

> ### 浏览器是怎样解析CSS选择器的？
- 按选择器从右向左遍历dom 数，如果某条路径符合选择器结构则加入结果集
- 为何要从右向左遍历：一开始可以筛掉尽可能多的无关元素，且需遍历的情况更少

> ### 关于flex 布局
一维弹性布局规则，还是要动手去写，附阮一峰老师的两篇参考文章
- http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html
- http://www.ruanyifeng.com/blog/2015/07/flex-examples.html

> ### 兼容retina 屏幕相关技术
- retina 屏幕的设备像素比是正常屏幕的两倍，正常屏幕下一个css 像素对应一个物理像素，但是retina 屏幕下一个css 像素对应两个物理像素，所以如果将正常的图片放在retina 屏幕下显示，一个像素可能要被放大四倍，导致图片发生轻微失真
- 解决办法是开发时准备正常图片和@2x 图两种图片，通过js 或者image-set 或者@media 查询来选择性地加载不同的图片

> ### css 选择器优先级
- 内置style 属性
- id 选择器
- 类、伪类和属性选择器
- 标签选择器和伪元素

> ### BEM
- BEM 是为了解决CSS 全局影响的方案，也可以看做是一种模块化的手段
- 其规则是通过添加模块名的方式来限制CSS 的作用域，实现模块化管理
- BEM 命名规则：block-name__element-name--modifier-name，也就是模块名 + 元素名 + 修饰器名
- BEM 的缺点是命名过长，工作了较大，webpack 中的css-loader 解决了这个问题，也是通过给选择器添加唯一标志的方式

> ### Css 优化手段
- 内联首屏css
- 异步加载非首屏css
    - Js动态插入
    - Media 属性设置为不匹配的媒体类型，文件加载完后需要时则设置回来
    - Rel 属性标记为可选样式表
    - Rel = preload
- 文件压缩
- 去除无用css
- 选择器使用最佳实践：少嵌套、尽量避免给通配符
- 减少重绘与重排操作
- 不要使用@import 

> ### 怎么看待float？如何清除
- Web 诞生之初，float 的本质是为了实现文字环绕效果，float 属性让父元素高度塌陷也是因为这个
- 如今，也会用来实现各种布局，但是此时float 引起的高度塌陷却成了需要克服的问题
- 常用的清除浮动方式
    - 可以使用clear both 进行清除，但是clear 属性是只有块级元素才有，所以还需要给要清楚的元素的前后伪元素设置display 属性
    - 父元素设置overflow: hidden
