

## flutter开发

### 一、环境安装

教程：http://t.csdnimg.cn/KZWW3

flutter SDK：http://t.csdnimg.cn/KZWW3

Android studio：https://developer.android.com/studio 

你的第一个flutter app： https://codelabs.developers.google.com/codelabs/flutter-codelab-first#0

flutter油管视频教程：https://www.youtube.com/playlist?list=PL4cUxeGkcC9jLYyp2Aoh6hcWuxFDX6PBJ

flutter组件学习利器：https://github.com/toly1994328/FlutterUnit



### 二、Dart语法

博客笔记：http://t.csdnimg.cn/q0eX4

该视频的代码：https://github.com/iamshaunjp/flutter-beginners-tutorial/tree/master

分支序号对应视频序号

![image-20231116111348474](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116111348474.png)

### 三、部件

#### 1、认识部件（首字母大写，并且每个小括号后面要有逗号）

```
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(      // 'Scaffold' 实现了基本的 Material Design 可视化布局结构, 提供了用于显示drawer、snackbar和底部sheet的API
  home: Home(),
));

// 'home' 用于指定进入应用程序后显示的第一个页面，即用来定义当前应用程序打开时所显示的界面。该属性值为Widget类型
```

```
class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold( 
    // 'Scaffold' 实现了基本的 Material Design 可视化布局结构, 提供了用于显示drawer、snackbar和底部sheet的API                        
      appBar: AppBar(                        
      // 'AppBar' 决定顶部属性栏外观, AppBar 内可以指定属性
      )
      
      body:
      //'body'属性决定的是屏幕主体部分的内容，就是应用栏下的任何内容都是body实现的
      
      
      floatingActionButton: FloatingActionButton(       
      // 'FloatingActionButton' 是一个悬浮在屏幕上方的按钮，常用于设置评论区
        onPressed: () {},                               
        // 没有'onPressed:() {},'回调， 会报错（炸裂，教程没加怎么不会报错？？？坑了好多时间）
        child: Text('click'),
        backgroundColor: Colors.red[600],               
        // 调颜色参数来源: https://m2.material.io/design/color/the-color-system.html#tools-for-picking-colors
      ),
    );
```

//AppBar的效果，作用于应用栏

![image-20231104195551095](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104195551095.png)

//body的作用于屏幕主体部分

![image-20231104195744869](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104195744869.png)

//floatingActionButton: FloatingActionButton()设置一个悬浮操作的按钮

![image-20231104200023491](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104200023491.png)

更多的组件内容：Scaffold class：https://api.flutter.dev/flutter/material/Scaffold-class.html



#### 2、颜色与字体

##### 2.1 颜色Color

```
// 调颜色参数来源: https://m2.material.io/design/color/the-color-system.html#tools-for-picking-colors
```

backgroundColor：Colors.red[600]//选择颜色

##### 2.2 字体Fonts

```
child: Text(                      // 'text' 放在 'Center' 而不是直接放在 'body', 使得内容集中嵌套在内部中心（不然很丑）
  'hello ninjas',
  style: TextStyle(
    fontSize: 20.0,               // 字体大小
    fontWeight: FontWeight.bold,  // 字体粗细
    letterSpacing: 2.0,           // 字母间距
    color: Colors.grey[600],      // 字体颜色
    fontFamily: 'IndieFlower',    // 字体形式，调用新字体前要现在 pubspec.yaml 指定，详见末尾注释
  ),
),
```



1、转化字体需要先到: https://fonts.google.com/specimen/Indie+Flower?query=indie+flo 下载目标字体的压缩包
2、将 ttf 文件拖拽到 fonts 文件夹中（自己创建），在 pubspec.yaml 中告诉 flutter 可以用新字体了
3、pubspec.yaml 有点像项目的配置文件，可以在 pubspec.yaml 中指定环境、依赖项或我们想在项目中使用的任何 asset 和 fonts
4、pubspec.yaml 格式严格，包括缩进等，稍有不同都会导致字体更改失败，且不会报错（手动打爆这一步，坑了太多时间）
5、找到 fonts, 先取消注释，调整格式。
6、删掉不需要的。起码留下 fonts 里面第一行的 ==family 一边修改字体==；留下==第一个 asset 放新字体的地址==
7、回到 main.dart 后，自动显示pubspec有变化，点击获取依赖项，最后在代码中指定字体即可

![image-20231104215009762](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104215009762.png)

![image-20231104215110893](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104215110893.png)

#### 3、无状态小部件和热重载

无状态小部件：不会随着时间的推移而改变，例如布局、颜色

状态小部件：包含可以随着时间的推移而改变的

根据设计的要求选择有无状态小部件

设计无状态小部件

```
class Home extends StatelessWidget {//定义了一个Home的无状态小部件，然后上面的main只需要返回这个就可以了，帮助热重载
  @override
  Widget build(BuildContext context) {//这个部分就是更新热重载的
    return Scaffold(
    
    );//内容嵌在这里面
    }
    }
```



```
void main() => runApp(MaterialApp(      // 'Scaffold' 实现了基本的 Material Design 可视化布局结构, 提供了用于显示drawer、snackbar和底部sheet的API
  home: Home(),
));
```

这样的写法有点相当于函数，可以提供我们重复使用一个东西。



#### 4、图像image和快捷方式Assets

##### 4.1图像

```

body:Center(
child: Image(
  调用网络照片，就是要复制图片的连接URL，
  image:NetworkImage('https://www.bing.com/th?id=OIP.YavLB3rCtQSn2U1IJBbJugAAAA&w=155&h=150&c=8&rs=1&qlt=90&o=6&dpr=1.5&pid=3.1&rm=2')
  调用本地图像前要先设置 pubspec.yaml
  image: AssetImage('assets/dog-1.jpg'),   
  // NetworkImage('') 中可以放链接
  //Assetimage('') 则放本地URL
)
)

// 使用AssetImage 同样需要在 pubspec.yaml 进行设置
// 如果使用某文件夹内的多个图像，只需要声明 folder 的名字（记得在 folder 名字后面加斜杆 '/' ）

```

![image-20231104221610587](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104221610587.png)



##### 4.2 图像快捷方式

```
// 调用图像的简便写法
child: Image.asset('assets/dog-1.jpg'),
child: Image.network('https://www.bing.com/th?id=OIP.YavLB3rCtQSn2U1IJB
```



#### 5、Icons图标和Button按钮

##### 5.1 Icons图标

```
body:Center(
child: Icon(                      // Icons 内置全套 material 图标
   Icons.local_airport,
   color: Colors.lightBlue,       //设计图标的颜色
   size: 50.0,                    //设计大小
 ),//加入小图标的
 )
```

![image-20231104222433503](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104222433503.png)



当我们输入Icons.就会出现，各种各样的选择，它的右边会有相应的图标样式，可以找到对应想要是设计的样式。

![image-20231104222142581](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104222142581.png)



##### 5.2Buttons按钮

###### 5.2.1单纯的文字按钮

按钮就是可以点击，点击之后会return的，这个部分是需要连接后端的

```
child: TextButton(
  onPressed: () {
    print('you clicked me');//这个onPressed是管理返回的，就是点击之后，会向控制台返回什么一样。
  },
  child: Text('click me'),//这个是Button里面再嵌套一个child，实现设计按钮的子部件   
  // color: Colors.lightBlue,        // 部分参数被弃用了，比如 color
  style: ElevatedButton.styleFrom( primary: Colors.lightBlue), // 设置按钮的背景色
),
//1、ElevatedButton是凸起按钮，像浮在面板上，有阴影和3D效果
//2、TextButton是平面按钮
//3、OutlinedButton

// FlatButton, RaisedButton, and OutlineButton 这三个 widget 已经有了新的控件替代，分别是TextButton, ElevatedButton, and OutlinedButton
```

![image-20231104223730232](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104223730232.png)

###### 5.2.2带有图标的按钮

```
child: ElevatedButton.icon(
  onPressed: () {
    print('you clicked me');//这个是点击按钮后的返回
  },
  icon: Icon(
    Icons.mail
  ),//Icons设计图标
  label: Text('mail me'),//在图标隔壁再设计一个文本
  style: ElevatedButton.styleFrom( primary: Colors.amber),//设计颜色
)
```

![image-20231104224038951](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104224038951.png)

5.2.3 图标按钮，但不带边框

```
child: IconButton(
  onPressed: () {
    print('you clicked me');
  },
  icon: Icon(Icons.alternate_email),//这个展示，@符号
  color: Colors.amber,
),
```

![image-20231104224240396](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104224240396.png)







### 四、布局

#### 1、Containers容器和Padding填充

```
body: Container(    //container是容器
  //填充
  //padding:EdgeInsets.all(20.0)， //如果是all就是在整个填充，
  padding:EdgeInsets.fromLTRB(10.0,20.0,30.0,40.0),//left，top,right,bottom
  margin:EdgeInsets.all(30.0),
  //Padding是实现填充东西
  //而margin是实现让容器和周围保持距离
  color:Colors.grey[400],//如果是仅仅只有这句话，那么灰色会覆盖整个页面，加上了子部件，之后，容器就之后覆盖子容器的大小，但这样往往又不好，所以就有了padding填充
  child:Text('hello'),
),
```

