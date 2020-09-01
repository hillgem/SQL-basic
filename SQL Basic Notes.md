---
title: SQL 基础教程
tags: SQL，SQL基础教程，StudyNote
notebook: 210 Language
---

# 一、数据库和SQL
* 数据库是什么
* 数据库的结构
* SQL概要
 * 表的创建
 * 表的删除和更新
## 1.1 数据库是什么
1. 数据库管理系统DBMS：管理数据库的计算机系统
2. 实现多个用户同时安全简单地操作大量数据
3. DBMS种类
    * HDB 层次数据库
            树形结构表示数据
    * RDB 关系数据库
            由行和列组成的二维表管理数据，使用SQL进行数据操作
            RDBMS 关系数据库管理系统
    * OODB 面向对象数据库
            把数据和对数据的操作集合起来以对象为单位进行管理
    * XMLDB XML数据库
            对XML形式的大量数据进行高速处理
    * KVS Key-Value Store 键值存储系统
            保存查询所使用的主键和值的组合数据库
## 1.2 数据库的结构
### RDBMS 常见结构
1. 最常见的系统结构：客户端/服务器类型 （C/S）
 ### 表的结构
1. 根据SQL语句的内容返回的数据同样必须是二维表的形式
2. 字段：保存在表中的数据项目（列）
3. 记录：一条数据（行）
4. 单元格：一个单元格只能输入一个数据
5. **RDB必须以行为单位进行数据读写**
## 1.3 SQL概要
### 标准SQL
1. SQL是为操作数据库而开发的语言
2. 虽然SQL有标准，但是根据RDBMS不同，SQL也会不同
### SQL语句及种类
 * DDL 数据定义语言：create，drop，alter
 * DML 数据操纵语言：select, insert, update, delete
  * DCL 数据控制语言：commit, rollback, grant, revoke
### SQL基本书写规则
* 以；结尾
* 不区分大小写，一般建议：关键字大写，表名首字母大写，其余小写
 * 表中的数据区分大小写
 * 常数书写方式固定，'字符串'，数字，'日期'
* 单词间需要半角空格或换行分隔
## 1.4 表的创建
### 创建数据库
```
CREATE DATABASE <数据库名称>;
```
   
 ### 创建表
 ```
 CREATE TABLE <表名> （
 <列名1> <数据类型> <该列所需约束>， 
 <列名2> <数据类型> <该列所需约束>， 
 <列名3> <数据类型> <该列所需约束>， 
 <列名4> <数据类型> <该列所需约束>，
 ...,
 <该表的约束1>， <该表的约束2>，……）
 ```
* 约束可以在定义列的时候设置，也可以在语句的末尾设置

### 命名规则
* 只能使用半角英文、数字、下划线命名
* 名称必须以半角英文字母开头
* 名称不能重复

### 数据类型的指定
* 所有列都必须制定数据类型
* 数据类型
    * INTEGER 整数数字
    * CHAR 字符串，可指定长度，以定长字符串的形式存储
    * VARCHAR 字符串，可变长字符串
    * DATE 指定存储日期

### 约束的设置
* 对列中存储的数据进行限制或追加条件的功能
* 约束种类
    * NOT NULL：必须输入数据
    * PRIMARY KEY：主键约束

## 1.5 表的删除和更新
### 表的删除
```
DROP TABLE <表名>;
```
* **删除的表无法恢复** 

### 表定义的更新
```
# 标准SQL添加列
ALTER TABLE <表名> ADD COLUMN <列的定义>;
# Oracle & MyServer
ALTER TABLE <表名> ADD <列名>;
# Oracle添加多列
ALTER TABLE <表名> ADD (<列名1>，<列名2>,...);
# 标准删除列
ALTER TABLE <表名> DROP COLUMN <列名>;
```
### 插入数据
```
INSERT INTO <表名> VALUES ('A', 'B',...);
```

---

# 二、查询基础

## 2.1 SELECT语句查询

### 列的查询
* 基本的SELECT语句
  ```
  SELECT <列名>, ... FROM <表名>;
  ```
* 查询结果中列的顺序和SELECT子句中的顺序相同

### 查询表中所有列
```
SELECT * FROM <表名>;
```
* 若使用*，无法设定列的显示顺序

