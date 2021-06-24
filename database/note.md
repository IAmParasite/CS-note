## 数据库知识点总结

> 18373059 胡鹏飞

### 第一章 引言

- data: used to record information/ is the carrier of Information
- information: interpretation of data
- Data Management - Database
  Data Processing - Computer program
  Data Transmission - Computer Network
- DBMS: Data Definition Language - DDL - easy to define schea
  Data Manipulation Language - DML - query language
  Storage management - retrieve data from disk automatically for you 
  Transaction Management - concurrency control/ recovery
  Automate a lot of boring/mundane operations on data
  Make execution very fast
  Make concurrent access/ modification possible
- schema vs data:
  - schema: describes how data is to be structured 
  - defined at set-up time
  - rarely changes 
  - also called "metadata"
  - data is actual "instance" of database, changes rapidly
- Main functions of DBMS: Data definition/ data manipulation/ data operation/ toolsets
- dbs(database system ) includes database, dbms, application, and users
- Databse system -> App development tools -> DBMS -> OS -> Hardware
- Database users: appliaction programmers/ sophisticated users/ specialized uses/ naive users
- The architecture of a database systems is greatly influenced by **centralized/ client-server/ parallel/ distributed**
- Database advantages: Data sharing/ Data integrity/ Concurrency/ Less data redundancy

### 第二章 数据模型(ER-model)

- data model: the abstraction of real world
- 现实世界-> 概念模型 -> 逻辑模型 -> 物理模型 -> 计算机世界 人类能理解能力逐渐减弱
- ER- model is the most popular conceptual model **Entity sets attributes Relationships** 
- domain: the set of permitted values for each attribute 
- attribute types:
  - simple and composite attributes
  - single-valued and multi-valued attributes 
  - derived attributes: can be computed from other attributes
- **Relation: the subset of $A \times B$**
- the **degree** of relationship: binary relationship/ (multi-way relationships -> )ternary relationship/ unitary relationship
- E/R Relationship Diagrams: one-one/ many-one/ many-many
- Constraints: an assertion about the database that must be true all the time
- Modeling Constraints:
  - **Keys**
  - **Single-value constraints**
  - **Referential integrity constraints**
  - **Domain constraints**
  - **General constraints**
- super key: a set of one or more attributes whose values uniquely determine each entity
- candidate key: an entity set is a minimal super key
- several candidate keys may exist, one of the candidate keys is selected to be **primary key.**
- ER Modeling Principle
  - avoid redundancy
  - don't use an entity set when an attribute will do
- entity set should satisfy at least one of the following conditions:
  - more than the name of something
  - the "many" in a many-one or many-many relationship
- 概念模型结构设计的特点：真实、充分地反映现实世界；易于理解；易于更改；易于向关系、网状、层次等各种数据模型转换
- 概念结构设计地方法与步骤：自顶向下，自底向上，逐步扩张，混合策略
- 数据抽象：对现实世界的一种抽象。三种常用抽象：分类、聚集、概括
- 局部视图设计：选择局部应用、逐一设计分E-R图
- 集成局部视图：合并（消除冲突（属性冲突、命名冲突、结构冲突））、修改与重构（消除不必要的荣誉）

### 第三章 Relational Model 关系模型(逻辑模型的一种)

- Logical Data Model(LDM)
- three elements of logical data model: data structure/ data operation/ data constraints
- 层次模型、网状模型、关系模型、XML模型、面对对象模型
- relation's features:
  - tuples with same value are not allowed
  - relations are unordered
  - attribute values must comply with domain constraint
  - each attribute must has a different name
  - different attributes can use a same domain
  - attribute values are required to be atomic
- Translating from ER to relational model:
  - many-many: 3 tables
  - many-one: no need for relation R, combine R into "many" end
  - one-one: any side is OK
- Relational Database Constraints:
  - Integrity Constraints: prevent semantic inconsistencies in data
    - Domain Integrity
      - attach constraints to values of attributes
      - check the Null value
    - Entity Integrity Constraints
      - **defined by primary key** (not null/ at most one primary key)
      - **unique key(allow null values/multiple unique keys)**
    - Referential Integrity Constraints

