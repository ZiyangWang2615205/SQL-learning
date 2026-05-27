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