### 为列设定别名
* 可使用AS关键字为列设定别名
* 别名为中文时需要用双引号括起，注意不是单引号

### 常数的查询
* 可直接通过SELECT语句添加相关列表和常数
* 例如：
  ```
  SELECT '商品' AS string, 38 AS number, '2009-02-24' AS date, product_id, product_name  FROM Product;
   ```

### 从结果中删除重复行
* 使用DISTINCT删除重复行
    ```
    SELECT DISTINCT <列名1>, <列名2>,... FROM <表名>;
    ```
* 使用DISTINCT时，NULL也被视为一条数据，含有NULL的数据也会合并
* DISTINCT关键词只能用在第一个列名之前

### 根据WHERE语句来选择记录
* 指定查询数据的条件
* 语法
  ```
  SELECT <列名>,...
  FROM <表名>
  WHERE <条件表达式>;
  ```
* 首先通过WHERE子句查询出符合条件的记录，然后再选出SELECT语句指定的列
* 可不选出作为查询条件的列
* SQL书写顺序不可随意更改，WHERE子句要紧跟在FROM子句之后

### 注释的书写方法
```
--行注释

/*列
注
释
*/
```

## 2.2 算数运算符和比较运算符
### 算数运算符
* 运算以行为单位执行
* SELECT子句中可以使用常数或者表达式
* Example
  ```
  SELECT product_name, sale_price, sale_price*2 AS "sale_price_x2" FROM Product;
  ```
* **所有包含NULL的计算，结果肯定为NULL**

### 比较运算符
* 比较运算符包括：
  * =, >=, >, <=, <
  * <> 不等于
* 使用比较运算符时一定要注意不等号和等号的位置
* Example
  ```
  SELECT product_name, sale_price, purchase_price
  FROM Product
  WHERE sale_price - purchase_price >= 500;
  ```
* 字符串类型的数据原则上按照字典顺序排序，不能与数字的大小顺序混淆
* 不能对NULL使用比较运算符：
  * 用 IS NULL 运算符专门判断是否为NULL 
  * 反之，则使用 IS NUT NULL 运算符

## 2.3 逻辑运算符
### NOT 运算符
* NOT 运算符不可单独使用，必须和其他查询条件组合使用
* Example
  ```
  SELECT product_name, product_id, sale_price
  FROM Product
  WHERE NOT sale_price >= 1000;
  ```

### AND 运算符和 OR 运算符
* Example
  ```
  -- AND运算符
  SELECT  product_name, purchase_price  FROM Product WHERE  product_type = '厨房用具' AND sale_price >= 3000;

  -- OR运算符
  SELECT product_name, purchase_price  FROM Product WHERE product_type = '厨房用具'    OR sale_price >= 3000;
  ``` 
* AND 运算符优先级高于OR运算符，希望OR优先时可以使用括号

### 逻辑运算符和真值
* SQL的逻辑运算为三值对应，除了真假二值外，还有**不确定**，应用于NULL

# 三、聚合与排序

## 3.1 对表进行聚合查询

### 聚合函数
* 聚合函数：用于汇总的函数
* 5个常用函数
  * COUNT
  * SUM
  * AVG
  * MAX
  * MIN
* 除COUNT外，其余函数不能以*为参数
* 聚合函数会将NULL排除在外，但COUNT(*)除外

### 计算表中的数据行数
* 语法
  ```
  SELECT COUNT(*) FROM Product;
  ```
* ()中为输入值，称为**参数**，输出值成为**返回值**
* COUNT函数的结果根据参数的不同而不同。COUNT(*)会得到包含NULL的数据
行数，而COUNT(<列名>)会得到NULL之外的数据行数。

### 计算合计值
* 语法
  ```
  SELECT SUM(<列名>) FROM <表名>;
  ```

### 计算平均值
* 语法
  ```
  SELECY AVG(<列名>) FROM <表名>;
  ```

### 计算最大最小值
* 语法
  ```
  SELECT MAX(<列名>), MIN(<列名>) FROM <表名>;
  ```
* SUM/AVG只能对数值类型的列使用，而MAX/MIN原则上适用于任何数据类型

### 使用聚合函数删除重复值
* 语法
  ```
  SELECT COUNT(DISTINCT <列名>) FROM <表名>;
  ```
* DISTINCT 必须写在括号中，因必须在计算行数之前删除列中的重复数据