![image-20231104225927085](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104225927085.png)

![image-20231104225328829](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104225328829.png)

1、symmetric就是中心对称式，如果你需要的上下左右对称的就可以选择这个

2、fromLTRB是可以自定义四个方向的填充的大小

3、all就是四个方向都采用同一个值的填充





在小部件的时候，也是可以使用padding来设置相应的位置信息的

```
body:Padding(
  padding:EdgeInsets.all(90.0),
  child:Text('hello'),
),
```

![image-20231104230125223](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231104230125223.png)



#### 2、Row行

##### 2.1行属性

行本来就是一个小部件，实现在一行中连续放置小部件

```
body:Row(//在行上连续放置小部件
  children:<Widget>[//<Widget>[] 相当于 List列表，该列表中应包含一些 Widget 元素，实现在 Row 中排列。
    Text('hello world'),
    TextButton(
      onPressed:(){},
      child:Text('click me')
    ),
    Container(
      color:Colors.cyan,
      padding:EdgeInsets.all(30.0),
      child: Text('inside container')
    )
  ],
),
```

![image-20231105092446972](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105092446972.png)



##### 2.2行布局

 摘要在这个 Flutter 初学者教程的第11集中，我们学到了如何使用行（Rows）来扩展我们应用的布局，使得页面上可以容纳多个不同的小部件。通过使用行和列的组合，我们能够更灵活地排列页面上的小部件。

 亮点

📋 我们学到了如何使用行（Rows）来容纳多个小部件，通过 `children` 属性可以将多个小部件组织在一起。

 🚀 通过添加文本小部件、按钮小部件和容器小部件，我们展示了如何在行内包含不同类型的小部件。

🔄 使用 `mainAxisAlignment` 属性，我们可以在主轴上控制小部件的对齐方式，例如居中、起始、结束或均匀分布

 ↕️ 通过 `crossAxisAlignment` 属性，我们可以控制小部件在交叉轴上的对齐方式，例如拉伸、居中或放置在开始或结束位置。

🌐 我们比较了主轴和交叉轴的概念，以及如何使用不同的属性值来调整小部件在行内的布局。

📐 我们演示了如何使用行和列，这是一种在 Flutter 中灵活布局的方式，类似于在Web中使用CSS

实现位置布局的调整。

![image-20231105092621107](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105092621107.png)

###### 2.2.1 mainAxisAlignment实现在主轴（main axis）的布局

```
mainAxisAlignment：MainAxisAlignment.     //控制主轴对齐main axis布局属性
```

![image-20231105092708392](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105092708392.png)

根据其中的英文可以得到相对应的布局信息。

1)、center就是小部件聚在中间，左右间隔一致

![image-20231105093216077](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105093216077.png)

2)、spaceBetween小部件之间保持距离，左右小部件是紧靠边缘的

![image-20231105093251250](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105093251250.png)

3)、spaceEvenly小部件距离均匀分布，

![image-20231105093416822](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105093416822.png)

4)、end全部紧靠右边

![image-20231105093457342](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105093457342.png)

5)、start全部紧靠左边

6)、spaceAround实现左右都有空间，而且部件之间也有空间。小部件之间的距离是边缘的两倍。

![image-20231105093706395](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105093706395.png)





###### 2.2.2 crossAxisAlignment实现在交叉轴上的布局

```
crossAxisAlignment: CrossAxisAlignment.    //实现在交叉轴上的布局
```

![image-20231105095256001](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105095256001.png)

1）、stretch拉伸到全部可用空间的整个高度。

![image-20231105095345839](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105095345839.png)

2)、center中心，就是默认值

![image-20231105095442443](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105095442443.png)

3)、start，有点像个阶梯式的布局

![image-20231105095542108](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105095542108.png)

4)、end，另一个方向的阶梯

![image-20231105095644448](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105095644448.png)



#### 3、Columns列

 摘要在这个视频中，作者展示了如何使用Flutter中的列（Columns）来垂直堆叠不同的小部件，与之前的水平排列相反。通过演示使用列（Columns）的基本语法，以及如何在列中使用主轴对齐和交叉轴对齐来控制小部件的布局。

 亮点

📋 展示如何使用Flutter的列（Columns）小部件垂直排列其他小部件。

🌈 创建了三个不同颜色和大小的容器，演示了列中的小部件堆叠效果

 🔄 介绍了如何使用主轴对齐（main axis alignment）来控制列中小部件的垂直对齐方式。

↔ 演示了如何使用交叉轴对齐（cross axis alignment）来控制列中小部件的水平对齐方式。

 ➕ 展示了如何在列中嵌套行（Row）以创建更复杂的布局。

🛠 提示通过调整不同的对齐方式和布局，可以灵活地创建各种界面。

🔄 鼓励观众在实践中尝试不同的布局和对齐方式，以加深对Flutter中列和行的理解。



和row的写法格式差不多，就是形式上由行变成了列。mainAxisAlignment和crossAxisAlignment的使用方式和效果和row的一样。

```
//Column行部件
body: Column(
  mainAxisAlignment: MainAxisAlignment.end,
  crossAxisAlignment: CrossAxisAlignment.end,
  children: <Widget>[
    Container(
      padding: EdgeInsets.all(20.0), // 设置容器内边距为30.0像素
      color: Colors.cyan, // 设置容器的背景颜色为粉红色
      child: Text('one'), // 在容器内放置一个文本控件，显示文本“two”
    ),
    Container(
      padding: EdgeInsets.all(30.0), // 设置容器内边距为30.0像素
      color: Colors.pinkAccent, // 设置容器的背景颜色为粉红色
      child: Text('two'), // 在容器内放置一个文本控件，显示文本“two”
    ),
    Container(
      padding: EdgeInsets.all(40.0), // 设置容器内边距为40.0像素
      color: Colors.amber, // 设置容器的背景颜色为琥珀色
      child: Text('three'), // 在容器内放置一个文本控件，显示文本“three”
    ),
  ],
),
```

![image-20231105100731963](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105100731963.png)





使用crossAxisAlignment: CrossAxisAlignment.end、crossAxisAlignment: CrossAxisAlignment. stretch可以实现对底部的设计。



![image-20231105100921058](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105100921058.png)



#### 4、shortcuts快捷方式&Flutter outline



###### 4.1shortcuts快捷方式

    //快捷方式，把鼠标悬浮在小部件名字上，点击左边的小灯泡，可以选择一些转换方式
    //还有就是最右边的outline，快捷方式

![image-20231105101202830](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105101202830.png)

1）、add padding添加填充

2）、move widget down移动这个部件向下

3）wrap with……表示变换成其他的部件

……

###### 4.2Flutter outline这个有点像是目录的，展示部件和子属性的布局

![image-20231105102041839](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105102041839.png)



#### 5、Expanded Widgets扩展小部件（实现扩展所有空白的地方，不留空白，和CSS的flexbos很像）

摘要在这个Flutter初学者教程中，我们介绍了扩展小部件（Expanded Widgets），这是一种用于布局屏幕内容的方法。与Web开发中的Flexbox相似，扩展小部件允许我们在行中的多个容器之间平均分配可用空间。此外，我们还了解了如何使用`flex`属性来控制每个扩展小部件所占的宽度比例。

亮点

📦 **容器和行列：** 已经学习了如何使用容器、行和列来布局屏幕上的内容。

🌐 **灵活布局：** 扩展小部件的使用方式类似于Web开发中的Flexbox，能够灵活地分配可用空间。

📏 **`flex`属性：** 通过为扩展小部件添加`flex`属性，我们可以精确控制它们在行中所占的宽度比例。

 🌈 **多个容器：** 演示了如何将多个容器放置在一行中，并使用扩展小部件使它们平均分配宽度。

🖼️ **包含图像：** 使用扩展小部件可以有效地将大图像限制在屏幕范围内，确保不会超出或遮挡其他内容。 

🚀 **简化布局：** 扩展小部件为简化布局提供了强大的工具，特别是在处理多个子元素时。-

###### 5.1扩展小部件

```
body:Row(
  children:<Widget>[
    Expanded(
    //flex:3,
      child: Container(
        padding:EdgeInsets.all(30.0),
        color:Colors.cyan,
        child:Text('1'),
      ),
    ),
    Expanded(
    //flex:2,
      child: Container(
        padding:EdgeInsets.all(30.0),
        color:Colors.pinkAccent,
        child:Text('2'),
      ),
    ),
    Expanded(
    //flex:1,
      child: Container(
        padding:EdgeInsets.all(30.0),
        color:Colors.amber,
        child:Text('3'),
      ),
    ),
  ],
),
//把container套在Expanded widget里面，实现小部件扩展
```

![image-20231105102907274](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105102907274.png)

然后，在每一个Expanded里面加上一个flex:数字 实现定制每个小部件的扩展的大小,数字除以数字之和得出所占多少分之多少。例如，上面的3+2+1，第一个展2分之1.

```
Expanded(
  flex:3,
  ……
```

![image-20231105103133258](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105103133258.png)



###### 5.2将扩展用到图像上

