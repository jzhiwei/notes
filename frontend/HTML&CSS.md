# HTML & CSS

- 伪类

    是存在于浏览器后台中的类，由浏览器来维护，设置伪类后浏览器会把符合的元素添加到伪类中

- line-height

    当使用百分比或 em 为单位设置，子元素中的行高是相对于父元素字体大小来计算的

    如果使用数字 1 表示子元素的行高是相对于本身的字体大小来计算

- margin 

    如果两个元素**垂直外边距**碰到一起，就会折叠

    - 浏览器并排放置两个内联元素时，会累加两个元素的外边距

    - 浏览器上下放置两个块元素时，会把外边距折叠在一起，折叠的外边距高度就是最大的外边距高度

    - 设置为浮动或绝对定位的元素垂直外边距不会折叠

    - 一个元素嵌套在另一个元素中垂直外边距也会重叠。如果外元素有一个边框，那么两个元素的外边距就不会碰到一起，这样就不会折叠
    

- float

    - 为元素设置浮动最好要设置元素宽度
    - 浮动的元素会脱离文档流
    - 浮动的元素会 block 化，但是元素的宽度与内容一致，不会沾满整行
    - 浮动的元素会去空格
    - 块级元素会忽略浮动元素，直接穿过。而块级元素中的内联元素会考虑浮动元素的边界，绕着浮动元素流动
    - 子元素浮动会导致父元素高度塌陷，使用CSS清除浮动的效果可以避免此类情况

            parent::after {
                content: '';
                display: table;
                clear: both;
            }

- position

    定位的元素都有一个 z-index 属性，指定虚拟z轴的位置（层级关系），属性值越大层级越高。

    - absolute

        - 绝对定位的元素会脱离文档流
        - 文档流中的所有元素都会忽略绝对定位元素（包括块级元素中的内联元素）
        - 绝对定位元素的位置是相对于页面
        - 绝对定位元素可以不设置宽度
        - 父元素设置为 absolute 后，所包含的块级元素宽度与最宽的子元素宽度一致
        - 绝对定位后的元素宽度与子元素中的内容一致

    
- layout

    - jello

        凝胶布局，介于流体布局和冻结布局之间。

        锁定页面中内容区的宽度，在浏览器居中显示

    - CSS table 

        通过 CSS 创建一种表格的结构，通过属性
        
          display: table        设置表格
          display: table-row    设置表格行
          display: table-cell   设置单元格