## 3.2 对表进行分组
### GROUP BY 子句
* 语法
  ```
  SELECT <列名1>,<列名2>,...
  FROM <表名>
  GROUP BY <列名1>,<列名2>,...
  ```
* 在GROUP BY子句中指定的列称为**聚合键**或**分组列**
* 子句顺序：SELECT - FROM - WHERE - GROUP BY
* 执行顺序：FROM - WHERE - GROUP BY - SELECT

### 聚合键中包含NULL的情况
* 当聚合键中包含NULL时，也会将NULL视为一组特定数据

### 与GROUP BY有关的常见错误
* 使用GROUP BY子句时，SELECT子句中不能出现聚合键之外的列名
* 在GROUP BY子句中不能使用SELECT子句中定义的别名
* GROUP BY子句结果的显示是无序的
* 只有SELECT和HAVING子句中可以使用聚合函数

## 3.3 为聚合结果指定条件

### HAVING 子句
* 对集合指定组的条件，WHERE不能用于指定组的条件，如“数据为两行”、“平均值为500”
* 语法
    ```
    SELECT <列名1>, <列名2>,...
    FROM <表名>
    GROUP BY <列名1>, <列名2>,...
    HAVING <分组结果对应的条件>;
    ```
* HAVING子句必须写在GROUP BY子句之后
* 构成要素限制
    * 常数
    * 聚合函数
    * GROUP BY子句中指定的列名
* 聚合键所对应条件既可以写在HAVING子键中，也可以写在WHERE子键中，推荐书写在WHERE子句里

### 对查询结果进行排序
* ORDER BY 明确指定排列顺序
* 语法
    ```
    SELECT <列名1>, <列名2>, ....
    FROM <表名>
    ORDER BY <排序基准列1>, <排序基准列2>, ...

    ```
* ORDER BY子句需要写在SELECT语句末尾，对数据行进行排序的操作必须在结果即将返回时执行。
* **排序键**：ORDER BY子句中书写的列名称
* 默认按升序排序，也可后加关键字ASC,降序为DESC
* ORDER BY可指定多个排序键，优先使用左侧的键，如果存在相同值，再参考右侧的键
* 排序键中包含NULL时，会在开头或末尾汇总
* ORDER BY子句中可以使用SELECT子句中定义的别名，而GROUP BY不可
* 再ORDER BY子句中可以使用SELECT子句中未使用的列和聚合函数（？）
* 不要使用列编号，影响代码可读性

# 四、数据更新

## 4.1 数据的插入
### INSERT
* 基本语法
  ```
  INSERT INTO <表名> (列1，列2，列3，...) VALUES (值1，值2，值3，...);
  ```
* 表名后面列清单和VALUES子句中的值清单的列数必须保持一致
* 原则上，执行一次INSERT会插入一行数据，但其实很多RDBMS支持一次插入多行数据，Oracle不支持
* 对表进行全列INSERT时，可省略表名后的列清单
* INSERT可直接在VALUES子句的值清单中插入NULL，但想插入NULL的列一定不能设置NOT NULL约束，否则语句会出错

### 插入默认值
* 通过在创建表时的CREATE TABLE中设置DEFAULT约束来设定
* 语法
  ```
  CREATE TABLE ProductIns
  (product_id CHAR(4) NOT NULL,
  sale_price INTEGER DEFAULT 0, -- 销售单价的默认值设定为0;
  PRIMARY KEY (product_id));
  ```
* 可通过显示方法插入默认值，在VALUES子句中指定DEFAULT关键字
* 可通过隐式方法插入默认值，在列清单和VALUES中省略设定了默认值的列
* 若省略了没有设定默认值的列，则该列值设为NULL，因此如果该列设置了NOT NULL约束，则INSERT语句会报错

### 从其他表中复制数据
* 创建表之后才可以复制数据
* 语法
  ```
  INSERT INTO ProductCopy (product_id, product_name, product_type, sale_price, purchase_price, regist_date)
  SELECT product_id, product_name, product_type, sale_price,purchase_price, regist_date
  FROM Product;
  ```
* INSERT语句的SELECT语句中，可使用WHERE子句或GROUP BY子句等任何SQL语法，但使用ORDER BY子句不会产生任何效果

