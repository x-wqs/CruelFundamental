数据库访问数据要通过页，一个页就是一个B+树节点，访问一个节点相当于一次I/O操作，所以越快能找到节点，查找性能越好。 B+树的特点就是够矮够胖，能有效地减少访问节点次数从而提高性能。