- 数据库访问数据要通过页，一个页就是一个 B + 树节点，访问一个节点相当于一次 I/O 操作，所以越快能找到节点，查找性能越好。  
- B + 树的特点就是够矮够胖，能有效地减少访问节点次数从而提高性能。  
-  
- B + 树是 B 树的改进，简单地说是：只有叶子节点才存数据，非叶子节点是存储的指针；所有叶子节点构成一个有序链表；  
- B + 树使用双向链表串连所有叶子节点，区间查询效率更高（因为所有数据都在 B + 树的叶子节点，扫描数据库 只需扫一遍叶子结点就行了），但是 B 树则需要通过中序遍历才能完成查询范围的查找。  
- B + 树的磁盘读写代价更小。B + 树的内部节点并没有指向关键字具体信息的指针，因此其内部节点相对 B 树更小，通常 B + 树矮更胖，高度小查询产生的 I/O 更少。  