## 4.2 数据的删除
DROP TABLE 可以将表完全删除，而DELETE会留下表，删除其中全部数据内容

### DELETE基本语法
* 语法
```
DELETE FROM <表名>;
```

### 搜索型DELETE
* 指定删除对象的DELETE语句，可通过WHERE子句实现
* 语法
  ```
  DELETE FROM <表名>
  WHERE <条件>;
  ```
* DELETE语句中不能使用ORDER BY, HAVING 和 GROUP BY，因其对删除功能不起作用

### TRUNCATE
* 只能删除表中的全部数据
* TRUNCATE 有时定义为DDL，而不是DML，不能使用ROLLBACK，会默认执行COMMIT

## 4.3 数据的更新

### UPDATE基本语法
* 语法
  ```
  UPDATE <表名>
    SET <列名> = <表达式>;
  ```
* 整列数据都会被修改

### 搜索型UPDATE
* 可以使用WHERE子句
* 语法
  ```
  UPDATE <表名>
    SET <列名> = <表达式>
  WHERE <条件>;
  ```
* 可使用NULL进行清空，但只限于未设置NOT NULL约束和主键约束的列

### 多列更新
* 方法一
  ```sql
  -- 使用逗号对列进行分隔排列
  UPDATE Product
  SET sale_price = sale_price * 10,
      purchase_price = purchase_price / 2
  WHERE product_type = '厨房用具';
  ```
* 方法二
  ```sql
  -- 将列用()括起来的清单形式
  UPDATE Product
  SET (sale_price, purchase_price) = (sale_price * 10, 
      purchase_price / 2)
  WHERE product_type = '厨房用具';
  ```
* 方法一都可以使用，方法二在某些DBMS中无法使用

## 4.4 事务
* 事务：需要在同一个处理单元中执行的一系列更新处理的合集

### 创建事务
* 语法
  ```
  事务开始语句;
    DML语句1;
    DML语句2;
    DML语句3;
    ...
  事务结束语句（COMMIT或者ROLLBACK）;
  ```
* 事务的开始语句不相同，SQL Server：BEGIN TRANSACTION; MySQL：START TRANSACTION；Oracle 无但规定了悄悄开始处理事务的方法

* COMMIT 提交事务包含的全部更新处理的结束处理，一旦提交则无法恢复到事务开始状态

* ROLLBACK 取消处理，取消事务包含的全部更新处理的结束指令，回滚后数据库恢复到事务开始前的状态

### ACID特性
* 原子性：在事务结束时，其中所包含的更新处理要么全部执行，要么完全不执行，也就是要么占有一切要么一无所有。
* 一致性：事务中包含的处理要满足数据库提前设置的约束
* 隔离性：保证不同事务之间互不干扰的特性
* 持久性：在事务（不论是提交还是回滚）结束后，DBMS 能够保证该时间点的数据状态会被保存的特性


# 五、复杂查询

## 5.1 视图
### 视图和表
* 创建表时，会通过INSERT将数据保存到数据库中，而数据库的数据实际上会保存到计算机的存储设备；视图保存从表中去出数据所使用的SELECT语句，数据不会被保存到存储设备中
* 视图的优点
    * 无需保存数据，节省存储设备容量
    * 将频繁使用的SELECT语句保存为视图，无需每次重写

### 创建视图 CREATE VIEW
* 语法
  ```
  CREATE VIEW 视图名称 (<视图列名1>,<视图列名2>,...)
  AS
  <SELECT语句>
  ```
* SELECT语句中列的排列顺序和视图中列的排列顺序相同
* 使用视图查询
  ```sql
  SELECT product_type, cnt product FROM ProductSum;
  ```
    * 首先执行定义视图的SELECT语句
    * 根据结果，再执行在FROM子句中使用视图的SELECT语句
* 多重视图：在视图基础上再次创建视图，要尽量避免，会降低SQL性能

### 视图的限制
* 定义视图时不能使用ORDER BY子句，数据行是没有顺序的
* 视图的更新
    * 若定义视图的SELECT语句能够满足某些条件，则该视图可以被更新
    * 代表性条件
        * SELECT 子句中未使用DISTINCT
        * FROM 子句中只有一张表
        * 未使用GROUP BY 子句
        * 未使用HAVING 子句
    * 对于含聚条件的视图，若更新数据，则对其原表无法修改，致使数据不一致