### 第四章 关系代数

- Five basic RA operations: 
  - Basic set Operations: union, difference(no intersection, no complement)
  - Selection: $\sigma$
  - Projection: $\varPi$
  - Cartesian Product:
- derived RA Operations:
  - Intersection: R1  R2 must have the same schema $R1 \cap (R1-R2)$
  - Join: Theta join, natural join, Equi-join, outer join, etc.
  - Division
  - Theta Join: $\bowtie _{\theta}$ 
    $R1 \bowtie _{\theta}R2=\sigma_{\theta}(R1\times R2)$
  - Natural join: $\bowtie$
    - $R\times S$
    - Select all the tuples where $r[A_i]=s[B_j]$
    - Eliminate the duplicate attributes
  - Equi-join: $R1\bowtie_{A=B}R2$
  - Outer join: 无法显示符号，左连接即保留左边的悬空元组
  - Division: 一定程度上可以理解为笛卡尔积的逆运算，表示至少，不排除有余数的情况

### 第五章 SQL

- core of SQL: DDL Query DML DCL

- Queries: Single-relation queries/ Multi-relation queries/ Subqueries/ Grouping and Aggregation

- Begin with the relation in the **FROM** clause, apply the selection indicated by the **WHERE** clause, apply the extended projection indicated by the **SELECT** clause.

- use **"AS <new name>"** to rename an attribute

- **FROM语句中可以使用等于、不等于、小于、大于、小于等于、大于等于、between, in, not in, not like, LIKE, || 等字符**

- **_ = 'any character', % = 'any string'**

- **desc for descending order, asc for ascending order**

- Three-Valued Logic: AND = MIN; OR = MAX; NOT(x) = 1-x

- ALL 为缺省值 NULL不计入

- If any aggregation is used, then each element of the SELECT list must be either:

  - Aggregated, or 

  - An attribute on the GROUP BY list

    ```sql
    select bar min(price)
    from sells
    where beer = 'bud'
    # illegal in SQL
    # bar is neither aggregated nor on the GROPU BY list 
    ```

- **HAVING<condition> may follow a GROUP BY clause where the condition applied to each group, and groups not satisfying the condition are eliminated**

- NATURAL JOIN(not supported in SQL Server)/ CROSS JOIN/ JOIN(theta join) ON<condition>/ Left outer join/ Right outer join/ Full outer join

- Subqueries ...

- Order by can not be used in subquery

- correlated subquery uses operator EXISTS

- **EXISTS (<relation>) is true if and only if the <relation> is not empty**

- EXISTS的子查询相当于遍历A表并导入B表，可以进行转化 The select clause can use any attribute with no difference

- 一些带EXISTS或NOT EXISTS 谓词的子查询不能被其他形式的子查询等价替换

- 所有带IN 谓词、比较运算符、ANY 和 ALL谓词的子查询都能用带EXISTS谓词的子查询等价替换

- The Operator ANY: x = ANY(<relation>): equals at least one tuple in the relation

- (subquery) Union, Intersection, and Difference (subquery)

### 第六章 SQL (DDL, DML, DCL, View)

- DDL - Data Definition Language - define a database schema

  - compriese declarations for the relations(tables) of the database
  - views, indexes, triggers
  - Declaring a Relation: CREATE TABLE <name> (<list of elements>);
  - Remove a relation: DROP TABLE <name>;
  - types: INT or INTEGER/ REAL or FLOAT/ CHAR(n)/ VARCHAR(n)/ DATA 'yyyy-mm-dd'/ TIME 'hh:mm:ss'
  - PRIMARY KEY or UNIQUE or NOT NULL or DEFAULT<value>
  - change a relation schema by adding/removing a new attribute: ALTER TABLE <name> ADD/DROP
  -  <attribute declaration>;

