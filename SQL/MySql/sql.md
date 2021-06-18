##### 常用SQL

```mysql
删除某一行:
delete from t_test where ID=4

删除一个表不流任何数据:
drop table t_test

创建表: 
CREATE TABLE t_order(id varchar2(12) primary key ,

​             status char(2),

​             orderer varchar2(10),

​             address varchar2(10),

​             price number(8),

​             phone varchar2(11));

SELECT * FROM 表名 WHEH  1=1
```



##### 表结构导出excel

[MySQL的information_schema库中有个COLUMNS表，里面记录了mysql所有库中所有表的字段信息](https://blog.csdn.net/lkforce/article/details/79557482)

```mysql
SELECT '字段','类型','长度','小数点','是否允许非空','是否为空','说明'

UNION

SELECT

COLUMN_NAME as 字段,

COLUMN_TYPE as 类型,

if(numeric_precision is null,0,numeric_precision) AS 长度,

if(numeric_scale is null,0,numeric_scale) AS 小数点,

is_nullable AS 是否允许非空,

if(COLUMN_KEY='PRI','-1','0') as 是否为空,

COLUMN_COMMENT as 说明

FROM

 INFORMATION_SCHEMA. COLUMNS

WHERE

 table_schema = 'metro_back02'

AND 

 table_name = 'dw_point'

INTO OUTFILE 'd:/test/dw_point.xls'CHARACTER SET gbk
```