### 删除视图 DROP VIEW
```
DROP VIEW <视图名称>
```

## 5.2 子查询

### 子查询和视图
* 子查询：将用来定义视图的SELECT语句直接用于FROM子句中
* 语法
  ```sql
  -- 在FROM子句中直接书写定义视图的SELECT语句
  ELECT product_type, cnt_product
  FROM ( SELECT product_type, COUNT(*) AS cnt_product FROM ProductGROUP BY product_type ) 
  AS ProductSum;
  ```
* 子查询作为内层查询会首先执行
* 子查询层数原则上没有限制，子查询的FROM子句中还可以继续使用子查询

### 子查询的名称
* 子查询原则上必须有名字
* 为子查询设定名称时需要使用AS关键字，该关键字有时可省略

### 标量子查询
* 什么是标量
  * 标量：单一
  * 标量子查询：必须且只能返回表中某一行某一列的值

* 在WHERE子句中使用标量子查询
  * WHERE子句中不能使用聚合函数
  * 语法
    ```sql
    SELECT product_id, product_name, sale_price
    FROM Product
    WHERE sale_price > (SELECT AVG(sale_price)
    FROM Product);
    ```
    先执行内层子查询，返回数字后再执行外层查询

* 能够使用常数或者列名的地方，无论是SELECT子句，GROUP BY子句，HAVING子句，还是ORDER BY子句，几乎所有的地方都可以使用
* **注意事项**：该子查询绝不能返回多行结果

## 5.3 关联子查询
### 普通子查询和关联子查询的区别
* 在细分的组内进行比较时，需要使用关联子查询
* 关键是在子查询中添加的WHERE子句的条件
* 语法
    ```sql
    SELECT product_type, product_name, sale_price
    FROM Product AS P1
    WHERE sale_price > (SELECT AVG(sale_price)
    FROM Product AS P2
    WHERE P1.product_type = P2.product_type
    GROUP BY product_type);
    ```
* 关联子查询也可以理解为对集合进行切分

# 六、函数、谓词、CASE表达式

## 6.1 函数

### 函数的种类
* 输入值为参数，输出值为返回值
* 种类：
    * 算数函数
    * 字符串函数
    * 日期函数
    * 转换函数
    * 聚合函数

### 算数函数
* 绝对值 ABS(数值)
* 求余 MOD(被除数，除数)
* 四舍五入 ROUND(对象数值，保留小数的位数)

### 字符串函数
* 拼接 字符串1||字符串2，如果包含NULL，则结果为NULL；mysql中用CONCAT()
* 字符串长度 LENGTH(字符串)
* 小写转换 LOWER(字符串)
* 替换 REPLACE(对象字符串，替换前的字符串，替换后的字符串)
* 截取 SUBSTRING(对象字符串 FROM 截取的起始位置 FOR 截取的字符数)
* 大写转换 UPPER(字符串)

### 日期函数
* 当前日期 CURRENT_DATE，无参数，无需使用括号
* 当前时间 CURRENT_TIME
* 当前日期和时间 CURRENT_TIMESTAMP
* 截取日期元素 EXTRACT(日期元素 FROM 日期)， 该函数的返回值不是日期类型而是数值类型
    ```sql
    SELECT CURRENT_TIMESTAMP,
    EXTRACT(YEAR FROM CURRENT_TIMESTAMP) AS year,
    EXTRACT(MONTH FROM CURRENT_TIMESTAMP) AS month,
    EXTRACT(DAY FROM CURRENT_TIMESTAMP) AS day,
    EXTRACT(HOUR FROM CURRENT_TIMESTAMP) AS hour,
    EXTRACT(MINUTE FROM CURRENT_TIMESTAMP) AS minute,
    EXTRACT(SECOND FROM CURRENT_TIMESTAMP) AS second;
    ```

### 转换函数
* 类型转换 CAST(转换前的值 AS 想要转换的数据类型)
* 返回左侧第一个非空值/替换空值 COALESCE(数据1，数据2，……) 

## 6.2 谓词
返回值为真值的函数

### LIKE 字符串的部分一致查询
* 前方一致查询
    ```sql
    SELECT *
    FROM SampleLike
    WHERE strcol LIKE 'ddd%';
    ```