```
body:Row(
  children:<Widget>[
    Image.asset('assets/图片1.jpeg'),
    //因为往往直接添加图片会影响到其他的部件，所以我们要通过expanded来调整大小
```

![image-20231105104229263](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105104229263.png)



给图片加入扩展

```
Expanded(
    child: Image.asset('assets/图片2.jpeg'),
  flex: 1,
),
```

![image-20231105104330418](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105104330418.png)









### 五、实战，开发一个Card名片

#### 1、首先是框架的构建

```
import 'package:flutter/material.dart';

void main() =>runApp(MaterialApp(
  home: NinjaCard(),
));

//输入stless即出class
class NinjaCard extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
    );
  }
}
//基本框架
```



#### 2、应用栏设计

```
appBar: AppBar(
  title: Text('Ninja ID Card'),
  centerTitle: true,//把题目放到中间
  backgroundColor: Colors.grey[850],//设置应用栏颜色
  elevation: 0.0,//控制应用栏于屏幕主体的阴影部分，0.0设置成没有阴影，使屏幕平坦
),
```

![image-20231105111628917](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105111628917.png)

#### 3、主体部分设计

##### 3.1主体背景颜色

```
return Scaffold(
  backgroundColor: Colors.grey[900],
```

![image-20231105112112764](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105112112764.png)

##### 3.2文字部分

```
body: Padding(
  padding: EdgeInsets.fromLTRB(30.0, 40.0, 30.0, 0.0),
  child: Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: <Widget>[
      Text(
          'NAME',
        style: TextStyle(
          color: Colors.grey,
          letterSpacing: 2.0,//蛇酒字与字之间间隔的，两个像素
        )
      ),
      //因为两个字离的太近了，所以要制作一个空盒子来分开两者
      SizedBox(height: 10.0),//空盒子
      Text(
          'HMark',
          style: TextStyle(
            color: Colors.amberAccent[200],
            letterSpacing: 2.0,//蛇酒字与字之间间隔的，两个像素
            fontSize: 28.0,//设计字体大小
            fontWeight: FontWeight.bold,//设计字体粗细
          )
      ),
      SizedBox(height: 30.0),//空盒子
      
    ],
  ),
),
```

![image-20231105113334034](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105113334034.png)



##### 3.3实现邮箱

```
//实现邮箱标志
Row(
  children: <Widget>[
    Icon(
      Icons.email,
      color:Colors.grey[400],
    ),
    SizedBox(width:10.0),//设计一个宽度为10的空盒子
    Text(
      'HMark@theninja.com',
        style: TextStyle(
          color: Colors.grey[400],
          letterSpacing: 1.0,//蛇酒字与字之间间隔的，两个像素
          fontSize: 18.0,//设计字体大小
        )
    )
  ],
)
```

![image-20231105114502671](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105114502671.png)



##### 3.4添加头像

```
//添加图片头像
CircleAvatar(//CircleAvatar是圆形图片框
  backgroundImage:AssetImage('assets/图片2.jpeg') ,
  radius:40.0,//设置图片框大小
),
```

![image-20231105115439359](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105115439359.png)



把头像放到中间，就把其放到center里面

```
//添加图片头像
Center(
  child: CircleAvatar(//CircleAvatar是圆形图片框
    backgroundImage:AssetImage('assets/图片2.jpeg') ,
    radius:40.0,//设置图片框大小
  ),
),
```

![image-20231105115544297](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105115544297.png)



##### 3.5分隔器小部件Divider

在头像和其余内容之间放置某种分隔符

```
//添加图片头像
Center(
  child: CircleAvatar(//CircleAvatar是圆形图片框
    backgroundImage:AssetImage('assets/图片2.jpeg') ,
    radius:40.0,//设置图片框大小
  ),
),

Divider(
  height: 60.0,//部件的大小高度
  color: Colors.grey[800],//部件的颜色
),
```

![image-20231105115936956](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105115936956.png)



##### 3.6悬浮按钮floatingActionButton

```
floatingActionButton: FloatingActionButton(
  // 'FloatingActionButton' 是一个悬浮在屏幕上方的按钮，常用于设置评论区
  onPressed: () {},
  // 没有'onPressed:() {},'回调， 会报错（炸裂，教程没加怎么不会报错？？？坑了好多时间）
  child: Text('click'),
  backgroundColor: Colors.red[600],
),
```



##### 整体效果

![image-20231105120725412](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231105120725412.png)





上面学的都是无状态小组件，它们是不包含任何随时间二发生变化的数据状态。





### 六、有状态State小部件

摘要

在本教程中，介绍了Flutter中的Stateful Widgets的基本概念和用法。通过创建一个简单的Stateful Widget，演示了如何在其中存储和更新动态数据，以及使用`setState`函数触发UI的更新。同时，展示了如何通过点击按钮改变应用中的数据状态。

 亮点

🧩 **Stateless Widget和Stateful Widget的区别：** Stateless Widget在创建后不会改变，而Stateful Widget可以随时间变化或包含动态数据。

🔄 **使用`setState`更新数据状态：** 通过`setState`函数，成功实现了在Stateful Widget中更新数据状态并刷新UI。

➕ **转换Stateless Widget为Stateful Widget：** 演示了将一个Stateless Widget转换为Stateful Widget的简便方法，以支持动态数据。

🖱️ **通过点击按钮改变数据状态：** 添加了一个Floating Action Button，点击按钮后通过`setState`函数增加了"Ninja Level"的值

 📋 **创建Stateful Widget的基本结构：** 展示了Stateful Widget的基本结构，包括State对象和build函数，以及如何在其中定义和更新数据。

输入stful点击，生成模版。

Test是这个新的状态小部件的名称

```
class Test extends StatefulWidget {//stateful是有状态小部件，这个是状态本身
  @override
  _TestState createState() => _TestState();//创建了这么一个函数，返回_TestState()，实例化了第二类
}

class _TestState extends State<Test> {//这个是状态对象

  int counter=1;//计数器
  //可以输出该计数器，当它发生变化时，它将重建这个小部件树，并且更新计数器，更新位置

  @override
  Widget build(BuildContext context) {//包含对象并返回这个小部件树
    return const Placeholder();
  }
}
```



###### 将无状态组件转变成有状态的方法

1、首先先把类改一下，点击小灯泡，选择stateful

![image-20231108192105550](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231108192105550.png)

下面的类就会发生相应的改变

![image-20231108193615238](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231108193615238.png)

2、然后创建一个状态数据 ，如上图的int ninjaLevel

3、创建一个按钮，实现动态，在这个按钮的onPressed里面加上setState((){在这里面放怎么改变状态数据的逻辑关系})

![image-20231108193726433](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231108193726433.png)

所以说，上面最重要的就是setState这个状态改变函数



#### 2、Lists of Data列表数据

```
List<String>quotes=[
  'Be yourself ;everyine else is already taken',
  'I have nothing to declare except my genius',
  'The trueh is rarely pure and never simple'
];
```

```
body:Column(
  children: quotes.map((quote)=>Text(quote)).toList(),
```



#### 3、定义类，使用类

创建自定义类来关联引用和作者，以及如何使用命名参数和类构造函数。通过创建自定义类，可以将引用和作者属性关联在一起，并且可以轻松地输出不同对象的属性。同时，还介绍了如何在文本小部件中输出对象的属性。

摘要

在本教程中，学习如何创建自定义类以关联每个引用与其作者，并使用命名参数来初始化对象。这将帮助我们更好地组织和管理数据。

亮点

- 📝 创建自定义引用类，包括引用文本和作者。
- 🤖 使用命名参数初始化对象，允许更灵活的属性顺序。
- 📋 通过引用类属性输出引用文本和作者。



其中创建了一个类文件quote.dart。用来定义类

```
class Quote {
  String text;
  String author;

  Quote({required this.text, required this.author}); // 使用 "required" 来确保参数不为 null
  //构造函数Quote被定义为接受两个必需参数：text和author。使用required关键字来标记这两个参数，这意味着在创建Quote对象时，你必须为这两个参数提供值，而不能将它们设置为null。
}
//记住类上基本上是对象类型或数据类型的定义，他将描述数据存储的函数的哪些属性
//因此类是描述和创建对象的一种方式
//Quote myquote=Quote(author:'oscar wilde',text:'this is the qite text');


//类的作用
//当你创建一个新的Quote对象时，你可以为text和author属性提供相应的值，然后使用这个对象来表示引用的信息。这有助于在你的应用程序中组织和管理引用数据。

```



#### 4、list列表的使用

 摘要本教程介绍了Flutter初学者教程的第17部分，主题是如何循环遍历数据列表并在小部件中动态输出该数据列表。教程创建了一个名为“quotes”的新项目，演示了如何使用StatefulWidget来处理具有变化数据的小部件。通过使用`map`函数，教程展示了如何轻松地循环遍历数据列表并输出相应的小部件。

#亮点

📱 创建名为“quotes”的Flutter项目，用于展示如何处理数据列表。

🔄 使用StatefulWidget处理具有变化数据的小部件。

🎨 使用Scaffold小部件创建应用程序的基本结构，包括AppBar和Body。

📋 使用`map`函数循环遍历数据列表。

