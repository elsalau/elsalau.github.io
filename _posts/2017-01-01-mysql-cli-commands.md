---
layout: post
title:  "MySQL Basic"
category: mysql
date:  2017-01-01 12:17:36 +0800
category: mysql
---
## Default Databases

#### mysql

  - MySQL system database stores user accounts and privileges
  - Only administrator role can manage this database

#### information_schema

  - stores metadata of other databases in MySQL server

#### test

  - database for test purpose
  - every user has read/write privilege

## Basic Commands

#### Login MySQL using root account

```bash
  $ mysql -u root -p
  Enter password:
```

#### Create new database

```sql
  > create database <database_name>;

  Example:
  > create database sample;
```

#### Delete specific database

```sql
  > drop database [if exists] <database_name>;

  Example:
  > drop database sample;
```

#### Display all databases

```sql
  > show databases;
  +--------------------+
  | Database           |
  +--------------------+
  | sample             |
  | information_schema |
  | mysql              |
  | test               |
  +--------------------+
```

#### Use specific database

```sql
  > use <database_name>;

  Example:
  > use mysql;
  Database changed
```

#### Display all tables in current database

```sql
  > show tables;
  +-----------------+
  | Tables_in_mysql |
  +-----------------+
  | columns_priv    |
  | db              |
  | func            |
  | help_category   |
  | .               |
  | .               |
  | .               |
  +-----------------+
```

#### Create new table

```sql
  > create table <table_name>
    ( <column_name_1> <data_type> [constraints] [attribute],
      <column_name_2> <data_type> [constraints] [attribute],
      ...
      <column_name_n> <data_type> [constraints] [attribute]
    );

  Example:
  > create table table_1
    ( x int,
      y varchar(5),
      z datetime
    );
```

#### Create new table refer to an existing table

```sql
  > create table <table_name> like <source_table_name>;
```
- Note: The new table will copy columns from source table.
  Including names, types, constraints and attributes

#### Display table detail

```sql
  > desc <table_name>;

  Example:
  > desc table_1
  +-------+------------+------+-----+---------+
  | Field | Type       | Null | Key | Default |
  +-------+------------+------+-----+---------+
  | x     | int(11)    | Yes  |     | Null    |
  | y     | varchar(5) | Yes  |     | Null    |
  | z     | date       | Yes  |     | Null    |
  +-------+------------+------+-----+---------+
```

#### Rename a table

```sql
  > rename table <old_name> to <new_name>;

  or
  > alter table <old_name> rename to <new_name>;
```

#### Delete a table

```sql
  > drop table <table_name>;
```
