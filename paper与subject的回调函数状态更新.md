
这里有一个bug，就是因为他们paper和subject不是父子关系的，我这里的实现是通过父home接受子subject的index1，然后传递给paper实现的一个状态更新

因为父home在得到index01还要传递给paper，**所以每一次都要重新加载一次页面**，与之前的添加科目名展示到科目列表中不同，**这次的不是严格的父子关系**


**使用回调函数进行状态更新的**
1. 父子关系状态通信：不需要重新加载页面
2. 不是父子关系，要传递通信的：需要重新加载页面



## 关于科目与试卷的状态更新操作
状态更新的实现方式，是通过回调函数实现的，*并且加上开关页面来实现*

首先定义回调函数onTagSubject
```
//回调函数，返回选中科目的index  
void onTagSubject(int Tagsubject) {  
  setState(() {  
    index1=Tagsubject;  
    print("选中的科目index: $index1");  
  
    //关闭所有对话框  
    // Navigator.of(context).popUntil((route) => route.isFirst);  
    Navigator.pushNamed(context, '/home');  
    // 打开新的对话框  
    showDialog(  
      context: context,  
      builder: (BuildContext context) {  
        return Home();  
        },  
    );  
  });  
}
```
![image.png](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/20240717133450.png)


然后，将回调函数传入子组件
```
child: SingleChildScrollView(  
      scrollDirection: Axis.vertical,  
      child: Wrap(  
        spacing: 25,  
        runSpacing: 10,  
        children: [  
          // SubjectList(subjects: subjectList),  
          SubjectList(subjects1: subjectnameList.sublist(0, subjectnameList.length),onTagSubject:onTagSubject,index01: index1,),  
        ],  
      ),  
    ),  
  ),  
),
```
![image.png](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/20240717133722.png)


接着，在子组件中的接收端，加上接受回调函数的参数
```
class SubjectList extends StatefulWidget {  
  final List<String> subjects1;  
  final Function onTagSubject;  
  final int index01;  
  const SubjectList({Key? key, required this.subjects1,required this.onTagSubject,required this.index01}) : super(key: key);  
  @override  
  _SubjectListState createState() => _SubjectListState();  
}
```
![image.png](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/20240717133825.png)


最后，在状态更新的时刻，将新的状态传递出去
```
// 更新选中的索引  
void updateSelectedIndex(int index) {  
  setState(() {  
    selectedIndex = index;  
  });  
  widget.onTagSubject(index);  
}
```

```
updateSelectedIndex(index); // 更新选中的索引
```
![image.png](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/20240717133914.png)

![image.png](https://hmark.oss-cn-guangzhou.aliyuncs.com/%E6%95%B0%E6%8D%AE/20240720143528.png)

从而完成整套的父子状态更新

















