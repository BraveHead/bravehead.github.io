# 什么是Path?什么是路径动画

- **path**: path元素是用来定义形状的通用元素。所有的基本形状都可以用path元素来创建。
- **路径动画：** 顾名思义沿着某一条特定的路径实现动画。



# 路径动画的常用实现方法：

- **用svg实现**： **可缩放矢量图形**（**Scalable Vector Graphics，SVG**），是一种用于描述基于二维的[矢量图形](https://zh.wikipedia.org/wiki/矢量图形)的，基于 [XML](https://developer.mozilla.org/zh-CN/docs/XML_介绍) 的标记语言。本质上，SVG 相对于图像，就好比 [HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML) 相对于文本。
- 基于canvas实现： Canvas是HTML的一个元素，通常被用来通过脚本绘制图形。其中绘制图形，保存的也是path的路径数据。



# [Paperjs](http://paperjs.org)中的path操作：

```typescript
const p =  new Path.Line(new Point(100, 100), new Point(150, 150));
p.lineTo(200, 100);
p.strokeColor = 'red';
p.strokeWidth = 1;  // 效果如下图所示 是一个折线
// 现在我们想画一个小球  让小球沿着这个路径去移动
// 先画一个小球
var b = new Path.Circle(new Point(100, 100), 4);
b.fillColor = 'blue';
// path是有长度的 也是按照px计算长度
var offset = 0;
var length = p.length;

// 只需要在动画的帧函数上动态获取路径上的点 然后赋值给小球 就可以完成动画
p.onFrame = () => {
   offset+= 1;
   if(offset > length) {
       offset = 0;
   }
   b.position = p.getPointAt(offset);
}






```

![te](E:\个人博客\bravehead.github.io\image\te.gif)