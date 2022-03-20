- 插入：
  ```sql
  INSERT INTO 基本表名 (字段名[,字段名]...)
  VALUES(常量[,常量]...); 查询语句
  INSERT INTO 基本表名 (列表名)
  SELECT 查询语句
  ```
  ```sql
  create view v_employees(number, name, age, sec, salary)
  as
  select number, name, age, sex, salary
  from employees
  where name='张三';
  - insert into v_employees
  values(001, '李力', 22, 'm', 2000)
  ```
- 删除：
  ```sql
  DELETE FROM 基本表名
  [WHERE 条件表达式]
  ```
- 修改：
  ```sql
  UPDATE 基本表名
  SET 列名=值表达式(,列名=值表达式...)
  [WHERE 条件表达式]
  ```
  ```sql
  update teachers
  set Salary = Salary * 1.05
  where Salary <= 1000
  ```