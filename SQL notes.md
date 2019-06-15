## SQL NOTE

### 1. SELECT

__SELECT__ * FROM table_name

#### Keyword: DISTINCT

SELECT __DISTINCT__ column_name FROM table_name

### 2. WHERE

SELECT column_name FROM table_name __WHERE__ column_name operator value

| operator | description              |
| -------- | ------------------------ |
| =        | 等于                     |
| <>       | 不等于                   |
| >        | 大于                     |
| <        | 小于                     |
| >=       | 大于等于                 |
| <=       | 小于等于                 |
| BETWEEN  | 范围内                   |
| LIKE     | 搜索某种模式             |
| IN       | 指定针对某列的多个可能值 |

### 3. AND&OR

### 4. ORDER BY

SELECT column_name FROM table_name __ORDER BY__ column_name ASC|DESC, column2_name

### 5. INSERT INTO

__INSERT INTO__ table_name VALUES (value1, value2, value3, ...)

__INSERT INTO__ table_name (column1, column2, column3, …) VALUES (value1, value2, value3, ...)

### 6. UPDATE

UPDATE *table_name*
SET *column1*=*value1*,*column2*=*value2*,...
WHERE *some_column*=*some_value*;

### 7. DELETE

DELETE FROM *table_name*
WHERE *some_column*=*some_value*;