🧑‍💻 利用`map`函数和Text小部件动态输出每个列表项的文本

 🎉 展示了通过`map`函数将数据列表转换为小部件列表的简洁方法。

 🚀 强调了灵活性，使得在未来处理更多数据项时更容易扩展。



```
List<Quote> quotes = [
  Quote(author: 'HMark', text: 'Be yourself; everyone else is already taken'),
  Quote(author: 'HMark', text: 'Be yourself; everyone else is already taken'),
  Quote(author: 'HMark', text: 'Be yourself; everyone else is already taken'),
];
//创建了一个名为 quotes 的列表，其中包含了三个 Quote 对象。
//这段代码的作用是创建了一个包含三个引用的列表，每个引用都由 author 和 text 组成。这使得你可以在你的应用程序中轻松管理和显示这些引用，例如在用户界面中显示引用列表。这有助于组织和展示引用数据。
```

list列表内容展示

```
children: 
quotes.map((quote) => Text('${quote.text} - ${quote.author}')).toList(),
//这段代码是在使用Flutter构建用户界面的部分，特别是在QuoteList类中的build方法中。它是用来创建一个包含引用文本和作者的文本小部件列表，并将这些小部件添加到Column小部件的children属性中。
具体来说，这行代码执行以下操作：
quotes.map((quote) => Text('${quote.text} - ${quote.author}'))：这部分使用map函数对quotes列表中的每个Quote对象执行操作。对于每个quote对象，它创建一个Text小部件，文本内容为${quote.text} - ${quote.author}，这里使用${}来将引用的文本和作者的值插入到文本字符串中。

.toList()：map函数返回一个可迭代对象，但children属性需要一个List<Widget>。因此，.toList()将map的结果转换为小部件列表。

最终，这个小部件列表作为Column小部件的children属性，用于在用户界面中显示引用的文本和作者。每个引用都会以文本的形式显示在Column中，一个引用占据一行。
```



![image-20231110113349621](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110113349621.png)



#### 5、自定义quote类

摘要

在17节课中，我们学习了如何创建自定义类以关联名言与作者，并使用命名参数和类构造函数。这有助于将数据更模块化和提高代码的可维护性。

亮点📝 创建自定义类 Quote 用于存储名言和作者信息。

🔄 使用类构造函数，通过命名参数指定属性值，提高数据输入的灵活性。

🖼️ 输出名言和作者信息，展示如何访问自定义类的属性。注意：请确保在实际使用中添加所需的导入语句和代码结构。



#### 6、Card卡片

摘要

在本教程中，作者介绍了如何使用Flutter创建卡片视图来显示引用文本和作者信息。他首先创建了一个函数，用于生成每个引用的卡片，然后使用此函数在列表中为每个引用创建卡片。作者还讨论了如何添加卡片的外边距和设置文本样式，以使卡片看起来更好。

亮点

[📝] 创建一个函数来生成引用卡片。

[📐] 添加卡片的外边距和文本样式。

[🔳] 使用卡片视图来显示引用文本和作者信息。

[👩‍💻] 讨论了更有效地生成卡片的方法。



上文中的把作者属性还有内容属性放在单个文本的小部件，看起来有点粗糙

所以这里学习卡片更好的模版。

https://api.flutter.dev/flutter/material/Card-class.html

使用卡牌呢小部件返回某种引号模板

创建一个函数，有一个返回类型，他将是一个小部件，然后保存函数名称，该函数名称将成为引用模版，然后我们将接受单个引号，所以基本上我们将在映射此列表是为每个引用调用此函数，把引号传递到函数中，根据引号返回一个小部件树，这样就可以在模板内输出该引号的数据。

然后需要在这里返回我们的内容，我们要做的就是返回一个卡片小部件，以此创建一张卡片，

```
Widget quoteTemplate (quote)//这是一个函数声明定义，接受quote的参数
{
  return Card(//函数返回Card小部件，Card是一个用于显示信息的材料设计小部件，通常用于包裹其他小部件以提供一个卡片效果
    margin: EdgeInsets.fromLTRB(16.0, 16.0, 16.0, 0.0),//设置了卡片的外边距
    //margin:EdgeInsets.fromLTRB(left, top, right, bottom)左顶右底
      child: Column(//行子部件 
        children: <Widget>[
          Text(
            quote.text,
            style: TextStyle(
              fontSize: 18.0,
              color: Colors.grey[600],
            )
          ),
          
          SizedBox(height: 0.0),//空白盒子
          //创建作者显示模块
          Text(
              quote.author,
              style: TextStyle(
                fontSize: 14.0,
                color: Colors.grey[800],
              )
          ),
        ],
      ),
    )
  );
```

```
//上面都是在定义函数和类，下面在scaffold中使用
children: quotes.map((quote) => quoteTemplate(quote)).toList(),
```

![image-20231110190131423](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110190131423.png)



![image-20231110190306041](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110190306041.png)

![image-20231110191340489](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110191340489.png)



上面我们学会了如何映射列表



#### 7、卡模板创建无状态小部件（快速方法）

 摘要在这个Flutter初学者教程中，我们学到了如何提取小部件（Extracting Widgets）以提高代码的模块性和可重用性。具体而言，我们通过创建一个自定义的无状态小部件（stateless widget）来表示卡片模板，将卡片模板从原始代码中提取出来，使得我们可以更轻松地在不同的上下文中重复使用它。

 亮点

 🔄 **提取小部件（Extracting Widgets）：** 通过创建自定义的无状态小部件，我们成功地将卡片模板从原始代码中提取出来，提高了代码的模块性和可重用性。

🚀 **优化代码结构：** 通过使用提取小部件的方法，我们避免了在原始函数中创建卡片模板的需要，使得代码更加清晰和高效。

 🔄 **参数传递：** 通过在新创建的自定义小部件中添加构造函数和参数传递，我们成功地将数据传递给卡片模板，增加了灵活性。

 📄 **文件模块化：** 将卡片模板的代码移动到独立的文件中，使得我们可以在将来的项目中轻松引入和重复使用这一模块化的代码。

🧩 **代码重构：** 通过删除冗余的函数调用，我们简化了代码，直接在映射函数内创建并返回了卡片模板的新实例。

🔄 **热重启：** 在进行模块化和重构后，通过热重启验证代码的有效性，确保所有更改都未引入错误。

📦 **导入模块：** 通过在主文件中导入新的模块文件，我们成功地将自定义小部件引入项目，实现了代码的更好组织和可维护性。

创建外部模版，使得程序更模式化

![image-20231110193252556](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110193252556.png)

封装成新的函数文件

![image-20231110195126743](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110195126743.png)

```
children: quotes.map((quote) => quoteCard(quote: quote)).toList(),
//调用的方式也改变了
```

```
import 'package:flutter/material.dart';
import 'quote.dart';

class quoteCard extends StatelessWidget {

  final Quote quote;

  quoteCard({ required this.quote });//// 使用 required 修饰符，表明 quote 参数为非空且必须提供

  @override
  Widget build(BuildContext context) {
    return Card(
        margin: EdgeInsets.fromLTRB(16.0, 16.0, 16.0, 0.0),
        child: Padding(
          padding: const EdgeInsets.all(12.0),//添加填充更好看
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Text(
                  quote.text,
                  style: TextStyle(
                    fontSize: 18.0,
                    color: Colors.grey[600],
                  )
              ),
              SizedBox(height: 0.0),//空白盒子
              //创建作者显示模块
              Text(
                  quote.author,
                  style: TextStyle(
                    fontSize: 14.0,
                    color: Colors.grey[800],
                  )
              ),
            ],
          ),
        )
    );
  }
}
```



#### 8、加入一个删除，实现动态删除部件

 摘要在这个 Flutter 初学者教程中，我们学到了如何将函数作为参数传递，以实现删除引用功能。通过在引用卡片中添加删除按钮，并使用函数参数来触发删除操作，我们成功地更新了用户界面。

 亮点- 🗑️ 为每个引用卡片添加了删除按钮。

📝 使用函数参数实现了点击删除按钮后删除引用的功能。

🧩 通过传递删除函数作为参数，解决了在无状态小部件中无法直接修改数据的问题。

🎨 使用 Flutter 的 `FlatButton` 和 `Icon` 小部件来创建删除按钮。

🔄 利用 `setState` 函数来更新用户界面并删除引用。

🛠️ 通过在删除函数中调用 `remove` 方法，从引用列表中移除特定引用

 🚀 探讨了如何将函数作为参数传递到其他小部件，为构建更复杂的 Flutter 应用铺平了道路。

```
 主函数需要改地方，在这个设计一个delete函数，实现删除quotes.remove(quote);
 
 body: Column(
      children: quotes.map((quote) => quoteCard(
          quote: quote,
          delete:(){
            setState(() {
              quotes.remove(quote);
            });
          }
      )
      ).toList(),
)
```

```
在card里面，传入参数

final Quote quote;
//final Function delete;
final VoidCallback delete;//因为delete没有返回，所以使用viodcallback，而不使用function
quoteCard({ required this.quote,required this.delete });
// 使用 required 修饰符，表明 quote 参数为非空且必须提供


//这是 quoteCard 类的构造函数。它接受两个必需的参数，分别是 quote 和 delete。使用 required 修饰符表示这两个参数是必需的，调用者在创建 quoteCard 对象时必须提供这两个参数。
```

