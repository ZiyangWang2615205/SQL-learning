# Day-01 Note

## SQL syntax

### Basic SQL syntax

```text
SELECT WHERE FROM 
```
这三者没有大小写敏感问题，比如SELECT和Select没有区别，但最好还是upper case

语句一般用；隔开，比如: ```SElECT * FROM table;```

对于string， 一般需要用''引用，：``` 'string' ```

### Create Database

```text
CREATE DATABASE test;
```

生成一个scheme，名为test

### Drop DataBase

```text
DROP DATABASE test;
```

会强制删除掉test的database，且里面的内容不会保存，不推荐使用

### Create Table

```text
CREATE TABLE test(
    test_column INT
);
```
这里创建了一个名为test的table，里面有一个test_column存储int类型的数据
变量名一般由字母和下划线组成，如果涉及到空格要写成；
```text
` test  column `
```
的形式

### Alter Table

```text
ALTER TABLE test
ADD another_column VARCHAR(255);
```
```ALTER``` 用与修改表结构，这里修改已经存在的table test，
```ADD``` 增加了一个column
VARCHAR(255)表示一个字符长度最多为255的文本

由于SQL每次读command都以；为划分，所以对于SQL来说：
```text
ALTER TABLE test
ADD another_column 
VARCHAR(255);
```
和上面的例子没有本质区别

### Drop Table

```text
DROP TABLE test;
```
删除名为test的table

### NOT NULL

```text
CREATE TABLE test(
    test_column INT NOT NULL
);
```
用于保证某个column里的数据一定为非null值

### AUTO_INCREMENT

```text
CREATE TABLE test(
    id INT NOT NULL AUTO_INCREMENT,
    test_column INT NOT NULL
);
```

每次添加数据，id会自增，**自增会从1开始**
注意各个不同的column之间以```,``` 作为分界点

### PRIMARY KEY

```text
CREATE TABLE test(
    id INT NOT NULL AUTO_INCREMENT,
    test_column INT NOT NULL,
    PRIMARY KEY(id)
);
```

即以id作为primary key，primary key确保每条记录的唯一性，绝对不会出现重复的primary key值
且primary key一定是非null的

### FOREIGN KEY

```text
CREATE TABLE test(
    subject_id INT NOT NULL AUTO_INCREMENT,
    test_column INT NOT NULL,
    student_id INT NOT NULL,
    PRIMARY KEY(subject_id),
    FOREIGN KEY(student_id) REFERENCES student(id) 
);

CREATE TABLE student(
    id INT NOT NULL AUTO_INCREMENT,
    test_column INT NOT NULL,
    PRIMARY KEY(id)
);
```

这里foreign key作为链接，链接两张表的字段，让test表中也能存储获取student id，并对应test的subject
foregin key的值可以重复，但一定是另一张表的primary key或者唯一标识，且当主表数据发生变化，foreign key会导致连锁反应

### INSERT INTO & VALUES

```text
CREATE TABLE bands(
    id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    release_year INT
)

INSERT INTO bands(name)
VALUES ('Deuces'), ('Ikun');

INSERT INTO bands (name, release_year)
VALUES ('Deuces', 2008),
       ('Ikun', 2022);
```
该指令用于向表中插入数据

### SELECT FROM

```text
SELECT * FROM bands //显示bands表中的所有column
SELECT name FROM bands//仅显示name colmun
SELECT * FROM bands LIMIT 2// 只显示起始2行信息

```

### AS

```text
SELECT name AS `my name`, id AS `Bands id` From bands
```
则在这一次查询过程中的变量名会分别被重命名，即别名，会显示my name和Bands id
但是实际上的bands表里的变量名仍然不变还是name和id

### ORDER BY

```text
SELECT * FROM bands ORDER BY name;
//升序
SELECT * FROM bands ORDER BY name ASC;
//降序
SELECT * FROM bands ORDER BY name DESC;
```
default情况下，直接order by name会呈现ASC的形式

### DISTINCT

```text
SELECT DISTINCT name FROM albums
```

这个时候会从 albums table中切出name这一栏，但是会把重复项去掉
比如有两个albums都叫ikun，他只会显示一个ikun

### UPDATE & SET

```text
UPDATE albums
SET release_year = 1982
```
这会让整个albums里的每一个元素的release_year都变为1982

### WHERE

```text
UPDATE albums
SET release_year = 1982
WHERE id = 1;
```
通过where关键词的使用，我们可以指定一个column改变变量，而不是整体改变，起到了filter的作用
我们还可以这样使用:

```text
SELECT * FROM albums
WHERE release_year < 2000;
```
输出release_year < 2000的albums

### LIKE

```text
SELECT * FROM albums
WHERE name LIKE '%er%'
```
会输出name column里任意位置有er连续出现的元素。
相似的：

```text
       %er -- 表示er结尾
       er% -- 表示er开头
       er -- 恰好为er
```

### AND & OR

```text
SELECT * FROM albums
WHERE name LIKE '%er%' AND band_id = 2;

SELECT * FROM albums
WHERE name LIKE '%er%' OR band_id = 2;
```
就像boolean一样，and输出两个条件都满足的结果，or输出任意一个条件满足的结果

### BETWEEN

```text
SELECT * FROM albums
WHERE release_year BETWEEN 2000 AND 2018;
```
则会输出release_year 2000 - 2018的结果，且2000和2018都包括，为闭区间

### IS NULL

```text
SELECT * FROM albums
WHERE release_year IS NULL;
```
输出release_year为null值

### DELETE FROM

```text
DELETE FROM albums WHERE id = 5;
```
会删除albums里id为5的row

### JOIN ON

```text
SELECT * FROM bands
JOIN albums ON bands.id = albums.band_id;
```
即只要bands table里的id = albums table里的band_id就把该row拼凑在一行
但是Join本身不会让bands_id和id合并，他们两个还是独立存在的
且由于你一开始select了bands，会让合并表里的bands元素出现在左边，albums出现在右边

#### INNER JOIN ON

```text
SELECT * FROM bands
INNER JOIN albums ON bands.id = albums.band_id;
```
inner join和原本的join没有区别，都是一一对应，然后没有对应元素的bands/albums我们会忽略，不显示

#### LEFT JOIN ON

```text
SELECT * FROM bands
LEFT JOIN albums ON bands.id = albums.band_id;
```
在这里会显示所有bands的元素，即使他没有对应的albums

#### RIGHT JOIN ON

```text
SELECT * FROM bands
RIGHT JOIN albums ON bands.id = albums.band_id;
```
会显示所有的albums元素，即使他没有对应的bands

### Aggregate function