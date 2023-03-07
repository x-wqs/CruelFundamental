## 优势：
- 基于内存，读写快
- 合理的数据结构设计，提供丰富的功能
- 支持主从、哨兵等
- 单线程操作，避免上下文切换

## 劣势：
- 受物理内存限制
- 因为是在内存，断电无法保证数据持久的完整(rdb,aof各有限制)