```
//card函数加上删除小部件
SizedBox(height: 8.0),
TextButton.icon(
  onPressed:delete,
  label:Text("delete quote"),
  icon:Icon(Icons.delete),

)
```

![image-20231110202540255](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110202540255.png)





### 七、实战世界时间器

摘要在这个Flutter初学者教程的第22集中，我们开始构建一个名为World Time的应用程序。教程着重介绍了如何创建Flutter应用程序并组织不同屏幕的基本框架。

亮点

🚀 **创建World Time应用程序：** 开始大型项目World Time应用程序，该应用程序包含三个屏幕：主屏幕（显示时间）、加载屏幕（初始化加载时显示的屏幕）和选择位置屏幕（允许用户选择不同位置查看时间）。

🗂️ **组织代码：** 通过创建不同的页面文件夹（pages）并在其中添加对应的Dart文件，教程强调了如何更好地组织Flutter代码。

📁 **删除测试：** 删除测试文件夹，作者提到目前应用程序相对简单，测试不在本教程范围内，因此删除测试文件夹。

📲 **导航和路由：** 引入基本的导航和路由概念，为将来在不同屏幕之间导航奠定基础。

🛠️ **安全区域小部件：** 引入SafeArea小部件，以确保文本内容不被设备顶部的状态栏遮挡

 🧭 **准备不同屏幕小部件：** 创建了三个基本的Stateful小部件，分别表示主屏幕、选择位置屏幕和加载屏幕，并简单测试了它们。这一集教程为初学者提供了构建Flutter应用程序时的基础知识，并为未来的导航和路由功能打下了基础。



```
//这个程序中程序有三个屏幕，一个是主屏幕显示时间，一个是加载界面，一个是用更新位置
```

所以创建了一个文件夹保存各个界面，

![image-20231110212040137](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110212040137.png)

其中main函数主要是用来控制路由的

然后在每个相应的界面dart里面，各自建造自己的功能模块和展示模块



```
//main.dart

import 'package:flutter/material.dart';
import 'package:world_time/pages/choose_location.dart';
import 'package:world_time/pages/home.dart';
import 'package:world_time/pages/loading.dart';
import 'package:world_time/pages/choose_location.dart';


void main()=>runApp(MaterialApp(
    //这个实验中程序有三个屏幕，一个是主屏幕显示时间，一个是加载界面，一个是用更新位置
    //home:Home(),//调用在home阶段设置的home
    //会和下面的第一个冲突
    initialRoute: '/home',//初始化路由，实现第一个是home，而且不冲突
    routes: {
        //使用routes来创建路线，这将会是一个map，要记住键值对，
        '/':(context)=>Loading(),//正斜杠，是指我们第一次打开应用程序是想要显示的第一个小部件
        //这些不同路线的值将是函数
        '/home':(context)=>Home(),
        '/location':(context)=>ChooseLocation(),





    },
));
```



有一个很重要的东西就是，创建模版的时候一定要把const去掉，不然会报错



```
//通过在按钮的onpressed里面放置这个导航器，实现页面之间的跳转

Navigator.pushNamed(context, '/location');
```



```
body: SafeArea(child: Text('Home screen')),//保证部件的呈现是在可以看见的地方，向下移动到屏幕上的安全区域
```



#### 1、map的概念

 摘要

在这个 Flutter 初学者教程中，我们学到了关于地图和路由的重要概念。通过创建地图，我们理解了在 Flutter 中如何设置和使用类似于对象文字或 Python 字典的地图。接着，我们学到了如何在应用程序中设置不同的路由，以便在屏幕之间进行导航。教程强调了路由的设置和如何使用 `navigator` 对象进行屏幕之间的切换。

亮点

🗺️ 地图学习：通过创建地图，我们了解了在 Flutter 中设置和使用类似于对象文字或 Python 字典的地图。

🛣️ 路由设置：学到了如何在 Flutter 应用程序中设置不同的路由，以便在屏幕之间进行导航。

🚀 初始路由：教程介绍了如何使用 `initialRoute` 属性来设置应用程序的初始路由。

🖱️ 导航操作：了解了如何使用 `navigator` 对象的 `push` 方法进行屏幕之间的导航。

⬅️ 路由管理：探讨了推送和弹出路由的概念，以及管理应用程序中多个路由的重要性

 🔄 刷新路由：演示了如何使用 `Navigator` 中的方法从路由栈中弹出页面，实现页面的返回功能。

🌐 多路由管理：提到了在应用中使用多个路由时，如何高效地管理路由栈。



关于路由map的一些知识

需要一种在这些不同屏幕之间导航的方法，为此我们要解决路由的问题 flutter ups

其实darts中的映射有点像JavaScript中的对象文字或python中的字典，

就像一组键和值对，

map是数据类型

![image-20231110205344422](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110205344422.png)











这样的实现主屏幕还在下面，





推动和弹出路线或屏幕的整个概念

![image-20231110211915235](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231110211915235.png)





### 八、部件的其他功能

#### 1、小部件的生命周期

内容本视频介绍了Flutter中小部件的生命周期，重点讨论了无状态和有状态小部件以及它们的生命周期方法。其中，使用`initState`方法演示了在页面加载时执行代码，以及通过按钮点击使用`setState`触发`build`方法更新小部件树。

 亮点

[🔄] 无状态小部件（Stateless Widget）是不能在创建后随时间更改状态的小部件。

 [🔄] 有状态小部件（Stateful Widget）具有可以随时间更改的状态，并使用`setState`方法触发`build`函数以重新构建小部件树。

 [🔄] 有状态小部件有三个生命周期方法：`initState`，`build`和`dispose`。- [🔄] `initState`方法在创建状态对象时运行一次，通常用于订阅流（streams）或设置小部件将来可能更改的数据。

[🔄] `build`方法用于构建小部件树，每次使用`setState`触发时都会运行，以反映数据更改。

[🔄] `dispose`方法在小部件或状态对象被完全移除时触发-

[🔄] 使用`initState`方法和示例演示小部件的生命周期，通过在页面加载时输出信息以及使用按钮和`setState`触发构建函数来更新计数器演示`build`的运行。



![image-20231112094426848](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112094426848.png)



有状态小部件，是可以随着时间变化而改变的

采用调佣设置状态方法，当我们更改该方法内的数据时，会触发构建函数来重构这个小部件，实现有状态，更新屏幕现有的状态。

小部件也有几个不同的生命周期方法

下面是几个方法：

![image-20231112100236842](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112100236842.png)



![image-20231112100629114](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112100629114.png)

![image-20231112100655937](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112100655937.png)

相关博客讲解：

http://t.csdnimg.cn/mPK9L

http://t.csdnimg.cn/P09OK



实例：

a、//TODO:implement initState

![image-20231112102015824](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112102015824.png)



b、初始化部件和构建部件

```
class _ChooseLocationState extends State<ChooseLocation> {
  int counter=0;
  initState(){
    super.initState();
    print('initState function ran');
    //这个是初始化有状态小部件
  }
  @override
  Widget build(BuildContext context) {
    print('build function ran');//这个是在里面执行，build构建
```

![image-20231112102423530](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112102423530.png)

初始化只会进行一次，而build是有改变就会进行重构



c、计数器

```
body: TextButton(
  onPressed:(){
    setState(() {
      counter+=1;
    });
  },
  child: Text('counter is $counter'),
)//这个是在里面创建一个计数器实例，没点一次这个就会重构build一次
```

![image-20231112103512319](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112103512319.png)



重要的

```
Widget build(BuildContext context) {……}

```

在Flutter中，`build` 方法是`StatefulWidget`的一个重要生命周期方法。这个方法定义了小部件的UI结构，并在小部件需要重新构建时被调用。`build` 方法接收一个`BuildContext`对象，这个对象包含了有关小部件在小部件树中位置的信息。



#### 2、异步

摘要这个教程介绍了Flutter中的异步代码处理方法，重点是使用异步函数、await关键字和Future对象。异步代码用于处理需要在未来某个时刻完成的操作，例如与API端点或数据库的交互。通过使用延迟函数模拟网络请求，演示了非阻塞代码的概念。最后，介绍了如何使用async和await创建异步函数，并使用await确保在一个请求完成后再执行下一个请求。

亮点

⏳ 异步代码表示一个在现在开始并在未来某个时刻完成的操作。

🔄 Flutter中处理异步代码的方法：异步函数、await关键字和Future对象。- 📡 使用延迟函数模拟网络请求，演示了非阻塞代码的工作原理。

🔄 使用async和await创建异步函数，确保在一个请求完成后再执行下一个请求。- 📦 引入Flutter包的概念，为未来使用第三方API获取时间信息做铺垫

 🚀 展示了异步代码的优势，使得在一个请求进行时，代码的其余部分能够继续执行



flutter中的处理Promise、async和wait异步代码之类的事情非常相似。

==异步表示在现在开始到未来的某个时间完成的操作（就是不会现在就停止的），==例如：与API端点或数据库或其他东西交互以获取一些数据