* 中间一致查询
    ```sql
    SELECT *
    FROM SampleLike
    WHERE strcol LIKE '%ddd%';
    ```
* 后方一致查询
    ```sql
    SELECT *
    FROM SampleLike
    WHERE strcol LIKE '%ddd';
    ```

### BETWEEN 范围查询
* 语法
    ```sql
    SELECT product_name, sale_price
    FROM Product
    WHERE sale_price BETWEEN 100 AND 1000;
    ```
* BETWEEN会包含最大最小两个临界值，若想不包含则需使用大于和小于号

### IS NULL, IS NOT NULL 判断是否为NULL
```sql
SELECT product_name, purchase_price
FROM Product
WHERE purchase_price IS NULL;
```

### IN, OR的简单用法
* 语法
    ```sql
    SELECT product_name, purchase_price
    FROM Product
    WHERE purchase_price IN (320, 500, 5000);
    ```
* 否定形式可以用 NOT IN 来实现
* IN 和 NOT IN 都无法选出NULL数据

### 使用子查询作为IN谓词的参数
* IN， NOT IN 和 子查询
    * IN 谓词可以使用子查询作为其参数
    * 语法
    ```sql
    -- 取得“在大阪店销售的商品的销售单价”
    SELECT product_name, sale_price
    FROM Product
    WHERE product_id IN (SELECT product_id
                            FROM ShopProduct
                            WHERE shop_id = '000C');
    ```
    * NOT IN 同理

### EXIST 谓词
* 用处：判断是否存在满足某种条件的记录
* 通常都会使用关联子查询作为参数
* 子查询中，EXIST只关心记录是否存在，与实际返回的列无关。EXIST只判断是否存在满足子查询中WHERE子句指定条件的记录
* NOT EXIST 可以替换 NOT IN

## 6.3 CASE表达式
* 在区分情况时使用，在编程中通常称为 **（条件）分支**
* 是函数的一种
* 分为**简单CASE表达式**和**搜索CASE表达式**

### 搜索CASE表达式
* 语法
    ```sql
    CASE WHEN <求值表达式> THEN <表达式>
    WHEN <求值表达式> THEN <表达式>
    WHEN <求值表达式> THEN <表达式>
    ...
    ELSE <表达式>
    END
    ```
* ELSE子句不写时，会默认为ELSE NULL，但仍建议写
* END不能省略
* CASE 表达式可以书写在任意位置

# 七、集合运算

## 7.1 表的加减法

### 集合运算
* 集合：记录的集合，表、视图和查询的执行结果
* 集合运算符

### 表的加法 UNION
* 语法
    ```sql
    SELECT product_id, product_name
    FROM Product
    UNION
    SELECT product_id, product_name
    FROM Product2;
    ```
* 集合运算符会除去重复的记录

### 集合运算注意事项
* 作为运算对象的记录的列数必须相同
* 作为运算对象的记录中列的类型必须一致
* 可以使用任何SELECT语句，但ORDER BY子句只能在最后使用一次

### 包含重复行的集合运算 ALL
* 语法
    ```sql
    SELECT product_id, product_name
    FROM Product
    UNION ALL
    SELECT product_id, product_name
    FROM Product2;
    ```
* 可以保留集合中的重复行

### 交集 INTERSECT
* 语法
    ```sql
    SELECT product_id, product_name
    FROM Product
    INTERSECT
    SELECT product_id, product_name
    FROM Product2
    ORDER BY product_id;
    ```
* 应用于两张表，选取除它们当中的公共记录

### 记录的减法 EXCEPT
* 语法
    ```sql
    SELECT product_id, product_name
    FROM Product
    EXCEPT
    SELECT product_id, product_name
    FROM Product2
    ORDER BY product_id;
    ```
* 结果包含Produt表中国记录出去Product2表中记录之后的剩余部分

## 7.2 联结 （以列为单位对表进行联结）

### 内联结 INNER JOIN
* 语法
    ```sql
    SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price
    FROM ShopProduct AS SP INNER JOIN Product AS P 
    ON SP.product_id = P.product_id;
    ```
