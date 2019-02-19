#### 功能特性：

**大数据和性能：**

ag-grid是性能最好的网格，处理大量复杂数据，同时执行最佳性能

**过滤&搜索**

提供最先进的过滤和搜索，并允许使用自己喜欢的框架创建自己的过滤器组件。定制**过滤、列过滤、Excel**如列过滤、搜索。

**旋转**

允许影虎在结尾时对数据切片和切块，这非常类似于Excel的旋转功能，它允许用户将行转换为列、应用计算，组数据...

**实时更新**

根据业务情况以不同的流行方式更新网格中的数据。因此您的更新总是立即推送到您的用户服务器推送 ——视口，本地推送。

**CRUD**

如需创建自己的编辑器，可通过喜欢的框架来进行编辑

**Excel集成**

ag-Grid允许生成Excel文件，文件的外观和感觉与您在应用程序中提供的文件完全相同。所有这些都无需服务器交互。Excel导出文档。

**分组,固定和管理列数**

ag-Grid提供了管理列数的所有最先进的功能，包括拖放他们的功能，或使用资金喜欢的框架创建自己的列标题组件。调整列、固定列、分组标题、创建自己的标题。

**排序**

ag-Grid提供开箱即用的快速排序，并让您提供自己的排序比较器，由许多列、动画排序...排序文档。

**APIs**

ag-Grid由程序员而做，为程序员所做。你可以通过UI做任何事情，你可以通过API做任何事情。不同定制选项的数量是无止境的。Grid属性、Grid api，列属性、列api、事件回调。

**分页**

ag-Grid为您提供分页功能，无论您的数据来自哪里，并提供极少的配置。分页文档。

**总计，树型数据和行分组**

ag-Grid允许您按照所需的方式对数据、行进行分组并提供总计。树型数据、浮动行、分组行、聚合、全宽行。

**UI定制**

ag-Grid允许您配置任何UI方面。几乎所有你在UI中看到的内容都是可配置的。创建你自己的主题、新主题、蓝色主题、黑暗主题、材质主题、引导主题、单元格样式。

**复杂单元内容**

ag-Grid可以创建复杂的内容，而不仅仅是渲染一些简单的数据。格式化数据、计算单元格、嵌套网格、单元格渲染器。

**图表**

ag-Grid可让您轻松集成第三方库，以便您可以轻松地将图表带入您的网格D3集成示例

**所有的大框架**

ag-Grid允许您使用以下任何框架：Angular1、Angular、React、Vue、Aurelia、WebComponents、javascript。

ag-Grid 提供了免费版和企业版。

#### 相关内置api:

**columnDefs**:**列标题设置**

**rowData**:**行内数据插入**

**enableColResize**:**是否支持列宽调整**

**rowHeight**:**行高设置**

**rowSelection**:'multiple'  //**单行选中**，"multiple" 多选（ctrl）,"single" 单选

**enableSorting:true**  /**/是否支持排序**

**enableFilter:true**   //**是否可以筛选**

**groupSelectsChildren:true**   //**选中组可选中组下子节点**，

**suppressRowClickSelection**: true, //**true的话点击行内不会进行行选择**

**suppressMovableColumns**: true,  //**阻止列拖拽移动**

**suppressDragLeaveHidesColumns**: true,   /**/阻止列拖拽出表格，列移除**

 **getRowClass**: function(params) {

 return (params.data.name === 'Ford') ? "orange" : null; 

},  //**给整行加样式**，表示name为Ford时，行文字颜色为橘色

 **onRowClicked**: function(event) { 

//event.data 选中的行内数据，event.event 为鼠标事件

 console.log('a row was clicked', event); 

​      },//**行内点击触发**

 **onColumnResized**: function(event) { 

console.log('a column was resized');

​     }, //**列宽度改变触发**

**//表格加载完成触发**

**onGridReady**: function(event) { console.log('the grid is now ready'); },

 //**单元格点击触发**           

 **onCellClicked**: function(event) { console.log('a cell was cilcked'); },

 //**单元格双击触发**         

 **onCellDoubleClicked**: function(event) { console.log('a cell was dbcilcked'); },





