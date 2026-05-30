---
title: SQL语言 - SQL语法基础
description: 按知识点整理 SELECT、DISTINCT、LIMIT、排序和过滤的常用写法。
date: 2026-05-30 14:30:00
permalink: sql-syntax-basic.html
categories:
  - SQL语言
tags:
  - SQL
  - 数据库
---

## SELECT

`SELECT` 用来从表中取出指定列。真实项目里建议明确列名，避免 `SELECT *` 带来不必要的数据传输和字段依赖。

```sql
SELECT id, name, created_at
FROM users;
```

## DISTINCT

相同值只会出现一次。它作用于所有列，也就是说所有列的值都相同才算相同。

```sql
SELECT DISTINCT col1, col2
FROM mytable;
```

## LIMIT

限制返回的行数。可以有两个参数，第一个参数为起始行，从 `0` 开始；第二个参数为返回的总行数。

返回前 5 行：

```sql
SELECT *
FROM mytable
LIMIT 5;
```

另一种等价写法：

```sql
SELECT *
FROM mytable
LIMIT 0, 5;
```

返回第 3 到第 5 行：

```sql
SELECT *
FROM mytable
LIMIT 2, 3;
```

## 排序

使用 `ORDER BY` 对查询结果排序。`ASC` 表示升序，`DESC` 表示降序。

```sql
SELECT id, name, score
FROM users
ORDER BY score DESC, id ASC;
```

## 过滤

`WHERE` 用来筛选行。多个条件可以通过 `AND`、`OR` 组合。

```sql
SELECT id, name, status
FROM users
WHERE status = 'active'
  AND created_at >= '2026-01-01';
```

## 分组

`GROUP BY` 常和聚合函数一起使用，例如 `COUNT`、`SUM`、`AVG`、`MAX`、`MIN`。

```sql
SELECT status, COUNT(*) AS total
FROM users
GROUP BY status;
```

## 过滤分组结果

`HAVING` 用来过滤分组后的结果，`WHERE` 用来过滤分组前的原始行。

```sql
SELECT status, COUNT(*) AS total
FROM users
GROUP BY status
HAVING COUNT(*) > 10;
```

> 记忆方式：`WHERE` 先过滤行，`GROUP BY` 再分组，`HAVING` 最后过滤分组。
