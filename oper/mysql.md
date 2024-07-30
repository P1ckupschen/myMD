新建表

CREATE TABLE create_test1(
	`id` INT PRIMARY KEY AUTO_INCREMENT,
	`name` VARCHAR(255) NOT NULL,
	`score` INT NOT NULL DEFAULT 0,
	`description` VARCHAR(100),
    <!-- KEY 和 INDEX 作用一直 非唯一性索引  -->
    <!-- UNIQUE KEY 唯一性索引 -->
	KEY `name_index`(`name`)
)ENGINE = INNODB DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_general_ci; 



CREATE TABLE user (    

id BIGINT(20) NOT NULL COMMENT '主键ID',   

 name VARCHAR(30) NULL DEFAULT NULL COMMENT '姓名',   

 age INT(11) NULL DEFAULT NULL COMMENT '年龄',  

 email VARCHAR(50) NULL DEFAULT NULL COMMENT '邮箱',    PRIMARY KEY (id)

 );

添加索引

ALTER TABLE tableName ADD INDEX indexName(columnName(length) [ASC|DESC]);

CREATE INDEX indexName ON tableName (columnName(length) [ASC|DESC]);

删除

DROP INDEX indexName ON tableName;



修改列类型
alter table table_name  modify column new_type;

alter table sys_dep add UNIQUE(`name`)
alter table sys_dep drop UNIQUE(`name`)
增加新列 
alter table table_name add new_col; 
更新新列
update tablename set new_col=old_col;
删除旧列
alter table table_name  drop column old_col;
修改新列名为原来表的列名
alter table tablename rename column new_col  to old_col;

5.7版本

alter table `sys_data` change column create_time createTime datetime;

数据插入
LOCK TABLES `STUDENT` WRITE;

INSERT INTO `STUDENT` VALUES ('108','曾华','男','1977-09-01 00:00:00','95033'),('105','匡明','男','1975-10-02 00:00:00','95031'),('107','王丽','女','1976-01-23 00:00:00','95033'),('101','李军','男','1976-02-20 00:00:00','95033'),('109','王芳','女','1975-02-10 00:00:00','95031'),('103','陆君','男','1974-06-03 00:00:00','95031');

UNLOCK TABLES;

数据更新
Update student
set class=95031
where sno=109;

数据删除
DELETE FROM student where condition

清空表数据
TRUNCATE TABLE sys_table;

导出表数据
mysqldump -u hbkj -p -h 10.195.159.201 --set-gtid-purged=off -P 30335 hb_sql > /mnt/data/back.sql;

查看表结构
show full columns from sys_report;



CREATE TABLE sys_jiuzhen(
	ID BIGINT PRIMARY key AUTO_INCREMENT,

​    BINGRENID VARCHAR(255),

​	YUANQUID VARCHAR(255) ,
​	XINGMING VARCHAR(255) ,
​	XINGBIE VARCHAR(10) ,
​	NIANLING INT ,
​	SHENFENZH VARCHAR(255) ,
​	JIUZHENID VARCHAR(255) ,
​	JIUZHENGRQ DATETIME ,
​	CHUSHENGRQ DATETIME ,
​	LIANXIDH VARCHAR(255) ,
​	JIUZHENYS VARCHAR(255),
​	JIUZHENYSXM VARCHAR(255) ,
​	JIUZHENKS  VARCHAR(255) ,
​	JIUZHENKSMC  VARCHAR(255) ,
​	ZHUSU LONGTEXT,
​	XIANBINGSHI LONGTEXT,
​	JIAZUSHI LONGTEXT,
​	YUEJINGSHI LONGTEXT,
​	TIGEJC LONGTEXT,
​	ZHONGYISZ1 LONGTEXT,
​	ZHONGYISZ2 LONGTEXT,
​	ZHONGYISZ3 LONGTEXT,
​	ZHONGYISZ4 LONGTEXT,
​	ZHIZEZHIFA LONGTEXT,
​	SHENGAO VARCHAR(255),
​	TIZHONG VARCHAR(255),
​	TIWEN VARCHAR(255),
​	MAIBO VARCHAR(255),
​	SHUZHANGYA VARCHAR(255),
​	SHOUSUOYA  VARCHAR(255),
​	SHEXIANG  VARCHAR(255),
​	MAIXIANG  VARCHAR(255),
​	XUEWEI  VARCHAR(255)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

##### 修改密码

ALTER USER 'username'@'localhost' IDENTIFIED BY 'new_password';

### 锁

查看表是否锁

SHOW OPEN TABLES WHERE `Table` = 't_rr' AND `Database` = 'test_sql';

查看引擎状态

SHOW ENGINE INNODB STATUS;

设置隔离级别；

set global TRANSACTION ISOLATION level read COMMITTED;

SET SESSION TRANSACTION ISOLATION LEVEL REPEATABLE READ;

SHOW VARIABLES LIKE 'transaction_isolation';

RC 读已提交 有不可重复读的问题 即A修改了值 提交后 B读A提交前的值和提交后的值不一致

RR 可重复度 解决不可重复读问题 即A修改了值 提交后 B读A提交前的值和提交后的值一致

#### RR级别下

但是我一个事务a，一个事务b，都是RR级别，我先在事务a里执行select 操作，然后我在b里新增了一条数据，然后提交，回到事务a，执行update操作后，执行select，发现出现了b新增的数据是怎么回事？

：因为update操作是加锁的 需要最新数据，所以重新生成了readview





DELETE FROM dataworks_qyztxx
WHERE id NOT IN (
    SELECT id FROM (
        SELECT id
        FROM dataworks_qyztxx
        WHERE (uniscid, record_time) IN (
            SELECT uniscid, MAX(record_time)
            FROM dataworks_qyztxx
            GROUP BY uniscid
        )
    ) as subquery
);解析