```
class _ChooseLocationState extends State<ChooseLocation> {

  void getdata(){//构建函数

    //simulate network request for a username
    Future.delayed(Duration(seconds:3),(){
     //Future是异步，delayed是使用延迟的意思，Duration(seconds:3）延迟3秒钟
      print('yoshi');
    });

    //simulate network request to get bio of the username
    Future.delayed(Duration(seconds:2),(){
     //Future是异步，delayed是使用延迟的意思，Duration(seconds:3）延迟3秒钟
      print('science');
    });

    print('statement');

  }
```

![image-20231112112456984](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112112456984.png)

按照上面这个对话，那个statement会比上面的yoshi更快出现，因为其没有延迟。



但如果我们想实现，先输出上面的，再输出下面的，就要通过await 等 来实现、

async await

![image-20231112112743515](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112112743515.png)

需要等哪里就加await在其前面，阻塞住



封装成变量

![image-20231112113154356](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112113154356.png)

![image-20231112113232181](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112113232181.png)



关于异步的相关博客：

http://t.csdnimg.cn/KXreX

http://t.csdnimg.cn/qXsk6

http://t.csdnimg.cn/RgQGI





#### 3、flutter包

摘要

在这个 Flutter 初学者教程中，我们学习如何使用 Flutter Packages 中的 HTTP 包。HTTP 包使我们能够轻松处理与第三方 API 的 HTTP 请求，为我们的应用程序提供强大的网络功能。

亮点

📦 Flutter Packages：使用 Flutter Packages，我们可以利用其他开发者已经编写的代码和逻辑，快速实现各种功能，如滑动菜单、日期选择器或文件上传。

🌐 HTTP 包：本教程重点介绍了 HTTP 包，该包允许我们轻松处理与第三方 API 的 HTTP 请求。通过安装和配置 HTTP 包，我们能够进行网络请求，获取所需的数据。

📈 Pub.dev：使用 pub.dev 网站，我们在 pubspec.yaml 文件中添加了 HTTP 包的依赖，通过简单的步骤完成安装。

🔄 异步处理：教程演示了如何使用 Flutter 中的异步代码，以及如何在加载屏幕中使用 HTTP 包进行网络请求，获取数据。

网址;https://pub.dev/packages?q=sdk%3Aflutter

http包实例

![image-20231112124917634](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112124917634.png)

![image-20231112130550780](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112130550780.png)

这两种加入http的方法的效果是一样的

1）方法1![image-20231112130720740](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112130720740.png)

2）方法2

```
dependencies:
  flutter:
    sdk: flutter
    http: ^1.1.0//这里面的^是更新版本号的意思
```

![image-20231112125306969](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112125306969.png)



```
import 'package:http/http.dart';//这个导包都是要加的
```





在loading页面中加入初始化小部件，并且通过我那两个请求的方式来获取数据

使用json占位符来返回信息，Response response

![image-20231112131935684](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112131935684.png)



在main中，把首页面改成'/'

![image-20231112132145016](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112132145016.png)



结果返回

![image-20231112132215113](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112132215113.png)





优化，定义成Map类型 ，使其呈链输出

![image-20231112132757167](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112132757167.png)

![image-20231112132829407](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231112132829407.png)

按照视频教程来的，在添加url的时候会报错，因为这个的形式的uri，所以我们要在前面加上

Uri.parse()



#### 4、World Time API

有关API的相关博客：

http://t.csdnimg.cn/ukSUO

http://t.csdnimg.cn/WL62B



 摘要

在本教程中，作者介绍了如何使用Flutter开发一个显示世界各地时间的应用。教程的焦点是使用World Time API获取时间数据。作者演示了如何通过API请求获取日期时间和时区偏移，并解释了如何将这些信息转换为可用于显示的格式。最后，作者提到了将这些逻辑分离到一个独立的类和文件中，以提高代码的可读性和可重用性。

亮点

🌐 使用World Time API获取时间数据

🌍 通过API请求获取不同地区的日期时间和时区偏移

 🔄 将API响应转换为可用于显示的数据格式

📅 处理日期时间和时区偏移以获得本地时间

 🚀 展示了如何在Flutter应用中实现这一功能

🧠 提到了将代码逻辑分离到独立类和文件中以提高可读性和可重用性

**API 是用于构建应用程序软件的一组子程序定义，协议和工具。一般来说，这是一套明确定义的各种软件组件之间的通信方法。**通用的格式包含 *XML* 和 JSON

对此发出HTTP请求，那么api就会从相应中返回其所有的信息



```
//make the request发送请求
Response response =await get(Uri.parse('http://worldtimeapi.org/api/timezone/America/Argentina/Salta'));//连接api获取数据
Map data=jsonDecode(response.body);//将其改为json协议
//print（data）;

//get properties from data 在数据中获取属性
String datetime =data['datetime'];
//String offset =data['utc_offset'];
String offset =data['utc_offset'].substring(1,3);//substring是选取字符串的部分，这个里面的就是选取1-3位置的子串，避免无关的需要
//print (datetime);
//print(offset);

//create DataTime object，创建DateTime类型
DateTime now =DateTime.parse(datetime);//调用了DateTime类型，来存储时间类型，使其输出更加好看，parse是将上面的传入的参数就行转换
now=now.add(Duration(hours: int.parse(offset)));//这个就是在时间部分加入偏移量或者其他一些时间量，加在时间上，使其更加准确
print(now);
```



![image-20231115090843782](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115090843782.png)



重要代码API

```
Response response =await get(Uri.parse('http://worldtimeapi.org/api/timezone/America/Argentina/Salta'));
//进行网络请求，使用了 Dart 中的 http 包,get 函数是 http 包提供的函数，用于发起 HTTP GET 请求
Map data=jsonDecode(response.body);//将其改为json协议
//response.body: 获取了网络请求的响应体，即从服务器返回的数据。
//jsonDecode(response.body): 将获取到的响应体数据进行 JSON 解码，将其转换为 Dart 中的 Map 对象。
```



#### 5、将world_time的实例化到页面上

 摘要在这个 Flutter 初学者教程的第 28 集中，作者介绍了如何将所有的世界时间逻辑和获取时间的函数分离到一个自定义类中。这个自定义类能够使代码更具可重用性，因为可以在未来的任何文件或小部件中导入该类，并且可以清理当前的小部件代码。教程中包括了创建服务文件夹、导入必要的包、定义世界时间类的属性和构造函数，以及如何在应用程序中使用该类。

亮点

📁 创建服务文件夹（services）和世界时间类（world_time.dart）以组织代码。

📦 导入 HTTP 和 dart:convert 包以支持请求和 JSON 解码。

🔄 将获取时间的函数从当前文件移到新创建的世界时间类中。- 🏗️ 定义世界时间类的属性，如位置、时间、标志图像 URL 和 API 终端 URL。

🛠️ 创建世界时间类的构造函数，以接受位置、标志和 URL，并初始化类的属性

 🔄 在应用程序中使用新的世界时间类，创建类的实例并调用获取时间的函数。

⚙️ 引入异步编程概念，使用 async/await 处理异步函数的调用和等待。





首先创建一个新的文件夹，在其里面定义一个.dart文件，对于一个新的dart文件，相应的import少不了。

world_time文件

```
import 'package:http/http.dart';
import 'dart:convert';

class WorldTime{

  String location;//地方名字for the UI
  String time='';//地方时间，因为下面操作的过程没有对time就行初始化，所以在这里需要初始化
  String flag;//url to an asset flag icon
  String url;//loaction url for api endpoint

  WorldTime({//一定要加require，设置这个参数不可以是null
    required this.location,
    required this.flag,
    required this.url});//这个就是函数擦传入参数设置，所以使用worldtime就要传入这三个参数
  Future<void> getTime() async {
    //future 有点像javascript中的承诺，意味着它是一个占位符值，知道函数完成为止，时刻保持返回void，仅当异步函数已完全完成
    //future是一个临时占位符
    //make the request
    Response response =await get(Uri.parse('http://worldtimeapi.org/api/timezone/$url'));
    //这里面的$url最重要，因为这个使api根据传入的参数而改变
    Map data=jsonDecode(response.body);//连接api获取数据
    //print（data）;

    //get properties from data 在数据中获取属性
    String datetime =data['datetime'];
    //String offset =data['utc_offset'];
    String offset =data['utc_offset'].substring(1,3);//substring是选取字符串的部分，这个里面的就是选取1-3位置的子串，避免无关的需要
    //print (datetime);
    //print(offset);

    //create DataTime object
    DateTime now =DateTime.parse(datetime);//调用了DateTime类型，来存储时间类型，使其输出更加好看，parse是将上面的传入的参数就行转换
    now=now.add(Duration(hours: int.parse(offset)));//这个就是在时间部分加入偏移量或者其他一些时间量，加在时间上，使其更加准确
    //设置时间属性
    time=now.toString();//使用tostring将其转换为字符串，赋予time
  }

  //WorldTime instance=WorldTime(location: 'Berlin',flag:'germany.png',url: 'Europe/Berlin');
  //这个是调用函数，这知识个事例，因为要在其他的函数里面展示，所以这个写在其他页面那里


}
```



loading文件部分

