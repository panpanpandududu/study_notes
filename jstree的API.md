# jstree的API

### jsTree 获取节点方法

#### 1.未采用checkbox

#### get_selected() //获取选中节点

##### 使用方法：$element.jstree().get_selected(true);

##### get_top_selected()  //获取选中节点的父级

$element.jstree().get_top_selected(true);

##### get_bottom_selected()  //获取被选中叶节点

$element.jstree().get_bottom_selected(true);

#### 1.采用checkbox

##### $element.jstree().get_checked(true); // 获取所有选中节点。

##### $element.jstree().get_top_checked(true);//获取所有被选中的父级节点

##### $element.jstree().get_bottom_checked(true);//获取所有被选中的叶节点
