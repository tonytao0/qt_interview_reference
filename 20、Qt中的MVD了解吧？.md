# 20、Qt中的MVD了解吧？

Model（模型）：负责管理数据，提供数据访问接口，当数据发生变化时通知视图  
View（视图）：负责数据的可视化展示，从模型获取数据并呈现给用户  
Delegate（代理）：负责处理视图中项目的编辑和渲染，允许自定义项目的显示和编辑方式  
基类分别为QAbstractItemModel、QAbstractItemView、QAbstractItemDelegate。
  
MVD 通过信号与槽（Signal & Slot） 实现组件间通信，关键交互围绕数据获取和状态通知展开： 
 
    模型（Model）→ 视图（View）：
    当模型数据发生变化时（如新增、修改、删除），模型会发射dataChanged、rowsInserted等信号，通知所有关联的视图更新显示。

    视图（View）→ 模型（Model）：
    视图通过模型提供的接口（如data()获取数据、setData()修改数据）与模型交互。用户在视图上的操作（如点击、编辑）会被视图转发给模型。

    代理（Delegate）→ 模型/视图：
    代理作为中间层，既从模型获取数据用于渲染或编辑（通过index.model()），也将编辑结果通过模型接口写回数据，同时会响应视图的编辑信号（如editorDataChanged）

Qt中提供了默认实现的MVD类，如QTableWidget、QListWidget、QTreeWidget等。 
