# Live SQL Zoo Study Guide

## Table of Contents

- [Live SQL Zoo Study Guide](#live-sql-zoo-study-guide)
  - [Table of Contents](#table-of-contents)
  - [**SELECT basics**](#select-basics)
  - [**SELECT from world**](#select-from-world)
  - [**SELECT from nobel**](#select-from-nobel)
  - [**SELECT in SELECT**](#select-in-select)
  - [**SUM and COUNT**](#sum-and-count)
  - [**JOIN**](#join)
  - [**More JOIN**](#more-join)
  - [**Using NULL**](#using-null)
  - [**Self JOIN**](#self-join)

## **SELECT basics**

| name        | continent | area    | population | gdp          |
| ----------- | --------- | ------- | ---------- | ------------ |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |


```sql
-- show the population of Germany
SELECT population FROM world 
  WHERE name = 'Germany'
```

| population |
| ---------- |
| 83149300   |

```sql
-- Show the name and the population for 'Sweden', 'Norway' and 'Denmark'
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

| name    | population |
| ------- | ---------- |
| Denmark | 5822763    |
| Norway  | 5367580    |
| Sweden  | 10338368   |

```sql
-- show the country and the population for countries with an population between 1,000,000 and 1,250,000
SELECT name, population FROM world
  WHERE population BETWEEN 1000000 AND 1250000
```

| name        | population |
| ----------- | ---------- |
| Bahrain     | 1234571    |
| Swaziland   | 1220000    |
| Timor-Leste | 1066409    |

```sql
-- shows the countries that start with Al
SELECT name, population FROM world
  WHERE name LIKE "Al%"
```

| name    | population |
| ------- | ---------- |
| Albania | 3200000    |
| Algeria | 32900000   |

```sql
-- shows the countries that end in A or L
SELECT name FROM world
  WHERE name LIKE '%a' OR 'l%'
```

```sql
SELECT name,length(name) FROM world
  WHERE length(name)=5 and region='Europe'
```

| name  | length(name) |
| ----- | ------------ |
| Italy | 5            |
| Malta | 5            |
| Spain | 5            |

```sql
SELECT name, area*2 FROM world WHERE population = 64000
```

| name    | area*2 |
| ------- | ------ |
| Andorra | 936    |


```sql
-- show the countries with an area larger than 50000 and a population smaller than 10000000
SELECT name, area, population FROM world
  WHERE area > 50000 AND population < 10000000
```

```sql
-- shows the population density of China, Australia, Nigeria and France
SELECT name, population/area FROM world
  WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
```

**[⬆ back to top](#table-of-contents)**

## **SELECT from world**

**[⬆ back to top](#table-of-contents)**

## **SELECT from nobel**

**[⬆ back to top](#table-of-contents)**

## **SELECT in SELECT**

**[⬆ back to top](#table-of-contents)**

## **SUM and COUNT**

**[⬆ back to top](#table-of-contents)**

## **JOIN**

**[⬆ back to top](#table-of-contents)**

## **More JOIN**

**[⬆ back to top](#table-of-contents)**

## **Using NULL**

**[⬆ back to top](#table-of-contents)**

## **Self JOIN**

**[⬆ back to top](#table-of-contents)**