```
String time = 'loading';//为下面文字展示用

  void setupWorldTime() async {
    WorldTime instance = WorldTime(
        location: 'Berlin', flag: 'germany.png', url: 'Europe/Berlin')；
    //调用函数，传入相应的参数
    await instance.getTime();
    print(instance.time);
    setState(() {//使用有状态部件更新页面
      time = instance.time;
    });
  }


  int counter = 0;

  @override
  initState() {
    super.initState();
    setupWorldTime();
    //getTime();
    //它实际运行是，可以在控制台中看到，将其复制粘贴到构建方法里面
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Padding(
        padding: EdgeInsets.all(50.0),
        child: Text(time),
      ),
    );
  }
}
```



重要代码：后面的$url使的api随着传入的参数而改变

==get(Uri.parse('http://worldtimeapi.org/api/timezone/$url'));==





小小避雷，在这个部分的定义函数传参

第一个是string time，因为在下面使用的过程往往会未对time进行初始化就使用，这样会报错，所以对于这种情况再一开始的时候最好给个初始化，time=‘ ’；

第二个就是函数的参数设计，如果直接设置成this.location……，这样的话传入的时候是可以为null，这样对于下面的相应的操作冲突，所以如果你不希望他们为null，就在其前面加上require关键字。

![image-20231115162506099](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115162506099.png)



#### 6、遇到错误的处理

代码中可能发生的错误处理方式

当我们调用的函数没有返回的时候，这个就不会跳转了，这样是不好的，遇到错误的时候，应该把错误展示出来，告诉用户发生了什么错误。

![image-20231115165454156](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115165454156.png)



 [🛠️] 使用 try 和 catch 块处理错误

try就是一开始运行的，如果错误，就运行catch的内容，这为错误提供了表达

```
try{

  //make the request
  Response response =await get(Uri.parse('http://worldtimeapi.org/api/timezones/$url'));
  Map data=jsonDecode(response.body);//连接api获取数据
  //print（data）;

  //get properties from data 在数据中获取属性
  String datetime =data['datetime'];
  //String offset =data['utc_offset'];
  String offset =data['utc_offset'].substring(1,3);//substring是选取字符串的部分，这个里面的就是选取1-3位置的子串，避免无关的需要
  //print (datetime);
  //print(offset);

  //create DataTime object
  DateTime now =DateTime.parse(datetime);//调用了DateTime类型，来存储时间类型，使其输出更加好看，parse是将上面的传入的参数就行转换
  now=now.add(Duration(hours: int.parse(offset)));//这个就是在时间部分加入偏移量或者其他一些时间量，加在时间上，使其更加准确
  //设置时间属性
  time=now.toString();//使用tostring将其转换为字符串，赋予time
}
catch(e){
  print('caught error:$e');
  time='could not get time data';//通过这个来解决红屏和空白问题
}
}
```

[💡] 更新变量以提供有意义的错误消息

```
time='could not get time data';//更新变量解决红屏和空白问题，提供有效错误信息
```

![image-20231115170145160](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115170145160.png)

 [🔄] 避免红屏错误，使用户了解发生了什么- 

[✔️] 成功处理错误



#### 7、在获取数据后重定向到主页展示数据

 摘要

在上面学习如何在loadiing屏幕中获取所需的时间数据，这节将学习如何在得到时间数据后重定向到主页。通过使用 Navigator 对象的 `pushReplacementNamed` 方法，我们成功地在加载屏幕上方推送了主页路由，而不是将其添加到路由堆栈中。此外，我们还探讨了如何通过 `arguments` 参数将数据传递到新路由，并在目标屏幕中访问这些数据。

首先我们先将loading界面上的输出删除，把其的数据传个其他界面。

 🔄 使用 `pushReplacementNamed` 在将loading得到的数据重定向到主页。

🗺️ 通过 `arguments` 参数传递位置、标志和时间数据。

```
void setupWorldTime() async {
  WorldTime instance = WorldTime(
      location: 'Berlin', flag: 'germany.png', url: 'Europe/Berlin');
  await instance.getTime();
  Navigator.pushReplacementNamed(context, '/home',arguments: {
  'location':instance.location,
    'flag':instance.flag,
    'time':instance.time,
  });
  }
  
  //pushReplacementNamed实现的是替换界面，'/home'是替换来的界面，argument是实现把参数传递出去
```



 🧩 利用 `modalRoute.settings.arguments` 在目标屏幕中接收传递的数据。

在home文件中，利用modalRoute.settings.arguments接收传递来的数据

```
class _HomeState extends State<Home> {

  Map data={};//定义一个map数据，用来存储，其设置为等于空映射，当我们启动此状态对象时

  @override
  Widget build(BuildContext context) {
    //在返回任何内容之前声明这些数据并覆盖它。
    data = ModalRoute.of(context)?.settings.arguments as Map<dynamic, dynamic>;
//这个用来接收我们传过来的argument，将返回数据映射
    print(data);
```

这个教程帮助我们理解了如何在 Flutter 中传递路由数据，实现了加载屏幕和主页之间的平滑过渡。



小避雷

仅仅输入这个会报错，错误原因是因为访问argument属性的，可能为空，所以需要使用控安全操作符     ?.    ，使用了空安全的操作符 `?.`，并将结果强制转换为 `Map<dynamic, dynamic>` 类型。这样做是因为 Dart 在运行时可能无法确定 `arguments` 的确切类型，所以你需要告诉它你期望的类型。

![image-20231115174100338](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115174100338.png)

```

//换成这个
data = ModalRoute.of(context)?.settings.arguments as Map<dynamic, dynamic>;//这个用来接收我们传过来的argument，将返回数据映射
```



#### 8、使用intl包格式化和现实日期，通过intl包

教程展示了如何安装这个包intl，并在代码中使用它来美化显示时间和日期。最后，教程还演示了如何将格式化后的日期和时间输出到应用程序的界面上。

📦 安装并使用intl包来格式化日期和时间。

装包都是有两种方式的，我个人推荐第一种在终端安装（快捷方便）、

第一种：在终端通过命令安装

![image-20231115224003972](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115224003972.png)



第二种：在pubspec.yaml处更改调用

![image-20231115224107085](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115224107085.png)





安装好后，记得加上头文件import 'package:intl/intl.dart';

🔄 使用`date format`方法将时间格式化为更易读的形式。

```
//设置时间属性
//time=now.toString();//使用tostring将其转换为字符串，赋予time

//优化时间的格式
time=DateFormat.jm().format(now);//使用这个对时间格式优化
```

![image-20231115224431727](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115224431727.png)

🚀 更新应用程序，以在主屏幕上显示经过格式化的日期和时间。

在home文件中

```
child:Padding(
  padding: const EdgeInsets.fromLTRB(0, 120, 0, 0),//控制左上右下四个方位的填充大小
  child: Column(
    children: <Widget>[
      TextButton.icon(
          onPressed: (){
            Navigator.pushNamed(context, '/location');
            },
        icon:Icon(Icons.edit_location),
        label:Text('Edit Location'),
      ),
      SizedBox(height: 20.0),//加入各种小部件使得界面把数据展示出来
      Row(
        mainAxisAlignment: MainAxisAlignment.center,//主轴中心堆成
        children: <Widget>[
          Text(
            data['location'],//将接受到的数据展示出来，类似数组的使用方式
            style: TextStyle(
              fontSize: 20.0,
              letterSpacing: 2.0
            ),
          )
        ],
      ),
      SizedBox(height: 20.0),
      Text(
        data['time'],
        style: TextStyle(
            fontSize: 70.0,
            letterSpacing: 2.0
        ),
      )
    ],
  ),
)
```

 🎨 通过调整文本样式，使界面更美观。

```
SizedBox(height: 20.0),
Text(
  data['time'],
  style: TextStyle(
      fontSize: 70.0,
      letterSpacing: 2.0
  ),
```



![image-20231115225849464](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115225849464.png)



#### 8、在加载界面上添加旋转图标，安装flutter_spinkit包

网址：https://pub.dev/packages/flutter_spinkit

 摘要本教程介绍了如何使用flutter_SpinKit包在加载屏幕上添加旋转图标，以提高用户体验。通过更改加载屏幕上的简单文本为吸引人的旋转图标，用户能够更清晰地知道应用正在加载数据。🔄 在加载屏幕上添加旋转图标以替代简单的文本，提升用户体验。

安装的教程就不多说，上一节已讲了两个安装方式



📦 使用Flutter Spin Kit包，通过在`pubspec.yaml`文件中添加相应依赖并运行`get dependencies`获取该包。-

🎨 定制旋转图标外观，可以选择不同形状和风格的旋转效果。

```
Widget build(BuildContext context) {
  return Scaffold(
    backgroundColor: Colors.blue[900],//loading界面的背景颜色
    body: Center(
      child: SpinKitFadingCircle(//这个是有统一格式的 SpinKitFading+图形英文，例如 SpinKitFadingCube
        color: Colors.white,//设置图标颜色
        size: 80.0,//设置图标大小
      ),
    ),
  );
}
```

