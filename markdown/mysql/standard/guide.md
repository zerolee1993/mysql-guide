# **你想做些什么？**

1. **[我想新建一张表](#我想新建一张表)**

2. **[我需要为已有表增加或修改字段](#我需要为已有表增加或修改字段)**

3. **[我需要为表建立或删除索引](#我需要为表建立或删除索引)**

4. **[我需要备份数据](#我需要备份数据)**

5. **[我要修改线上数据](#我要修改线上数据)**

6. **[我正在开发业务功能](#我正在开发业务功能)**

---

### **我想新建一张表**

**> 建表语句参考**

```sql
CREATE TABLE `table_name` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键',
  `column_name1` TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT 'tinyint 示例',
  `column_name2` INT UNSIGNED NOT NULL COMMENT 'int 示例',
  `column_name3` VARCHAR(100) NOT NULL DEFAULT '' COMMENT 'varchar 示例',
  `column_name4` DECIMAL(16,2) NOT NULL DEFAULT 0.00 COMMENT 'decimal 示例',
  `column_name5` DATETIME NOT NULL COMMENT 'datetime 示例',
  `is_deleted` TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '逻辑删除 (1：已删，0：未删)',
  `gmt_create` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_column_name` (`column_name`),
  KEY `idx_column_name` (`column_name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='表备注';
```

**> 需要注意的事项**

- 参考：[建表需要注意什么](standard-v1.0.md#建表需要注意什么？)

- 参考：[如何命名](standard-v1.0.md#如何命名？)

- 参考：[如何选择列的类型](standard-v1.0.md#如何选择列的类型？)

- 参考：[如何建立索引](standard-v1.0.md#如何建立索引？)

---

### **我需要为已有表增加或修改字段**

**> 需要注意的事项**

- 参考：[如何命名？](standard-v1.0.md#如何命名？)

- 参考：[如何选择列的类型？](standard-v1.0.md#如何选择列的类型？)

- 参考：[如何建立索引？](standard-v1.0.md#如何建立索引？)

- 修改字段时，将多个 `ALTER` 语句合并为一个执行

- 所有表和字段都要添加注释，修改字段含义或对字段表示的状态追加时，需要及时更新字段注释

---

### **我需要为表建立或删除索引**

**> 建立索引语句参考**

```sql
ALTER TABLE table_name ADD INDEX idx_column1_column2(`column1`,`column2`);
ALTER TABLE table_name ADD UNIQUE uk_column1_column2(`column1`,`column2`);
```

**> 删除索引语句参考**

```sql
ALTER TABLE table_name DROP INDEX idx_xxx;
```

**> 需要注意的事项**

- 参考：[如何建立索引？](standard-v1.0.md#如何建立索引？)

---

### **我需要备份数据**

**> 备份语句参考**

```sql
CREATE TABLE bak_table_name_yyyyMMdd  LIKE table_name;
ALTER TABLE bak_table_name_yyyyMMdd COMMENT 'xxxx备份，请保留至yyyyMMdd';
INSERT INTO bak_table_name_yyyyMMdd SELECT * FROM table_name [WHERE ...];
```

**> 需要注意的事项**

- 备份部分数据时，可以在 `INSERT` 语句最后增加 `WHERE` 条件
- 备份表必须以 `bak_` 为前缀，并以 `_yyyyMMdd` 实时日期为后缀。例如 `bak_test01_20190409`
- 最好将备份表更改备注，注明备份原因，及最后保留日期，方便清理

---

### **我要修改线上数据**

**> 需要注意的事项**

- 参考：[操作线上数据时需要注意什么？](standard-v1.0.md#操作线上数据时需要注意什么？)

---

### **我正在开发业务功能**

**> 需要注意的事项**

- 参考：[开发需要注意什么？](standard-v1.0.md#开发需要注意什么？)