- DML - Data Manipulation Language *Insert Delete Update*

  -  Insert: **INSERT INTO <relation> VALUES (<list of values>) or INSERT INTO <relation>(column1, column2, ...)VALUES (<list of values>)  or INSERT INTO<relation> (<subquery>);**
  - **DELETE FROM <relation> WHERE <condition>; Delete all Tuples: DELETE FROM Likes**
  - UPDATA <relation> SET <list of attribute assignments> WHERE <condition on tuples>;

- DCL - Data Control Language

  - discuss this topic later in data security chapter

- Views

  - virtual table: **CREATE VIEW <name> AS <query>;** we can use this virtual table in the other query statement...
  - base table: relation whose value is really stored in the database
  - WITH CHECK OPTION: 在通过视图进行增删改操作时，不破坏视图定义中的谓词条件
  - 避免 SELECT * 方式创建的视图

- 索引

  - 建立索引时加快查询速度的有效手段（基本表的数据存放杂乱无章）

  - 指定某个属性列上建立索引以后，DBMS会建立一个辅助的数据结构，存储经过排序的该属性列的值，以及该值所对应的基本表元组的存放位置

  - 原理：查询涉及到索引列时用B*树结构加快查找

  - 有些DBMS自动建立以下列上的索引：PRIMARY KEY/ UNIQUE

  - ```sql
    CREATE [UNIQUE][CLUSTER] INDEX <index_name> on <table_name>(<column_name>[<order>], ...)
    ```

  - 索引可以建立在一列或多列上，次序为ASC/DESC，缺省值为ASC，CLUSTER 表示索引时**聚簇索引**

- 存储器

- 触发器

### 第七章 规范化理论

- 四种异常：数据冗余、插入异常、删除异常、更新异常
- 函数依赖：关系模式中的个属性之间的相互依赖、相互制约的练习称为数据依赖
  - 函数依赖、多值依赖、连接依赖
  - 函数依赖时最重要的数据依赖
  - 单值函数依赖：Y=F(x) x可以决定一个唯一的函数值Y: $X \rightarrow Y \ $$X$为决定因素，$Y$为依赖因素  $X \leftrightarrow Y$ 否则为 $X \nrightarrow Y$
  - 平凡的函数依赖: Y是X的子集
  - 非平凡的函数依赖: Y不是X的子集 不加说明是非平凡的函数依赖
  - 函数依赖是语义范畴的概念
  - 函数依赖关系的存在与时间无关
  - 无损连接：自然连接可以复原关系模式
  - 函数依赖的性质：
    - 投影性：一组属性函数决定它的所有子集
    - 扩张性：若$X\rightarrow Y 且 W\rightarrow Z$，则$(X,W) \rightarrow (Y,Z)$
    - 合并性：若$X\rightarrow Y 且 X\rightarrow Z$，则$X \rightarrow (Y,Z)$
    - 分解性：$X \rightarrow (Y,Z)$，则$X\rightarrow Y 且 X\rightarrow Z$
  - 完全函数依赖f：如果$X\rightarrow Y$，并且对于任何一个真子集$X'$，都有$X'\nrightarrow Y$，否则为部分函数依赖p
  - 只有当决定因素是组合属性时，讨论部分函数依赖才有意义
  - 传递函数依赖：$X\rightarrow Y, Y\nrightarrow X, Y\rightarrow Z$则称Z对X传递函数依赖 t；若$Y\rightarrow X$则为直接函数依赖
- 范式
  - 第一范式：每个属性都是不可再分的简单项
  - 第二范式：每个非主属性都完全函数依赖于R的每个关系键
    - 超键：$X\rightarrow U$在$R$上成立
    - 候选键：超键且$X$的任一真子集$X_1$都有$X_1\rightarrow U$不成立
    - 主键：可任意指定一个候选键为主键
    - 主属性：任一候选键中出现过的属性
    - 从1NF关系中消除非主属性对关系键的部分函数依赖，可以得到2NF
    - 如果R的关系键为单属性，或R的全体属性均为主属性，则$R\in 2NF$
    - 分解原则为"一事一表"
    - 形式化描述：$X_1\rightarrow^{p}Y且X_1\rightarrow^fY$则可以分解为$R[X_1,Y]$和$R[X,Z]$
    - 缺点：仍然具有上述的4点缺点
  - 第三范式：每个非主属性都不传递依赖于$R$的每个关系键，则$R$属于第三范式
    - 3NF规范化：一事一表
    - 缺点：没有限制主属性对主键的依赖关系
  - BC范式：消除任何属性对键的部分函数依赖和传递函数依赖（主要是解决主属性之间的互相依赖关系）
    - 主要看ppt例子