核心代码：==child: SpinKitFadingCircle(//这个是有统一格式的 SpinKitFading+图形英文，例如 SpinKitFadingCube==

 🚀 通过在加载完成后导航到主屏幕，展示旋转图标的加载效果。

![image-20231115231546419](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115231546419.png)

 🎉 提供了多种旋转图标选项，例如旋转圆圈、方块、渐变立方体等。

样式

![image-20231115230812856](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231115230812856.png)

 🛠️ 通过查看Flutter Spin Kit包的文档，了解如何进一步自定义和使用各种属性。



#### 9、动态更新背景

在Flutter教程的第33部分中，介绍了如何使用三元运算符在应用程序中动态显示白天或黑夜的背景图像。教程重点是如何使用Dart中的三元运算符来评估条件，以确定当前时间是白天还是黑夜，并相应地设置背景图像和顶部条颜色。

- 🌞 使用三元运算符动态设置白天或黑夜的背景图像。

  🕐 使用`DateTime`类评估当前时间，以确定是白天还是黑夜。

  📏 介绍了在Flutter中使用`BoxDecoration`和`DecorationImage`来设置背景图像。

在world_time.dart文件中修改

```
bool isDaytime=true;//定义一个布尔类型，判断是不是白天
```

```
//isDaytime = condition ? true : false;
isDaytime = now.hour>6&&now.hour<20? true : false;//使用三元运算法，动态判断白天和黑夜
```



在loading.dart文件中，把isDaytime变量传给其他页面，

```
Navigator.pushReplacementNamed(context, '/home',arguments: {
'location':instance.location,
  'flag':instance.flag,
  'time':instance.time,
  'isDaytime':instance.isDaytime,
});
```

在home.dart文件中

```
//set background
String bgImage=data['isDaytime']?'day.png':'night.png';//接收传入的数据
```



```
//因为我们是将图片完全嵌入到背景里面，为了更适合屏幕，我们使用container容器来实现
  child:Container(
    decoration: BoxDecoration(//Container的装饰属性decoration,BoxDecoration是一个用于定义装饰效果的类。
      image: DecorationImage(//DecorationImage 是用于处理装饰图像的类
        image: AssetImage('assets/$bgImage'),//通过AssetImage获取一个图像文件
        fit:BoxFit.cover,
        //fit: BoxFit.cover 指定了图像的适应方式。BoxFit.cover 的意思是使图像尽可能大，同时保持其纵横比，覆盖整个容器。
      )
    ),
```

![image-20231116084410609](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116084410609.png)



![image-20231116085441883](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116085441883.png)

![image-20231116085522071](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116085522071.png)

- 🎨 根据时间==设置顶部条的颜色==，白天为浅蓝色，黑夜为深蓝色。

![image-20231116090958036](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116090958036.png)

```
//Color bgColor =data['isDaytime'] ? Colors.blue : Colors.indigo[700]; 这个发生了空安全问题

//定义一个颜色变量来设置背景，使用三元运算符进行判断，
Color? bgColor = data['isDaytime'] != null ? (data['isDaytime'] ? Colors.blue : Colors.indigo[700]) : Colors.grey;
//添加了非空断言 !，这表示我们确信 data['isDaytime'] 不会是 null。这样就可以将其安全地转换为 bool 类型，然后再根据条件选择颜色。
```



```
return  Scaffold(
backgroundColor: bgColor,//通过设置背景就可以使那个通知栏变色，但是是在scaffold下面设置
```

- 通过更改，把文字属性变明显

  ```
  icon:Icon(
        Icons.edit_location,
      color: Colors.grey[300],
    ),
    label:Text(
        'Edit Location',
            style:TextStyle(
        color: Colors.grey[300],
    )
    ),
  ),
  ```

![image-20231116091803888](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116091803888.png)

注意

- ⚠️ 需要注意在应用程序中将背景图像和顶部条颜色与当前时间相关联，以使应用在白天和黑夜之间动态变化。
- ℹ️ 三元运算符用于根据条件在两个值之间进行选择，这在动态设置应用程序UI方面非常有用。



#### 10、创建一个选择位置的页面，展示不同的按钮和卡片

摘要

在这个Flutter教程的第34部分中，我们着重于创建一个选择位置的页面。我们计划使用`ListView.builder`构建一个模板，以展示不同位置的按钮或卡片。点击其中一个位置将触发更新操作，创建一个新的`WorldTime`类实例以获取时间数据，并在返回主页时显示更新后的数据。

亮点

🌍 创建`ListView.builder`以展示不同位置的按钮或卡片。

```
//把所有的地址数据，存放在一个列表里面，我们要做的就是循环每一层输出
List <WorldTime> locations=[
WorldTime(url: 'Europe/London', location: 'London', flag: 'uk.png'),
WorldTime(url: 'Europe/Berlin', location: 'Athens', flag: 'greece.png'),
WorldTime(url: 'Africa/Cairo', location: 'Cairo', flag: 'egypt.png'),
WorldTime(url: 'Africa/Nairobi', location: 'Nairobi', flag: 'kenya.png'),
WorldTime(url: 'America/Chicago', location: 'Chicago', flag: 'usa.png'),
WorldTime(url: 'America/New_York', location: 'New York', flag: 'usa.png'),
WorldTime(url: 'Asia/Seoul', location: 'Seoul', flag: 'south_korea.png'),
WorldTime(url: 'Asia/Jakarta', location: 'Jakarta', flag: 'indonesia.png'),
];
```



在部分放在主体部分那里

```
body: ListView.builder(
  itemCount: locations.length,
  itemBuilder:(context,index){
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 1.0,horizontal: 4.0),
      //在垂直方向上应用 1.0 的上下间距，在水平方向上应用 4.0 的左右间距
      child: Card(
        child:ListTile(
          onTap: (){//ontap点击返回
            print(locations[index].location);
          },
          title: Text(locations[index].location),
          leading: CircleAvatar(//添加背景照片，设置圆形头像
            backgroundImage: AssetImage('assets/${locations[index].flag}'),//当我们在字符串中输出变量时，我们必须使用大括号
          ),
        ),
      ),
    );
  }
),
```



🖼️ 使用`ListTile`和`CircleAvatar`创建每个位置的模板。

```
child:ListTile(
  onTap: (){
    print(locations[index].location);
  },
  title: Text(locations[index].location),
  leading: CircleAvatar(
    backgroundImage: AssetImage('assets/${locations[index].flag}'),//当我们在字符串中输出变量时，我们必须使用大括号
  ),
```

🚀 使用`onTap`函数捕获用户点击事件，目前只是打印所选位置的信息。

 📋 使用`Padding`小部件为每个卡片添加间距。

```
return Padding(
  padding: const EdgeInsets.symmetric(vertical: 1.0,horizontal: 4.0),
  //在垂直方向上应用 1.0 的上下间距，在水平方向上应用 4.0 的左右间距
```

![image-20231116093400383](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116093400383.png)

![image-20231116094213045](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116094213045.png)





#### 11、更新返回主界面

摘要

在本教程中，我们学到了如何更新Flutter应用程序中的时间数据，具体涉及点击不同位置后更新时间的过程。我们通过创建一个void函数`update time`来实现这一点，该函数接收索引参数，表示我们要调用`get time`方法的`WorldTime`实例。通过异步方式等待获取时间数据，然后将数据传递回主页并更新UI。

 🌍 更新时间：创建了一个void函数`update time`，用于在点击不同位置后更新时间数据。

在location.dart

```
void updateTime(index) async{
  WorldTime instance=locations[index];
  await instance.getTime();
  //navigate to home screen
  Navigator.pop(context,{
    'location':instance.location,
    'flag':instance.flag,
    'time':instance.time,
    'isDaytime':instance.isDaytime,
  });
}
```



 🔄 异步操作：通过异步操作等待获取时间数据，确保在数据准备好之前不会继续执行后续操作。

🚀 导航和数据传递：使用`navigator.pop`方法将页面弹出栈，返回到底部页面，并传递更新后的数据。

在home.dart文件

```
TextButton.icon(
      onPressed: ()async{
      dynamic result = await Navigator.pushNamed(context, '/location');
      if(result != null){
         setState(() {
         data = {
         'time': result['time'],
         'location': result['location'],
         'isDaytime': result['isDaytime'],
         'flag': result['flag']
         };
         });
    }
},
```

🔄 使用`setState`更新状态：通过`setState`方法更新主页的状态，以便反映新的时间和位置数据。

🌐 网络请求：通过调用`get time`方法获取时间数据，确保在获取数据时应用程序不会阻塞。

```
if(result != null){
  setState(() {
    data = {
      'time': result['time'],
      'location': result['location'],
      'isDaytime': result['isDaytime'],
      'flag': result['flag']
    };
  });
}
```

实现点击，传入新的数据，返回到主界面展示

![image-20231116094213045](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116094213045.png)

![image-20231116104609990](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/image-20231116104609990.png)



📱 Flutter开发：学习了在Flutter应用程序中处理页面导航和状态更新的基本技巧。

🧩 扩展应用：作者鼓励在此基础上进行扩展，例如添加更多位置或使用Firebase作为后端。



**注意：** ==以上仅是是Flutter入门课程的一部分，深入开发建议查阅==

Flutter文档https://flutter.cn/docs

官方Cookbookhttps://flutter.cn/docs/cookbook
