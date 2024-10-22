当使用Provider进行全局状态管理时，一般会遵循以下步骤：

1. **在应用程序的顶层创建Provider**：在应用程序的顶层（通常是main.dart文件）创建一个Provider，并将要共享的状态放在其中。这个Provider可以是一个简单的数据模型，也可以是一个复杂的状态管理类。
    
2. **在需要访问状态的地方使用Provider**：在需要访问共享状态的地方，使用Provider.of()或Consumer来获取状态。
    
3. **更新状态**：在应用程序的任何地方都可以通过Provider来更新状态，Provider会通知监听该状态的部件进行更新。

引用
```
import 'package:provider/provider.dart';
```

# 1、局部使用 
局部使用与全局使用很相似，假设有两个子组件需要共享某个状态，这时你可以在这两个子组件的公共父组件上使用ChangeNotifierProvider来提供状态。

首先，定义一个数据模型类用来共享状态，在里面设置一些用来改变状态的函数
接着，在父组件中，
```
return ChangeNotifierProvider(
create :(context)=>数据模型类
child:样式

)
```

在子组件1中展示样式，设置一个变量接收状态类的对象
var counter = Provider.of< CounterModel >(context);
展示出来

在子组件2中改变状态，先接收状态类对象
var counter = Provider.of< CounterModel >(context);

使用状态类的函数进行状态改变
onPressed: () {
        counter.increment(); // 触发状态变化
      },



```
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

// 创建一个数据模型表示共享的状态
class CounterModel extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

// 父组件，创建Provider来提供状态
class ParentWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => CounterModel(),
      child: Column(
        children: [
          ChildWidget1(),
          ChildWidget2(),
        ],
      ),
    );
  }
}

// 子组件1，使用Provider.of获取共享状态，并显示
class ChildWidget1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var counter = Provider.of<CounterModel>(context);

    return Container(
      child: Center(
        child: Text(
          'Count: ${counter.count}',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}

// 子组件2，使用Provider.of获取共享状态，并触发状态变化
class ChildWidget2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var counter = Provider.of<CounterModel>(context);

    return ElevatedButton(
      onPressed: () {
        counter.increment(); // 触发状态变化
      },
      child: Text('Increment Count'),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(title: Text('Local State Sharing')),
      body: ParentWidget(),
    ),
  ));
}
```



在试卷簿的科目和试卷使用以上操作

创建状态类
```
// 创建一个provider模型来管理 paperList状态  
class PaperListModel extends ChangeNotifier {  
  List<Paper1> _paperList = [];  
  
  List<Paper1> get paperList => _paperList;  
  
  void addPaper(Paper1 paper) {  
    _paperList.add(paper);  
    notifyListeners(); // 通知监听者状态已更新  
  }  
  
  void removePaper(int index) {  
    _paperList.removeAt(index);  
    notifyListeners(); // 通知监听者状态已更新  
  }  
  
  void addPaperList(List<Paper1> papers) {  
    _paperList.addAll(papers);  
    notifyListeners(); // 通知监听者状态已更新  
  }  
}
```


在主页面新建状态类的对象
```
class _HomeState extends State<Home> {  
  //用于获取输入框的内容  
  TextEditingController _searchController = TextEditingController();  
  
  //paperlist状态管理  
  late PaperListModel _paperListModel;  
  //初始化，获取subject列表  
  @override  
  
  
  void initState() {  

  
    super.initState();  
    _paperListModel=PaperListModel();  
  }
```


把paper需要接收的东西改了,改成需要接收状态类的paperlist信息
子组件1
```
class PaperList extends StatelessWidget {  
  final PaperListModel paperListModel;  
  
  const PaperList({Key? key, required this.paperListModel}) : super(key: key);  
  
  @override  
  Widget build(BuildContext context) {  
    return Wrap(  
      spacing: 20,  
      runSpacing: 10,  
      children: _buildPaperList(),  
    );  
  }  
  
  List<Widget> _buildPaperList() {  
    return paperListModel.paperList.map((paper) => PaperTile(paper: paper)).toList();  
  }  
}
```


子组件2
更改状态
```
children: List.generate(widget.subjects1.length, (index) {  
  return GestureDetector(  
    onTap: () async {  
      updateSelectedIndex(index); // 更新选中的索引  
      // 等待异步操作完成  
      List<dynamic> list2 = await subjects[index].getPapers();  
      print(index);  
      print(subjects[index].index_name);  
      print(list2);  
      // 将 Future<List<dynamic>> 转换为 List<dynamic>      List<dynamic> paperDataList = await list2;  
      // 将数据转换为 Paper 对象列表  
      List<Paper1> papers = convertToPaperList(paperDataList);  
      // 获取 PaperListModel 实例  
      print(papers);  
      var paperListModel = Provider.of<PaperListModel>(context, listen: false);  
      // 将试卷列表添加到 PaperListModel 中  
      paperListModel.addPaperList(papers);  
    },
```