- 关系模式的规范化
  - 规范化的基本原则：一事一表
  - 方法：若多余一个实体，就把它分离出来
  - 无损连接性：判断方法有定理判别法、列表法、
  - 函数依赖保持性：
  - 三种标准：01,10,11
  - 两个性质是相互独立的标准
- 非规范化设计：增加荣誉、派生列、对表进行合并、分割（水平分割、垂直分割）或增加重复表。主要问题是影响了数据库的完整性...优点减少连接、减少索引的数量、提高响应速度

### 第九章 完整性约束

- Kinds of Constraints: 

  - Keys: specifies that a relation is a ste, not a bag **(Primary Key/ Candidate/Unique Keys/CHECK<condition>)**

    - an attribute-based check is checked only when a value for that attribute is inserted or updated

  - Foreign-key or referential-integrity **(REFERENCES)** two ways to denote the foreign keys

    - Cascade/ Default/ Set NULL

    - ```sql
      ON [UPDATE, DELETE][SET NULL/CASCADE]
      
      create table sells(
        bar char(20),
        beer char(20),
        price REAL,
        foreign key(beer)
          references beers(name)
          on delete set null
          on update cascade
      );
      ```

  - Valued-based constraints(CHECK)

  - Tuple-based constraints

  - Assertions

    - ```sql
      create assertion <name>
      	check(<condition>)
      
      create assertion NoRipoffBars CHECK(
      	not exists(
          	select bar from sells
              group by bar
              having 5.00 < AVG(price)
          )
      );
      ```

    - Trigger: AFTER/ BEFORE/ INSTEAD OF  INSERT/ DELETE/ UPDATE

### 第十章 事务

- ACID properties:
  - atomocity: either all operations of the transaction are properly reflected in the database or none are.
  - consistency: execution of a transaction in isolation preserves the consistency of the database
  - isloation: unaware of other concurretly executing transactions
  - durability: after a transaction completes successfully, the changes it has made to the database persist, even if there are system failures.
- Transaction State:
  - active
  - partially commited
  - failed
  - aborted 
  - commited
- Conflicting instructions
- conflict equivalent: two schedules can transform into each other 
- conflict serialization: schedule S is conflict equivalent to a serial schedule
- four types of conflicts:
  - $I_i=read(Q), \ I_j=read(Q) \ I_i \ and \ I_j \ don't \ conflict$
  - $I_i=read(Q), \ I_j=write(Q)$ $T_i\rightarrow^{Q} T_j$
  - $I_i=write(Q), \ I_j=read(Q) $ $T_i\rightarrow^{Q} T_j$
  - $I_i=write(Q), \ I_j=write(Q)$$T_i\rightarrow^{Q} T_j$
- Lack of Concurrency Control can create data integrity and consistency problems:
  - Lost updates
  - Uncommitted data
  - Inconsistent Retrievals
- Binary locks - lock with 2 states - Eliminates Lost Updates / Too Restrictive
- Shared/ Exclusive Locks
  - 3 states: unlocked, shared, exclusive
  - Shared locks - multiple transactions can hold these on a particular item at the same time
  - exclusive locks - only one of these and no other locks, can be held on a particular item at a time
- Two-Phase Locking (2PL)
  - A transaction can not request additional locaks once it releases any locks
- Strict Two-phase Locking(Strict 2PL) Protocol:
  - Same as 2PL, except: All locks held by a transaction are released only when the transaction completes
  - in effect "shrinking phase" is delayed until: Transaction has commited or decision has been made to abort the transaction(then the locks can be released after rollback)
