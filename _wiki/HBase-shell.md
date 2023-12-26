---
layout: wiki
title: HBase Shell
cate1: Bigdata
cate2: 
description: HBase Shell常用命令
keywords: HBase Shell
---

<meta name="referrer" content="no-referrer"/>


### 一般操作
1、HBase shell中的帮助命令非常强大，使用help获得全部命令的列表，使用help ‘command_name’获得某一个命令的详细信息。 例如：
```
help ‘list'
```
2、查询服务器状态
```
status
```
3、查询Hbase版本：
```
version
```
4、查看所有表
```
list
```
### 增删改
1、创建一个表
```
create 'member','member_id','address','info’
```
2、获得表的描述
```
describe 'member'
```
3、添加一个列族
```
alter 'member', 'id'
```
4、删除一个列族
```
alter 'member', {NAME => 'member_id', METHOD => 'delete’}
```
5、删除列
1）通过`delete`命令，我们可以删除id为某个值的`‘info:age’`字段，接下来的get就无视了
```
delete 'member','debugo','info:age'
get 'member','debugo','info:age'
```
2）删除整行的值：deleteall
```
deleteall 'member','debugo'
get 'member',’debugo'
```
6、通过enable和disable来启用/禁用这个表,相应的可以通过`is_enabled`和`is_disabled`来检查表是否被禁用。
```
is_enabled 'member'
is_disabled 'member'
```
7、使用exists来检查表是否存在
```
exists 'member'
```
8、删除表需要先将表disable。
```
disable 'member'
drop 'member'
```
9、put
在HBase shell中，我们可以通过put命令来插入数据。例如我们新创建一个表，它拥有id、address和info三个列簇，并插入一些数据。列簇下的列不需要提前创建，在需要时通过:来指定即可。
```
create 'member','id','address','info'
# 数据
put 'member', 'debugo','id','11'
put 'member', 'debugo','info:age','27'
put 'member', 'debugo','info:birthday','1987-04-04'
put 'member', 'debugo','info:industry', 'it'
put 'member', 'debugo','address:city','beijing'
put 'member', 'debugo','address:country','china'
put 'member', 'Sariel', 'id', '21'
put 'member', 'Sariel','info:age', '26'
put 'member', 'Sariel','info:birthday', '1988-05-09 '
put 'member', 'Sariel','info:industry', 'it'
put 'member', 'Sariel','address:city', 'beijing'
put 'member', 'Sariel','address:country', 'china'
put 'member', 'Elvis', 'id', '22'
put 'member', 'Elvis','info:age', '26'
put 'member', 'Elvis','info:birthday', '1988-09-14 '
put 'member', 'Elvis','info:industry', 'it'
put 'member', 'Elvis','address:city', 'beijing'
put 'member', 'Elvis','address:country', 'china'
```
### 查询
1、查询表中有多少行：count
```
count 'member'
```
2、get
1)获取一个id的所有数据
```
get 'member', ‘Sariel'
```
2)获得一个id，一个列簇（一个列）中的所有数据:
```
get 'member', 'Sariel', 'info'
```
3、查询整表数据
```
scan 'member'
```
4、扫描整个列簇
```
scan 'member', {COLUMN=>'info'}
```
5、指定扫描其中的某个列：
```
scan 'member', {COLUMNS=> 'info:birthday'}
```
6、除了列`（COLUMNS）`修饰词外，HBase还支持`Limit`（限制查询结果行数），`STARTROW`（`ROWKEY`起始行。会先根据这个`key`定位到`region`，再向后扫描）、`STOPROW`(结束行)、`TIMERANGE`（限定时间戳范围）、`VERSIONS`（版本数）、和`FILTER`（按条件过滤行）等。比如我们从`Sariel`这个`rowkey`开始，找下一个行的最新版本
```
scan 'member', { STARTROW => 'Sariel', LIMIT=>1, VERSIONS=>1}
```
7、Filter是一个非常强大的修饰词，可以设定一系列条件来进行过滤。比如我们要限制某个列的值等于26
```
scan 'member', FILTER=>"ValueFilter(=,'binary:26’)"
```
值包含6这个值：
```
scan 'member', FILTER=>"ValueFilter(=,'substring:6')"
```
列名中的前缀为birthday的
```
scan 'member', FILTER=>"ColumnPrefixFilter('birth') “
```
FILTER中支持多个过滤条件通过括号、AND和OR的条件组合
```
scan 'member', FILTER=>"ColumnPrefixFilter('birth') AND ValueFilter ValueFilter(=,'substring:1988')"
```
`PrefixFilter`是对Rowkey的前缀进行判断,这是一个非常常用的功能。
```
scan 'member', FILTER=>"PrefixFilter('E')"
```
