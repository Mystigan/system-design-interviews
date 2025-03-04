# Storage\_MySQL\_SchemaDesign

* [MySQL DB Design](storage_mysql_schemadesign.md#mysql-db-design)
  * [\[TODO:::\] Logical design](storage_mysql_schemadesign.md#todo-logical-design)
    * [ER chart](storage_mysql_schemadesign.md#er-chart)
    * [Normal forms](storage_mysql_schemadesign.md#normal-forms)
      * [First norm form](storage_mysql_schemadesign.md#first-norm-form)
      * [Second norm form](storage_mysql_schemadesign.md#second-norm-form)
      * [Third norm form](storage_mysql_schemadesign.md#third-norm-form)
    * [Procedure](storage_mysql_schemadesign.md#procedure)
  * [Physical design](storage_mysql_schemadesign.md#physical-design)
    * [Select the DB engine](storage_mysql_schemadesign.md#select-the-db-engine)
    * [Select the correct data type](storage_mysql_schemadesign.md#select-the-correct-data-type)
    * [Best practices for primary key of Innodb engine](storage_mysql_schemadesign.md#best-practices-for-primary-key-of-innodb-engine)
  * [Performance optimization](storage_mysql_schemadesign.md#performance-optimization)
    * [Factors impacting DB performance](storage_mysql_schemadesign.md#factors-impacting-db-performance)
    * [\[TODO:::\] Slow queries](storage_mysql_schemadesign.md#todo-slow-queries)
    * [Query optimization](storage_mysql_schemadesign.md#query-optimization)
      * [Choose index columns](storage_mysql_schemadesign.md#choose-index-columns)
      * [InnoDB clustered index](storage_mysql_schemadesign.md#innodb-clustered-index)
        * [Always define a primary key for each table](storage_mysql_schemadesign.md#always-define-a-primary-key-for-each-table)
        * [Use auto-increment int column when possible](storage_mysql_schemadesign.md#use-auto-increment-int-column-when-possible)
      * [Composite index](storage_mysql_schemadesign.md#composite-index)
        * [Push range query conditions to last](storage_mysql_schemadesign.md#push-range-query-conditions-to-last)
        * [Order/Group By](storage_mysql_schemadesign.md#ordergroup-by)
        * [Use IN for low radix attributes if leftmost prefix index could not be used](storage_mysql_schemadesign.md#use-in-for-low-radix-attributes-if-leftmost-prefix-index-could-not-be-used)
      * [Use efficient pagination](storage_mysql_schemadesign.md#use-efficient-pagination)
      * [Use covering index to avoid loo](storage_mysql_schemadesign.md#use-covering-index-to-avoid-loo)
      * [Join](storage_mysql_schemadesign.md#join)
      * [Avoid](storage_mysql_schemadesign.md#avoid)
        * [IN operator](storage_mysql_schemadesign.md#in-operator)
        * [Unequal filter when possible](storage_mysql_schemadesign.md#unequal-filter-when-possible)
        * [Filtering based on Nullable match conditions](storage_mysql_schemadesign.md#filtering-based-on-nullable-match-conditions)
        * [Prefix based fuzzy matching](storage_mysql_schemadesign.md#prefix-based-fuzzy-matching)
        * [Type conversion in the filtering condition](storage_mysql_schemadesign.md#type-conversion-in-the-filtering-condition)
        * [Functions on index](storage_mysql_schemadesign.md#functions-on-index)
  * [Appendix](storage_mysql_schemadesign.md#appendix)
    * [ecommerce MySQL physical design](storage_mysql_schemadesign.md#ecommerce-mysql-physical-design)
      * [Product group tables](storage_mysql_schemadesign.md#product-group-tables)
      * [Parameters table](storage_mysql_schemadesign.md#parameters-table)
      * [Brand table](storage_mysql_schemadesign.md#brand-table)
      * [Category table](storage_mysql_schemadesign.md#category-table)
      * [Spu table](storage_mysql_schemadesign.md#spu-table)
      * [Category and brand association table](storage_mysql_schemadesign.md#category-and-brand-association-table)
      * [Sku table](storage_mysql_schemadesign.md#sku-table)
      * [Location table](storage_mysql_schemadesign.md#location-table)
      * [Warehouse table](storage_mysql_schemadesign.md#warehouse-table)
      * [Warehouse and sku association table](storage_mysql_schemadesign.md#warehouse-and-sku-association-table)
      * [Retail shop table](storage_mysql_schemadesign.md#retail-shop-table)
      * [Retail shop and sku association table](storage_mysql_schemadesign.md#retail-shop-and-sku-association-table)
      * [Membership table](storage_mysql_schemadesign.md#membership-table)
      * [Customer table](storage_mysql_schemadesign.md#customer-table)
      * [Customer address table](storage_mysql_schemadesign.md#customer-address-table)
      * [Voucher](storage_mysql_schemadesign.md#voucher)
        * [Voucher table](storage_mysql_schemadesign.md#voucher-table)
        * [Voucher customer association table](storage_mysql_schemadesign.md#voucher-customer-association-table)
      * [Order](storage_mysql_schemadesign.md#order)
        * [Order table](storage_mysql_schemadesign.md#order-table)
        * [Order detail table](storage_mysql_schemadesign.md#order-detail-table)
      * [Dept](storage_mysql_schemadesign.md#dept)
      * [Job](storage_mysql_schemadesign.md#job)
      * [employee](storage_mysql_schemadesign.md#employee)
      * [user](storage_mysql_schemadesign.md#user)
      * [Delivery table](storage_mysql_schemadesign.md#delivery-table)
      * [Return table](storage_mysql_schemadesign.md#return-table)
      * [Rating table](storage_mysql_schemadesign.md#rating-table)
      * [Supplier table](storage_mysql_schemadesign.md#supplier-table)
      * [Supplier sku table](storage_mysql_schemadesign.md#supplier-sku-table)
      * [Purchase table](storage_mysql_schemadesign.md#purchase-table)
      * [Warehouse keeper table](storage_mysql_schemadesign.md#warehouse-keeper-table)
      * [WarehouseKeeper product table](storage_mysql_schemadesign.md#warehousekeeper-product-table)

## MySQL DB Design

### \[TODO:::\] Logical design

* [https://study.163.com/course/courseLearn.htm?courseId=1209773843\#/learn/video?lessonId=1280444061&courseId=1209773843](https://study.163.com/course/courseLearn.htm?courseId=1209773843#/learn/video?lessonId=1280444061&courseId=1209773843)

#### ER chart

* [https://coding.imooc.com/lesson/353.html\#mid=26102](https://coding.imooc.com/lesson/353.html#mid=26102)

#### Normal forms

* Normal forms are a way to measure the redundancy and potential maintenance \(Needs to update multiple relation tables\). They should not be bindly followed to minimize redundancy because they will also increase query cost. 

**First norm form**

* Def: 
  * A relation is in first normal form if every attribute in that relation is atomic and could not be split further.
* Examples for violations:
  * Use Json as an attribute.
  * Use concatination of multiple attribute as an attribute. 

**Second norm form**

* Def: 
  * Prerequisite: If a relation satisfy second norm form, then it must satisfy first norm form. 
  * A relation is in 2NF if it has No Partial Dependency, i.e., no non-prime attribute \(attributes which are not part of any candidate key\) is dependent on any proper subset of any candidate key of the table.
* Examples for violations: 
  * Redundancy in tables. Partial primary key could determine another attribute. 

**Third norm form**

* Def: 
  * Prerequisite: If a relation satisfy third norm form, then it must satisfy second norm form. 
  * A relation is in third normal form if a non-prime attribute is dependent on a non-prime attribute. 
* Example for violations: 

```text
// a relation table for student's record
StudentId int, 
StudentName varchar,
StudentBirthDate timestamp,
SchoolName varchar,
SchoolAddress varchar // School address depends on SchoolName
```

#### Procedure

* Based on the requirements, write down SQL queries. 
* Then based on the complexity of these SQL queries, write down 

### Physical design

#### Select the DB engine

* Comparison between different DB engines: [https://coding.imooc.com/lesson/49.html\#mid=403](https://coding.imooc.com/lesson/49.html#mid=403) 3.08'

#### Select the correct data type

* Cheatsheet for all data types: [https://tableplus.com/blog/2018/07/mysql-data-types-cheatsheet.html](https://tableplus.com/blog/2018/07/mysql-data-types-cheatsheet.html)
* Step
  1. Determine the type category: number, string, time, binary
  2. Determine the specific type: 
     * TinyInt vs SmallInt vs MediumInt vs ..: Use TinyInt to replace enum. 
     * Float vs Double vs Decimal: Use decimal whenever possible because it is more precise.
     * Datetime vs Timestamp vs Date vs Time: In most case use Datetime \(twice the size of Timestamp but unlimited time range. Timestamp only extends until 2038\).
     * String:  
       * Varchar vs Char: Char has fixed size length. Space will be padded in the end. 0-255 byte; Varchar has a larger upperbound 65535 byte. 
         * Use char whenever possible. 
         * Use varchar on cases where max size could be much bigger than average and not so often updated \(Updating on varchar might break indexes\)

#### Best practices for primary key of Innodb engine

* [https://coding.imooc.com/lesson/49.html\#mid=406](https://coding.imooc.com/lesson/49.html#mid=406)

### Performance optimization

#### Factors impacting DB performance

* Hardware 
* Operating system
* DB engine selection
* DB configuration parameters
* DB schema design
  * Slow queries

#### \[TODO:::\] Slow queries

* [https://coding.imooc.com/lesson/49.html\#mid=513](https://coding.imooc.com/lesson/49.html#mid=513)
* [https://study.163.com/course/courseLearn.htm?courseId=1209773843\#/learn/video?lessonId=1280437152&courseId=1209773843](https://study.163.com/course/courseLearn.htm?courseId=1209773843#/learn/video?lessonId=1280437152&courseId=1209773843)

#### Query optimization

* In most cases, please use EXPLAIN to understand the execution plan before optimizing. But there are some patterns practices which are known to have bad performance. 

**Choose index columns**

* [Where to set up index](https://www.freecodecamp.org/news/database-indexing-at-a-glance-bb50809d48bd/)
  * On columns not changing often
  * On columns which have high cardinality
  * On columns whose sizes are smaller. If the column's size is big, could consider build index on its prefix. 

```text
// create index on prefix of a column
CREAT INDEX on index_name ON table(col_name(n))
```

**InnoDB clustered index**

**Always define a primary key for each table**

1. When PRIMARY KEY is defined, InnoDB uses primary key index as the clustered index. 
2. When PRIMARY KEY is not defined, InnoDB will use the first UNIQUE index where all the key columns are NOT NULL and InnoDB uses it as the clustered index.
3. When PRIMRARY KEY is not defined and there is no logical unique and non-null column or set of columns, InnoDB internally generates a hidden clustered index named GEN\_CLUST\_INDEX on a synthetic column containing ROWID values. The rows are ordered by the ID that InnoDB assigns to the rows in such a table. The ROWID is a 6-byte field that increases monotonically as new rows are inserted. Thus, the rows ordered by the row ID are physically in insertion order.

**Use auto-increment int column when possible**

* Why prefer auto-increment over random \(e.g. UUID\)? 
  * In most cases, primary index uses B+ tree index. 
  * For B+ tree index, if a new record has an auto-increment primary key, then it could be directly appended in the leaf node layer. Otherwise, B+ tree node split and rebalance would need to be performed. 
* Why int versus other types \(string, composite primary key\)?
  * Smaller footprint: Primary key will be stored within each B tree index node, making indexes sparser. Things like composite index or string based primary key will result in less index data being stored in every node. 

**Composite index**

* Def: Multiple column builds a single index. MySQL lets you define indices on multiple columns, up to 16 columns. This index is called a Multi-column / Composite / Compound index. If certain fields are appearing together regularly in queries, please consider creating a composite index.

**Push range query conditions to last**

* For range query candidate, please push it to the last in composite index because usually the column after range query won't really be sorted. 

**Order/Group By**

* When using EXPLAIN, the ext column means whether the Order/Group By uses file sort or index sort
* If the combination of WHERE and ORDER/GROUP BY satisfies the leftmost prefix index, then 

**Use IN for low radix attributes if leftmost prefix index could not be used**

```text
// using dating website as an example
// 1. Composite index: city, sex, age
select * from users_table where city == XX and sex == YY and age <= ZZ

// 2. There will be cases where some users don't filter based on sex
select * from users_table where city == XX and age <= ZZ

// 3. Could use IN to make WHERE clause satisfy leftmost prefix condition
select * from users_table where city == XX and Sex in ('male', 'female') and age <= ZZ
```

**Use efficient pagination**

* Pagination starts from a large offset index.

```text
// Original query
select * from myshop.ecs_order_info order by myshop.ecs_order_info.order_id limit 4000000, 100

// Optimization option 1 if order_id is continuous, 
select * from myshop.ecs_order_info order where myshop.ecs_order_info.order_id between 4000000 and 4000100

// Optimization option 2 if order_id is not continuous,
// Compared the original query, the child query "select order_id ..." uses covering index and will be faster.
select * from myshop.ecs_order_info where 
(myshop.ecs_order_info.order_id >= (select order_id from myshop.ecs_order_info order by order_id limit 4000000,1) limit 100)
```

```text
// Original query
select * from myshop.ecs_users u where u.last_login_time >= 1590076800 order by u.last_login_time, u.user_id limit 200000, 10

// Optimization with join query
select * from myshop.ecs_users u (select user_id from myshop.ecs_users where u.last_login_time >= 1590076800) u1 where u1.user_id = u.user_id order by u.user_id
```

**Use covering index to avoid loo**

* Def: A special kind of composite index where all the columns specified in the query exist in the index. So the query optimizer does not need to hit the database to get the data — rather it gets the result from the index itself. 
* Special benefits: Avoid second-time query on Innodb primary key
* Limitations:
  * Only a limited number of indexes should be set up on each table. So could not rely on covered index. 
  * There are some db engine which does not support covered index

```text
// original query
select * from orders where order = 1

// Optimized by specifying the columns to return
// order_id column has index
// queried columns already contain filter columns
select order_id from orders where order_id = 1
```

**Join**

* When joining two tables, assume table A has num1 returned according to the JOIN condition, table B has num2 returned according to the JOIN condition. And Assume num1 &gt; num2. 
* Make sure:
  * Query against table B \(smaller\) will be executed first.
  * filters on table A \(bigger\) will be based on indexed column. 
* Avoid using more than three joins in any case. 
  * For join, handle that inside application code when the join is big. Business applications are easier to scale. 
* Two algorithms:
  * Block nested join
  * Nested loop join

**Avoid**

**IN operator**

* When there are too few or many operators inside IN, it might not go through index. 

**Unequal filter when possible**

* Don't use "IS NOT NULL" or "IS NULL": Index \(binary tree\) could not be created on Null values. 
* Don't use != : Index could not be used. Could use &lt; and &gt; combined together.
  * Select name from abc where id != 20
  * Optimized version: Select name from abc where id &gt; 20 or id &lt; 20

**Filtering based on Nullable match conditions**

* There are only two values for a null filter \(is null or is not null\). In most cases it will do a whole table scanning. 

**Prefix based fuzzy matching**

* Use % in the beginning will cause the database for a whole table scanning. "SELECT name from abc where name like %xyz"

**Type conversion in the filtering condition**

**Functions on index**

* [https://coding.imooc.com/lesson/49.html\#mid=439](https://coding.imooc.com/lesson/49.html#mid=439)
* Don't use function or expression on index column

```text
// Original query:
select ... from product
where to_days(out_date) - to_days(current_date) <= 30

// Improved query:
select ... from product
where out_date <= date_add(current_date, interval 30 day)
```

### Appendix

#### ecommerce MySQL physical design

* SPU: Standard product unit. A specific product such as an iphone 10
* SKU: Stock keeping unit. 

```text
┌───────────────────────┐                     ┌───────────────────────┐ 
│                       │                     │                       │ 
│                       │                     │                       │ 
│                       │                     │                       │ 
│    Category table     │◀─────────1:n───────▶│    Parameter table    │ 
│                       │                     │              *        │ 
│                       │                     │                       │ 
│                       │                     │                       │ 
└───────────────────────┘                     └───────────────────────┘ 
            ▲                                                           
            │                                                           
            │                                                           
           1:1                                                          
            │                                                           
            │                                                           
            ▼                                                           
┌───────────────────────┐                      ┌───────────────────────┐
│                       │                      │                       │
│                       │                      │                       │
│                       │                      │  Stock keeping unit   │
│     Product table     │◀────────1:n─────────▶│         table         │
│                       │                      │                       │
│                       │                      │                       │
│                       │                      │                       │
└───────────────────────┘                      └───────────────────────┘


┌───────────────────────┐                     ┌───────────────────────┐
│                       │                     │                       │
│                       │                     │                       │
│                       │                     │                       │
│     Retail store      │◀─────────m:n───────▶│       Warehouse       │
│                       │                     │              *        │
│                       │                     │                       │
│                       │                     │                       │
└───────────────────────┘                     └───────────────────────┘
            ▲                                             ▲            
            │                                             │            
            │                                             │            
           m:n                                            │            
            │                                             │            
            │                                             │            
            ▼                                             │            
┌───────────────────────┐                                 │            
│                       │                                 │            
│                       │                                 │            
│                       │                                 │            
│       Products        │◀─────────m:n────────────────────┘            
│                       │                                              
│                       │                                              
│                       │                                              
└───────────────────────┘
```

**Product group tables**

* t\_spec\_group table
  * id -- primary key
  * spg\_id -- this category id will help identify categories much faster. 
    * e.g. 0-1000 fruit / 1000-2000 funiture. 
    * Index and unique constraint will be added for this column. 
  * name -- category name

```text
CREATE TABLE t_spec_group(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT "automatically generated primary key",
spg_id INT UNSIGNED NOT NULL COMMENT "category id",
`name` VARCHAR(200) NOT NULL COMMENT "category name",
UNIQUE INDEX unq_spg_id(spg_id),
UNIQUE INDEX unq_name(`name`),
INDEX idx_spg_id(spg_id)
)COMMENT="product group table";
```

**Parameters table**

```text
DROP TABLE IF EXISTS `t_spec_param`;
CREATE TABLE `t_spec_param`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `spg_id` int(10) UNSIGNED NOT NULL COMMENT 'category id',
  `spp_id` int(10) UNSIGNED NOT NULL COMMENT 'parameter id inside a category',
  `name` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'paramter name',
  `numeric` tinyint(1) NOT NULL COMMENT 'whether the parameter is a digit',
  `unit` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'unit of the parameter',
  `generic` tinyint(1) NOT NULL COMMENT 'whether it is a generic parameter, whether this parameter needs to be displayed',
  `searching` tinyint(1) NOT NULL COMMENT 'whether this parameter will be used for search',
  `segements` varchar(500) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'enumeration of parameter values',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_spg_id`(`spg_id`) USING BTREE,
  INDEX `idx_spp_id`(`spp_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 11 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'parameter table' ROW_FORMAT = Dynamic;
```

**Brand table**

```text
CREATE TABLE `t_brand`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `name` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'name ',
  `image` varchar(500) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'image url for the website',
  `letter` char(1) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'first letter of a brand',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_name`(`name`) USING BTREE,
  INDEX `idx_letter`(`letter`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 13 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'brand table' ROW_FORMAT = Dynamic;
```

**Category table**

```text
CREATE TABLE `t_category`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `name` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT '',
  `parent_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'previous categorization level',
  `if_parent` tinyint(1) NOT NULL COMMENT 'whether it has child categorization level',
  `sort` int(10) UNSIGNED NOT NULL COMMENT 'ranking weight',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_parent_id`(`parent_id`) USING BTREE,
  INDEX `idx_sort`(`sort`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 16 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'category table' ROW_FORMAT = Dynamic;
```

**Spu table**

```text
CREATE TABLE `t_spu`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `title` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'title',
  `sub_title` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'sub title',
  `category_id` int(10) UNSIGNED NOT NULL COMMENT 'category id',
  `brand_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'brand id',
  `spg_id` int(10) UNSIGNED NOT NULL COMMENT '品类ID',
  `saleable` tinyint(1) NOT NULL COMMENT 'whether online',
  `valid` tinyint(1) NOT NULL COMMENT 'whether the product is still on the market',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'create timestamp',
  `last_update_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'last modified timestamp',
  `is_delete` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_brand_id`(`brand_id`) USING BTREE,
  INDEX `idx_category_id`(`category_id`) USING BTREE,
  INDEX `idx_spg_id`(`spg_id`) USING BTREE,
  INDEX `idx_saleable`(`saleable`) USING BTREE,
  INDEX `idx_valid`(`valid`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'product table' ROW_FORMAT = Dynamic;
```

**Category and brand association table**

```text
CREATE TABLE `t_category_brand`  (
  `category_id` int(10) UNSIGNED NOT NULL COMMENT 'category id',
  `brand_id` int(10) UNSIGNED NOT NULL COMMENT 'brand id',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`category_id`, `brand_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'association table for brand and category' ROW_FORMAT = Dynamic;
```

**Sku table**

```text
REATE TABLE `t_sku`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `spu_id` int(10) UNSIGNED NOT NULL COMMENT 'product ID',
  `title` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'title',
  `images` json NULL COMMENT 'a list of images',
  `price` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'price', // for discount on price based on memberships, the price does not need to be stored separately. 
  `param` json NOT NULL COMMENT 'parameters',
  `saleable` tinyint(1) NOT NULL COMMENT 'whether this item is still on sale',
  `valid` tinyint(1) NOT NULL COMMENT 'whether this item is still valid',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `last_update_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'last modified time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_spu_id`(`spu_id`) USING BTREE,
  INDEX `idx_saleable`(`saleable`) USING BTREE,
  INDEX `idx_valid`(`valid`) USING BTREE,
  FULLTEXT INDEX `title`(`title`)
) ENGINE = InnoDB AUTO_INCREMENT = 5 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '商品表' ROW_FORMAT = Dynamic;
```

**Location table**

* Province/City tables are created so that it no longer are strings

```text
CREATE TABLE `t_province`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `province` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'province name',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_province`(`province`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 35 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'province table' ROW_FORMAT = Dynamic;

CREATE TABLE `t_city`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `city` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'city',
  `province_id` int(10) UNSIGNED NOT NULL COMMENT 'province ID',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 9 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'city table' ROW_FORMAT = Dynamic;
```

**Warehouse table**

```text
CREATE TABLE `t_warehouse`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `city_id` int(10) UNSIGNED NOT NULL COMMENT 'city ID',
  `address` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'address',
  `tel` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'telephone',
  `lng` decimal(15, 10) NULL DEFAULT NULL COMMENT 'longtitude',
  `lat` decimal(15, 10) NULL DEFAULT NULL COMMENT 'altitude',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_city_id`(`city_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 5 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'warehouse table' ROW_FORMAT = Dynamic;
```

**Warehouse and sku association table**

```text
CREATE TABLE `t_warehouse_sku`  (
  `warehouse_id` int(10) UNSIGNED NOT NULL COMMENT 'warehouse ID',
  `sku_id` int(10) UNSIGNED NOT NULL COMMENT 'product ID',
  `num` int(10) UNSIGNED NOT NULL COMMENT 'number inside warehouse',
  `unit` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'sku unit',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`warehouse_id`, `sku_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'warehouse and sku association table' ROW_FORMAT = Dynamic;
```

**Retail shop table**

```text
CREATE TABLE `t_shop`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `city_id` int(10) UNSIGNED NOT NULL COMMENT 'city id',
  `address` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'address',
  `tel` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'telephone',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_city_id`(`city_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 6 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'retail shop table' ROW_FORMAT = Dynamic;
```

**Retail shop and sku association table**

```text
CREATE TABLE `t_shop_sku`  (
  `shop_id` int(10) UNSIGNED NOT NULL COMMENT '零售店ID',
  `sku_id` int(10) UNSIGNED NOT NULL COMMENT '商品ID',
  `num` int(10) UNSIGNED NOT NULL COMMENT '库存数量',
  `unit` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT '库存单位',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT '逻辑删除',
  PRIMARY KEY (`shop_id`, `sku_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '零售店商品库存表' ROW_FORMAT = Dynamic;
```

**Membership table**

```text
CREATE TABLE `t_level`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `level` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'level',
  `discount` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'discount',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 6 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'membership' ROW_FORMAT = Dynamic;
```

**Customer table**

```text
CREATE TABLE `t_customer`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键',
  `username` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'username',
  `password` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'password encrypted by AES',
  `wechat` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'wechat id',
  `tel` char(11) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'cellphone id',
  `level_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'membership level',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `last_update_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'last modification time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_username`(`username`) USING BTREE,
  INDEX `idx_username`(`username`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 3 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'Customer table' ROW_FORMAT = Dynamic;
```

**Customer address table**

```text
CREATE TABLE `t_customer_address`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `customer_id` int(10) UNSIGNED NOT NULL COMMENT 'customer id',
  `name` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'name',
  `tel` char(11) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'telephone',
  `address` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'address',
  `prime` tinyint(1) NOT NULL COMMENT 'whether to use address as default address to receive the package',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_customer_id`(`customer_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 4 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '?????' ROW_FORMAT = Dynamic;
```

**Voucher**

* Voucher table needs to have two tables. One single table solution is 

**Voucher table**

```text
CREATE TABLE `t_voucher`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `deno` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'amount in the vouncher',
  `condition` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'when this voucher could be applied',
  `start_date` date NULL DEFAULT NULL COMMENT 'start date, could be null meaning always effective',
  `end_date` date NULL DEFAULT NULL COMMENT 'end date, could be null meaning always effective',
  `max_num` int(11) NULL DEFAULT NULL COMMENT 'the max number of voucher',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 3 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'voucher table' ROW_FORMAT = Dynamic;
```

**Voucher customer association table**

```text
CREATE TABLE `t_voucher_customer`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `voucher_id` int(10) UNSIGNED NOT NULL COMMENT 'voucher id',
  `customer_id` int(10) UNSIGNED NOT NULL COMMENT 'customer id',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 6 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'customer voucher association table' ROW_FORMAT = Dynamic;
```

**Order**

* What about use JSON to store multiple ordered items inside a single table?
  * Easy to store, but hard to query. e.g. search for historical orders
  * Needs to split into two table 

**Order table**

```text
CREATE TABLE `t_order`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `code` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'order number, defined as string, which could contain more info about order such as time, category, ...',
  `type` tinyint(3) UNSIGNED NOT NULL COMMENT 'type of order: physical store vs online store',
  `shop_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'physical store id',
  `customer_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'member ID',
  `amount` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'total amount',
  `payment_type` tinyint(3) UNSIGNED NOT NULL COMMENT 'payment method: 1 debit card, 2 credit card, 3 cash',
  `status` tinyint(3) UNSIGNED NOT NULL COMMENT 'order status：1未付款,2已付款,3已发货,4已签收',
  `postage` decimal(10, 2) UNSIGNED NULL DEFAULT NULL COMMENT 'shipping fees',
  `weight` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'weight(gram)',
  `voucher_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'voucher ID',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical deletion',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_code`(`code`) USING BTREE,
  INDEX `idx_code`(`code`) USING BTREE,
  INDEX `idx_customer_id`(`customer_id`) USING BTREE,
  INDEX `idx_status`(`status`) USING BTREE,
  INDEX `idx_create_time`(`create_time`) USING BTREE,
  INDEX `idx_type`(`type`) USING BTREE,
  INDEX `idx_shop_id`(`shop_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 3 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'order table' ROW_FORMAT = Dynamic;
```

**Order detail table**

```text
CREATE TABLE `t_order_detail`  (
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'orderID',
  `old_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'old SKU_OLD table ID',
  `sku_id` int(10) UNSIGNED NOT NULL COMMENT 'sku ID',
  `price` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'original price',
  `actual_price` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'purchase price',
  `num` int(10) UNSIGNED NOT NULL COMMENT 'purchase number',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`order_id`, `sku_id`) USING BTREE,
  INDEX `idx_old_id`(`old_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'order details table' ROW_FORMAT = Dynamic;
```

**Dept**

```text
CREATE TABLE `t_dept`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `dname` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'department name',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_dname`(`dname`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 7 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'department table' ROW_FORMAT = Dynamic;
```

**Job**

```text
CREATE TABLE `t_job`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `job` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'job title',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_job`(`job`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 10 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'job table' ROW_FORMAT = Dynamic;
```

**employee**

```text
CREATE TABLE `t_emp`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键',
  `wid` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'work id',
  `ename` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `sex` char(1) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `married` tinyint(1) NOT NULL,
  `education` tinyint(4) NOT NULL,
  `tel` char(11) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `email` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `address` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `job_id` int(10) UNSIGNED NOT NULL COMMENT 'job ID',
  `dept_id` int(10) UNSIGNED NOT NULL COMMENT 'department ID',
  `mgr_id` int(10) UNSIGNED NULL DEFAULT NULL COMMENT 'manager ID',
  `hiredate` date NOT NULL COMMENT 'employee date',
  `termdate` date NULL DEFAULT NULL COMMENT 'leave date',
  `status` tinyint(3) UNSIGNED NOT NULL COMMENT 'status：1 work,2 vacation,3 leave, 4 death',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_wid`(`wid`) USING BTREE,
  INDEX `idx_job_id`(`job_id`) USING BTREE,
  INDEX `idx_dept_id`(`dept_id`) USING BTREE,
  INDEX `idx_status`(`status`) USING BTREE,
  INDEX `idx_mgr_id`(`mgr_id`) USING BTREE,
  INDEX `idx_wid`(`wid`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 5 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'employee table' ROW_FORMAT = Dynamic;
```

**user**

```text
CREATE TABLE `t_user`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `username` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'username',
  `password` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'password',
  `emp_id` int(10) UNSIGNED NOT NULL COMMENT 'employee ID',
  `role_id` int(10) UNSIGNED NOT NULL COMMENT 'role ID',
  `status` tinyint(3) UNSIGNED NOT NULL COMMENT 'status：1 allow, 2 forbidden',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `last_update_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'last modified time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_username`(`username`) USING BTREE,
  INDEX `idx_username`(`username`) USING BTREE,
  INDEX `idx_emp_id`(`emp_id`) USING BTREE,
  INDEX `idx_role_id`(`role_id`) USING BTREE,
  INDEX `idx_status`(`status`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'user table' ROW_FORMAT = Dynamic;
```

**Delivery table**

```text
CREATE TABLE `t_shipment`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'shipment ID',
  `sku` json NOT NULL COMMENT '商品',
  `qa_id` int(10) UNSIGNED NOT NULL COMMENT 'quality checker ID',
  `de_id` int(10) UNSIGNED NOT NULL COMMENT 'sender ID',
  `postid` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'shipment order',
  `price` decimal(10, 0) UNSIGNED NOT NULL COMMENT 'delivery fee',
  `ecp` tinyint(3) UNSIGNED NOT NULL COMMENT 'id of shipment company',
  `address` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'delivery address',
  `warehouse_id` int(10) UNSIGNED NOT NULL COMMENT 'warehouse ID',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_order_id`(`order_id`) USING BTREE,
  INDEX `idx_qa_id`(`qa_id`) USING BTREE,
  INDEX `idx_de_id`(`de_id`) USING BTREE,
  INDEX `idx_postid`(`postid`) USING BTREE,
  INDEX `idx_warehouse_id`(`warehouse_id`) USING BTREE,
  INDEX `idx_address_id`(`address`) USING BTREE,
  INDEX `idx_ecp`(`ecp`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'shipment table' ROW_FORMAT = Dynamic;
```

**Return table**

```text
CREATE TABLE `t_return`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'order ID',
  `sku` json NOT NULL COMMENT 'return product',
  `reason` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'return reason',
  `qa_id` int(10) UNSIGNED NOT NULL COMMENT '质检员ID',
  `payment` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'return order amount',
  `payment_type` tinyint(3) UNSIGNED NOT NULL COMMENT 'refund way：1 debit card，2 credit card，3 check',
  `status` tinyint(3) UNSIGNED NOT NULL COMMENT 'status: 1 successful returned. 2 failed',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical deletion',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_order_id`(`order_id`) USING BTREE,
  INDEX `idx_qa_id`(`qa_id`) USING BTREE,
  INDEX `idx_status`(`status`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'return table' ROW_FORMAT = Dynamic;
```

**Rating table**

```text
CREATE TABLE `t_rating`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'comment ID',
  `order_id` int(10) UNSIGNED NOT NULL COMMENT 'order ID',
  `sku_id` int(10) UNSIGNED NOT NULL COMMENT 'product ID',
  `img` json NULL COMMENT 'buyers' images',
  `rating` tinyint(3) UNSIGNED NOT NULL COMMENT '评分',
  `comment` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'buyers' comments',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'creation time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_order_id`(`order_id`) USING BTREE,
  INDEX `idx_sku_id`(`sku_id`) USING BTREE,
  INDEX `idx_create_time`(`create_time`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'comment table' ROW_FORMAT = Dynamic;
```

**Supplier table**

```text
CREATE TABLE `t_supplier`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `code` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'supplier id',
  `name` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'supplier name',
  `type` tinyint(3) UNSIGNED NOT NULL COMMENT 'type of supplier：1 factory, 2 agent,3 individual',
  `link_man` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'contact person',
  `tel` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'contact number',
  `address` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL COMMENT 'contact address',
  `bank_name` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'bank name',
  `bank_account` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'bank account',
  `status` tinyint(3) UNSIGNED NOT NULL COMMENT 'status:1 allow, 2 forbidden',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unq_code`(`code`) USING BTREE,
  INDEX `idx_code`(`code`) USING BTREE,
  INDEX `idx_type`(`type`) USING BTREE,
  INDEX `idx_status`(`status`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'supplier table' ROW_FORMAT = Dynamic;
```

**Supplier sku table**

```text
CREATE TABLE `t_supplier_sku`  (
  `supplier_id` int(10) UNSIGNED NOT NULL COMMENT 'supplier ID',
  `sku_id` int(10) UNSIGNED NOT NULL COMMENT 'sku ID',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`supplier_id`, `sku_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = 'supplier sku association table' ROW_FORMAT = Dynamic;
```

**Purchase table**

```text
CREATE TABLE `t_purchase`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  `sku_id` int(10) UNSIGNED NOT NULL COMMENT 'sku ID',
  `num` int(10) UNSIGNED NOT NULL COMMENT 'number',
  `warehouse_id` int(10) UNSIGNED NOT NULL COMMENT 'warehouse ID',
  `in_price` decimal(10, 2) UNSIGNED NOT NULL COMMENT 'purchase price',
  `out_price` decimal(10, 2) UNSIGNED NULL DEFAULT NULL COMMENT 'suggest price',
  `buyer_id` int(10) UNSIGNED NOT NULL COMMENT 'buyer ID',
  `status` tinyint(3) UNSIGNED NOT NULL COMMENT 'status: 1 finished 2 unknown',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT 'modified time',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT 'logical delete',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_sku_id`(`sku_id`) USING BTREE,
  INDEX `idx_warehouse_id`(`warehouse_id`) USING BTREE,
  INDEX `idx_buyer_id`(`buyer_id`) USING BTREE,
  INDEX `idx_status`(`status`) USING BTREE,
  INDEX `idx_create_time`(`create_time`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '采购表' ROW_FORMAT = Dynamic;
```

**Warehouse keeper table**

```text
CREATE TABLE `t_productin`  (
  `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键',
  `storekeeper_id` int(10) UNSIGNED NOT NULL COMMENT '保管员ID',
  `amount` decimal(15, 2) UNSIGNED NOT NULL COMMENT '总金额',
  `supplier_id` int(10) UNSIGNED NOT NULL COMMENT '供应商ID',
  `payment` decimal(15, 2) UNSIGNED NOT NULL COMMENT '实付金额',
  `payment_type` tinyint(3) UNSIGNED NOT NULL COMMENT '支付方式',
  `invoice` tinyint(1) NOT NULL COMMENT '是否开票',
  `remark` varchar(200) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT '备注',
  `create_time` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '添加时间',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_storekeeper_id`(`storekeeper_id`) USING BTREE,
  INDEX `idx_supplier_id`(`supplier_id`) USING BTREE,
  INDEX `idx_payment_type`(`payment_type`) USING BTREE,
  INDEX `idx_create_time`(`create_time`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 2 CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '入库信息表' ROW_FORMAT = Dynamic;
```

**WarehouseKeeper product table**

```text
CREATE TABLE `t_productin_purchase`  (
  `productin_id` int(10) UNSIGNED NOT NULL COMMENT '入库ID',
  `purchase_id` int(10) UNSIGNED NOT NULL COMMENT '采购ID',
  `is_deleted` tinyint(1) NOT NULL DEFAULT 0 COMMENT '逻辑删除',
  PRIMARY KEY (`productin_id`, `purchase_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '入库商品表' ROW_FORMAT = Dynamic;
```

