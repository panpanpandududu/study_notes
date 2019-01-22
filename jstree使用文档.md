# jstree使用文档

### 1.引入脚本

#### 需引入三个脚本文件：

1.jquery:版本>=1.9.1

2.一个jstree主题

3.jstree资源文件

```html
<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/jstree/3.3.3/themes/default/style.min.css" />
<script src="//cdnjs.cloudflare.com/ajax/libs/jstree/3.3.3/jstree.min.js"></script>
```

### 2.用html标签定义树

只需用jQuery选择要渲染成jstree的dom元素，然后调用，jstree渲染就可以，也可以用 `$.jstree.create(element)` 的方式渲染。如下所示：

```html
<div id="container">
  <ul>
    <li>Root node
      <ul>
        <li>Child node 1</li>
        <li>Child node 2</li>
      </ul>
    </li>
  </ul>
</div>
<script>
$(function() {
  $('#container').jstree();
});
</script>
```

