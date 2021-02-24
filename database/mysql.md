# Mysql

## 基本架构

- 应用层	
- Mysql服务层	
  - MySQL Management Server & utilities(系统管理)	
  - NoSQL Interface(Nosql 接口)	
  - SQL Interface(SQL 接口)	
  - SQL Parser(SQL 解析器)	
  - Optimizer (查询优化器)	
  - Caches & buffers(缓存)	
- 存储引擎层

## 存储引擎比较	
|  Feature  |  MyISAM	|   Memory	|   InnoDB	|  Archive  |   NDB  |	
|-----------|-----------|-----------|-----------|-----------|--------|	
|B树索引   |是         |	是|	是|	|	|	
|备份|	是|	是|	是|	是|	是|	
|集群数据库支持|	 | |		| |	是|	
|聚集索引	| |	 |	是	| 	| |	
|压缩数据	|是	| 	|是	|是	| |	
|数据缓存	| ||	是|	 |	是|	
|数据加密	|是	|是	|是|	是|	是|	
|外键支持	| |	 |	是|	 |	是|	
|全文索引	|是	 |  	|是	| 	| |	
|哈希索引	| |	是|	否|	 |	是|	
|索引缓存	|是	||	是|	 |	是|	
|锁定粒度	|表	|表|	行	|行|	行|	
|MVCC	 | 	| |	是|	 |	 |	
|复制支持| 是	|限量	|是	|是	|是|	
|储存限制|	256TB|	内存	|64TB	| |	384EB|	
|T树索引	| 	| 	| 	| |	是|	
|事务|	 	| |	是	| |	是|

## InnoDB存储引擎

- [链接](innodb.md)

## 索引

- clustered index 
- secondary index
- 倒排索引
- 联合索引
- 哈希索引
- 自适应哈希索引
- 优化器不选择索引

## 优化

## 面试题

- partition 用法
- 分表