* FROM子句后面有两张表
* ON后指定两张表联结所使用的列，即**联结键**；指定多个键时可使用AND/OR；內联结时ON子句必不可少，且必须写在FROM和WHERE之间
* SELECT子句中，同时存在于两张表中的列必须标明其表名，推荐所有列均标明
* 內联结可以和**WHERE子句**结合使用选取记录
    ```sql
    SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price
    FROM ShopProduct AS SP INNER JOIN Product AS P ①
    ON SP.product_id = P.product_id
    WHERE SP.shop_id = '000A';
    ```

### 外联结 OUTER JOIN
* 语法
    ```sql
    SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price
    FROM ShopProduct AS SP RIGHT OUTER JOIN Product AS P ①
    ON SP.product_id = P.product_id;
    ```
* 外联结只要数据存在于某一张表，就可以读取，常用于业务上生成固定行数的单据；相比之下內联结只能选出同时存在于两张表中的数据，在执行时，商店库存的情况不同，结果的行数也会发生改变
* 使用LEFT 时FROM 子句中写在左侧的表是主表，使用RIGHT时右侧的表是主表，最终结果会包含主表内的所有数据

### 三张表以上联结
```sql
SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price, IP.inventory_quantity
FROM ShopProduct AS SP INNER JOIN Product AS P
    ON SP.product_id = P.product_id
        INNER JOIN InventoryProduct AS IP ②
            ON SP.product_id = IP.product_id
WHERE IP.inventory_id = 'P001';
```

### 交叉联结 CROSS JOIN
* 语法
    ```sql
    SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name
    FROM ShopProduct AS SP CROSS JOIN Product AS P;
    ```

# 八、SQL高级处理

## 8.1 窗口函数
* 窗口函数，即OLAP函数（Online Analytical Processing），即对数据库数据进行实时分析处理

### 窗口函数语法
```sql
-- []中的内容可以省略。
<窗口函数> OVER ([PARTITION BY <列清单>]
ORDER BY <排序用列清单>)
```
* 能作为窗口函数使用的函数
    * 可作为窗口函数的聚合函数：SUM/AVG/COUNT/MAX/MIN
    * 专用窗口函数：RANK/DENSE_RANK/ROW_NUMBER

### RANK函数
```sql
SELECT product_name, product_type, sale_price,
RANK () OVER (PARTITION BY product_type
ORDER BY sale_price) AS ranking
FROM Product;
```
* PARTITION BY: 设定排序的对象范围，横向上对标进行分组
* ORDER BY：指定按照哪一列，何种顺序进行排序，决定纵向排序规则
* 通过PARTITION BY分组后的记录集合称为“窗口”，即“范围”
* 可以不指定PARTITION BY，即不分类
* 由于专用窗口函数无需参数，因此通常括号中都是空的。

### 专用窗口函数种类
* RANK 函数
    * 计算排序时，如果存在相同位次记录，则会跳过之后的位次
    * 1、1、1、4、...
* DENSE_RANK 函数
    * 计算排序，即使存在相同位次记录，也不会跳过之后的位次
    * 1、1、1、2、...
* ROW_NUMBER 函数
    * 赋予唯一连续位次
    * 1、2、3、4、...

### 窗口函数的适用范围
* 原则上窗口函数只能在SELECT子句中使用

### 作为窗口函数使用的聚合函数
```sql
SELECT product_id, product_name, sale_price,
　SUM (sale_price) OVER (ORDER BY product_id) AS current_sum
FROM Product;
```
* 累计，自己与所有排在自己之上的商品价格的总和
* 其他函数同理

### 计算移动平均
* **框架**：包含在窗口中指定更加详细的汇总范围的备选功能
* 语法
    ```sql
    -- 指定“最靠近的3行”作为汇总对象
    SELECT product_id, product_name, sale_price,
        AVG (sale_price) OVER (ORDER BY product_id
                                ROWS 2 PRECEDING) AS moving_avg
    FROM Product;
    ```
* 将PRECEDING替换为FOLLWING，则指定截至到~之后2行的窗口范围
* 同时使用PRECEDING和FOLLOWING实现指定前后行
    ```sql
    SELECT product_id, product_name, sale_price,
        AVG (sale_price) OVER (ORDER BY product_id
                                ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS moving_avg
    FROM Product;
    ```

### 两个ORDER BY
* OVER子句中的ORDER BY只决定窗口函数按照什么顺序计算，不影响结果排列顺序
* 若要结果按顺序排列，则需在SELECT语句最后使用ORDER BY指定