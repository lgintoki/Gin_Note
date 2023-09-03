## 一、由于删改表导致表的自增ID不连续

```mysql
问题：俩个表，A表由于删除过字段导致自增的id不连续，现在需要让id连续
解决：
-- 创建一个新表，与原始表的结构相同
CREATE TABLE new_table LIKE table_A;

-- 将 AUTO_INCREMENT 设置为新的初始值
SET @@auto_increment_increment=1;
SET @@auto_increment_offset=1;
SELECT @new_id := 0;

-- 插入数据，重新分配连续的 id
INSERT INTO new_table (column1, column2, ...)
SELECT column1, column2, ...
FROM table_A
ORDER BY id;

-- 修改新表的 id 列为连续的值
UPDATE new_table SET id = (@new_id := @new_id + 1);

-- 删除原始表，将新表重命名为原始表的名称
DROP TABLE table_A;
RENAME TABLE new_table TO table_A;
```