- Two ways of dealing with deadlocks: prevention and detection
- Deadlock Prevention:
  - Wait-Die: If Ti has higher priority, Ti waits for Tj; otherwise Ti aborts
  - Wound-wait: If Ti has higher priority, Tj aborts; otherwise Ti waits
- Deadlock Detection:
  - Create a waits-for graph:
    - nodes are transactions
    - there is an edge from Ti to Tj if Ti is waiting for Tj to release a lock
  - If a deadlock is found, abort/ rollback one of the transactions

### 第十一章 恢复

- After a system crash, use log to:
  - redo some transaction that did't commit
  - Undo other transactions that didn't commite
- Undo Logging
  - <STart T>
  - <COMMIT T>
  - <ABORT T> 
  - <T, X, v>: T has updated element X, and its old value was v
  - **If T modifies X, then <T,X,v>must be written to disk before X is written to disk**
  - If T commits, then <COMMIT T> must be written to disk only after all changes by T are written to disk
  - Hence: OUTPUTs are done early
- Recovery with Undo Log
  - Idea 1. Decide for each transaction T whether it is completed or not
    - <START T> ... <COMMIT T> ... yes
    - <START T> ... <ABORT T> ... yes
    - <START T> ...  no - incompleted transactions
  - Idea 2. Undo all modifications by incompleted transactions
  - Revocery manager:
    - Read log from the end; cases:
      - <COMMIT T>: mark T as completed
      - <ABORT T>: mark T as completed
      - <START T>: ignore
      - <T,X,v>: if T is not completed then write X = v to disk else ignore
    - from the end to the beginning
- Checkpointing: Checkpoint the database periodically
  - Stop accepting new transactions
  - Wait until all current transactions complete
  - Flush log to disk
  - Write a <CKPT> log record,flush
  - resume transactions
- Redo Logging:
  - <COMMIT T>: mark T as completed
  - <ABORT T>: mark T as completed
  - <START T>: ignore
  - <T,X,v>: T has updated element X, and its new value is v
  - **If T modifies X, then both <T,X,v> and <COMMIT T> must be written to disk before X is written to disk**
  - OUTPUTS are done late
  - Step 1. as same as "Undo"
  - Step 2. Read log from the beginning, redo all updates of **committed** transactions
- UNDO/ REDO Logging
  - only one change:
    - <T, X, u, v> = T has updated element X, its old value was u, and its new value is v
  - **If T modifies X, then <T, X, u, v> must be written to disk before X is written to disk **as same as Undo logging does
  - after system's crash, run recovery manager
    - Redo all commited transactions, top-down First!
    - Undo all uncommitted transactions, bottom-up

### 第十二章 数据库安全性

- 数据库破坏类型：系统故障、事务故障、对数据操作引入的数据错误、认为破坏
- 对应的恢复措施：备份与恢复、并发控制、完整性约束、数据库安全
- 自主式访问控制DAC、强制访问MAC
- 安全管理三个级别：服务器安全管理、数据库安全管理、对象安全管理
- 其中服务器权限：系统管理员、服务器管理员、磁盘管理员、进程管理员、安全管理员、安装管理员、数据库创建者
- Transaction_SQL语句使用grant、revoke和deny三种命令来实现权限管理
- 定义不同外模式来给不同用户来进行访问

### APPENDIX

- BASE
  - Basically Available - the system does guarantee availability, in terms of the CAP theorem. It is always available, but subsets of data may become unavailable for short periods of time.
  - Soft state – State of system may change over time, even without input. Data does not have to be consistent.
  - Eventual Consistency – System will become consistent eventually in the future. ACID, on the contrary, enforces consistency immediately after any operation.
  
- NOSQL - Give up Consistency 

- Recoverable schedule - if a transaction $T_j$ reads a data item previously written by a transaction $T_i$, then the commit operation of $T_i$ appears before the commit operation of $Tj$

  

 

