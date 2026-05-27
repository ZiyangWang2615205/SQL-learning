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
