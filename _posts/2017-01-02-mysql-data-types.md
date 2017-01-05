---
layout: post
title:  "MySQL Data Type"
category: mysql
date:  2017-01-02 11:03:41 +0800
category: mysql
---

## Data Types

  - [Numeric Types](#numeric-types)
  - [Date and Time Types](#date-and-time-types)
  - [String Types](#string-types)
  - [Binary Types](#binary-types)
  - [Enum Types](#enum-types)
  - [Set Type](#set-type)

### Numberic Types

#### Integer Types

|    Type     |  Bytes  |                      Signed Range                      |         Unsigned Ranged        |
| :---------: | :-----: | :----------------------------------------------------: | :----------------------------: |
|   TINYINT   |    1    |                       -128 ~ 127                       | 0 ~ 255                        |
|   SMALLINT  |    2    |                    -32,768 ~ 32,767                    | 0 ~ 65535                      |
|  MEDIUMINT  |    3    |                 -8,388,608 ~ 8,388,607                 | 0 ~ 16,777,215                 |
|     INT     |    4    |             -2,148,483,648 ~ 2,148,483,647             | 0 ~ 4,294,967,295              |
|    BIGINT   |    8    | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 | 0 ~ 18,446,744,073,709,551,615 |

- Note: Integer Type will use signed range by default

#### Fixed-Point Types

- The `DECIMAL` and `NUMERIC` types store exact numeric data values.
- These types are used when it is important to preserve exact precision.

```sql
  DECIMAL(M, D)
```
- In standard SQL, the syntax DECIMAL(M) is equivalent to DECIMAL(M,0)
- The default value of M is 10

#### Floating-Point Types

|   Type    |  Bytes  |                      Signed Range                      |         Unsigned Ranged        |
| :-------: | :-----: | :----------------------------------------------------: | :----------------------------: |
|   FLOAT   |    4    |                       -3.                       | 0 ~ 255                        |
|   DOUBLE  |    8    |                    -32,768 ~ 32,767                    | 0 ~ 65535                      |

#### Bit-Value Type - BIT

#### Numeric Type Attributes

### Date and Time Types

### String Types

### Binary Types

### Enum Types

### Set Type

