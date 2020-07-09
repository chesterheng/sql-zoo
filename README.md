# Live SQL Zoo Study Guide

## Table of Contents

- [Live SQL Zoo Study Guide](#live-sql-zoo-study-guide)
  - [Table of Contents](#table-of-contents)
  - [**SQL Guide**](#sql-guide)
  - [**SELECT basics**](#select-basics)
  - [**SELECT Quiz**](#select-quiz)
  - [**SELECT from world**](#select-from-world)
  - [**SELECT from nobel**](#select-from-nobel)
  - [**Using nested SELECT**](#using-nested-select)
  - [**SELECT in SELECT**](#select-in-select)
    - [List each country name where the population is larger than that of 'Russia'.](#list-each-country-name-where-the-population-is-larger-than-that-of-russia)
    - [Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.](#show-the-countries-in-europe-with-a-per-capita-gdp-greater-than-united-kingdom)
    - [List the name and continent of countries in the continents containing either Argentina or Australia.](#list-the-name-and-continent-of-countries-in-the-continents-containing-either-argentina-or-australia)
    - [Which country has a population that is more than Canada but less than Poland?](#which-country-has-a-population-that-is-more-than-canada-but-less-than-poland)
    - [Show the name and the population as a percentage of the population of Germany for each country in Europe](#show-the-name-and-the-population-as-a-percentage-of-the-population-of-germany-for-each-country-in-europe)
    - [Which countries have a GDP greater than every country in Europe?](#which-countries-have-a-gdp-greater-than-every-country-in-europe)
    - [Find the largest country (by area) in each continent](#find-the-largest-country-by-area-in-each-continent)
    - [List each continent and the name of the country that comes first alphabetically.](#list-each-continent-and-the-name-of-the-country-that-comes-first-alphabetically)
    - [Find the continents where all countries have a population <= 25000000.](#find-the-continents-where-all-countries-have-a-population--25000000)
    - [Some countries have populations more than three times that of any of their neighbours (in the same continent)](#some-countries-have-populations-more-than-three-times-that-of-any-of-their-neighbours-in-the-same-continent)
  - [**SUM and COUNT**](#sum-and-count)
    - [Total world population](#total-world-population)
    - [List of continents](#list-of-continents)
    - [GDP of Africa](#gdp-of-africa)
    - [Count the big countries](#count-the-big-countries)
    - [Baltic states population](#baltic-states-population)
    - [Counting the countries of each continent](#counting-the-countries-of-each-continent)
    - [Counting big countries in each continent](#counting-big-countries-in-each-continent)
    - [Counting big continents](#counting-big-continents)
  - [**JOIN**](#join)
    - [Basic SQL Join Types](#basic-sql-join-types)
  - [**More JOIN**](#more-join)
  - [**Using NULL**](#using-null)
  - [**Self JOIN**](#self-join)

## **SQL Guide**

- [SQL Zoo](https://sqlzoo.net/wiki/SELECT_basics)
- [SQL PD](https://sqlpd.com)

| Table                           | Keywords | Filters & Values                                                           |
| ------------------------------- | -------- | -------------------------------------------------------------------------- |
| SELECT (columns and processed)  | DISTINCT | Binary Numeric and string comparison operator: =, <, <=, >, >=, !=, <>, () |
| FROM (table)                    | LIMIT    | Add ALL or ANY when right side of the operator have multiple values        |
| WHERE (filter rows, then group) | ASC      | List one value: = value                                                    |
| GROUP BY                        | DESC     | List many values: IN (value1, value2, ...)                                 |
| HAVING (filter groups)          |          | Inclusive ranges: BETWEEN min AND max                                      |
| ORDER BY (sort rows)            |          | Logical Operators: NOT, AND, OR, XOR                                       |

- The WHERE clause is applied before the GROUP BY clause.
- The WHERE clause applies the condition to individual rows before the rows are summarized into groups by the GROUP BY clause.

- The HAVING clause is applied after the GROUP BY clause.
- The HAVING clause applies the condition to the groups after the rows are grouped into groups.

## **SELECT basics**

world Table

| name        | continent | area    | population | gdp          |
| ----------- | --------- | ------- | ---------- | ------------ |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |


```sql
-- show the population of Germany
SELECT population 
FROM world 
WHERE name = 'Germany'
```

| population |
| ---------- |
| 83149300   |

```sql
-- Show the name and the population for 'Sweden', 'Norway' and 'Denmark'
SELECT name, population 
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

| name    | population |
| ------- | ---------- |
| Denmark | 5822763    |
| Norway  | 5367580    |
| Sweden  | 10338368   |

```sql
-- show the country and the area for countries with an area between 200,000 and 250,000
SELECT name, area 
FROM world
WHERE area BETWEEN 200000 AND 250000
```

| name    | area           |
| ------- | -------------- |
| Belarus | 207600         |
| Ghana   | 238533         |
| Guinea  | 245857         |
| Guyana  | 214969         |
| Laos    | 236800         |
| Romania | 238391         |
| Uganda  | 241550         |
| United  | Kingdom	242900 |

**[⬆ back to top](#table-of-contents)**

## **SELECT Quiz**

world Table

| name        | region      | area    | population | gdp         |
| ----------- | ----------- | ------- | ---------- | ----------- |
| Afghanistan | South Asia  | 652225  | 26000000   |             |
| Albania     | Europe      | 28728   | 3200000    | 6656000000  |
| Algeria     | Middle East | 2400000 | 32900000   | 75012000000 |
| Andorra     | Europe      | 468     | 64000      |             |

```sql
SELECT name, population
FROM world
WHERE population BETWEEN 1000000 AND 1250000
```

| name        | population |
| ----------- | ---------- |
| Bahrain     | 1234571    |
| Swaziland   | 1220000    |
| Timor-Leste | 1066409    |

```sql
SELECT name, population 
FROM world
WHERE name LIKE "Al%"
```

| name    | population |
| ------- | ---------- |
| Albania | 3200000    |
| Algeria | 32900000   |

```sql
-- shows the countries that end in A or L
SELECT name 
FROM world
WHERE name LIKE '%a' OR 'l%'
```

```sql
SELECT name,LENGTH(name) 
FROM world
WHERE length(name)=5 and region='Europe'
```

| name  | length(name) |
| ----- | ------------ |
| Italy | 5            |
| Malta | 5            |
| Spain | 5            |

```sql
SELECT name, area*2 
FROM world 
WHERE population = 64000
```

| name    | area*2 |
| ------- | ------ |
| Andorra | 936    |


```sql
-- show the countries with an area larger than 50000 and a population smaller than 10000000
SELECT name, area, population 
FROM world
WHERE area > 50000 AND population < 10000000
```

```sql
-- shows the population density of China, Australia, Nigeria and France
SELECT name, population/area 
FROM world
WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
```

**[⬆ back to top](#table-of-contents)**

## **SELECT from world**

| name        | continent | area    | population | gdp          |
| ----------- | --------- | ------- | ---------- | ------------ |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

```sql
-- show the name, continent and population of all countries
SELECT name, continent, population 
FROM world
```

| name        | continent | population |
| ----------- | --------- | ---------- |
| Afghanistan | Asia      | 25500100   |
| Albania     | Europe    | 2831741    |
| Algeria     | Africa    | 37100000   |
| Andorra     | Europe    | 78115      |
| Angola      | Africa    | 20609294   |

```sql
-- Show the name for the countries that have a population of at least 200 million
SELECT name 
FROM world
WHERE population >= 200000000
```

| name          |
| ------------- |
| Brazil        |
| China         |
| India         |
| Indonesia     |
| Nigeria       |
| Pakistan      |
| United States |

```sql
-- Give the name and the per capita GDP for those countries with a population of at least 200 million
SELECT name, gdp/population as 'per capita GDP' 
FROM world
WHERE population >= 200000000
```

| name          | per capita GDP |
| ------------- | -------------- |
| Brazil        | 9721.37        |
| China         | 8724.3064      |
| India         | 1891.7811      |
| Indonesia     | 3804.7723      |
| Nigeria       | 1822.8862      |
| Pakistan      | 1377.0363      |
| United States | 59121.1921     |

```sql
-- Show the name and population in millions for the countries of the continent 'South America'
SELECT name, population/1000000 as 'population in millions' 
FROM world
WHERE continent = 'South America'
```

| name                             | population in millions |
| -------------------------------- | ---------------------- |
| Argentina                        | 44.9387                |
| Bolivia                          | 11.4699                |
| Brazil                           | 211.4426               |
| Chile                            | 19.1072                |
| Colombia                         | 49.3957                |
| Ecuador                          | 17.4729                |
| Guyana                           | 0.7828                 |
| Paraguay                         | 7.2527                 |
| Peru                             | 32.1314                |
| Saint Vincent and the Grenadines | 0.1106                 |
| Suriname                         | 0.5814                 |
| Uruguay                          | 3.5186                 |
| Venezuela                        | 32.2195                |

```sql
-- Show the name and population for France, Germany, Italy
SELECT name, population 
FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```

| name    | population |
| ------- | ---------- |
| France  | 67076000   |
| Germany | 83149300   |
| Italy   | 60238522   |

```sql
-- Show the countries which have a name that includes the word 'United'
SELECT name 
FROM world
WHERE name LIKE '%United%'
```

| name                 |
| -------------------- |
| United Arab Emirates |
| United Kingdom       |
| United States        |

```sql
-- Show the countries that are big by area or big by population. 
-- Show name, population and area
SELECT name, population, area 
FROM world
WHERE area > 3000000 OR population > 250000000
```

| name          | population | area     |
| ------------- | ---------- | -------- |
| Australia     | 25690023   | 7692024  |
| Brazil        | 211442625  | 8515767  |
| Canada        | 38007166   | 9984670  |
| China         | 1402378640 | 9596961  |
| India         | 1361503224 | 3166414  |
| Indonesia     | 266911900  | 1904569  |
| Russia        | 146745098  | 17125242 |
| United States | 329583916  | 9826675  |


```sql
-- Exclusive OR (XOR)
-- Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both
-- Show name, population and area.
SELECT name, population, area 
FROM world
WHERE area > 3000000 XOR population > 250000000
```

| name      | population | areav    |
| --------- | ---------- | -------- |
| Australia | 25690023   | 7692024  |
| Brazil    | 211442625  | 8515767  |
| Canada    | 38007166   | 9984670  |
| Indonesia | 266911900  | 1904569  |
| Russia    | 146745098  | 17125242 |

```sql
-- For South America show population in millions and GDP in billions both to 2 decimal places
SELECT 
  name, 
  ROUND(population/1000000, 2) as 'population in millions', 
  ROUND(gdp/1000000000, 2) as 'GDP in billions'  
FROM world
WHERE  continent = 'South America'
```

| name                             | population in millions | GDP in billions |
| -------------------------------- | ---------------------- | --------------- |
| Argentina                        | 44.94                  | 637.49          |
| Bolivia                          | 11.47                  | 37.51           |
| Brazil                           | 211.44                 | 2055.51         |
| Chile                            | 19.11                  | 277.08          |
| Colombia                         | 49.4                   | 309.19          |
| Ecuador                          | 17.47                  | 104.3           |
| Guyana                           | 0.78                   | 3.09            |
| Paraguay                         | 7.25                   | 29.44           |
| Peruv	32.13                      | 211.4                  |
| Saint Vincent and the Grenadines | 0.11                   | 0.73            |
| Suriname                         | 0.58                   | 5.21            |
| Uruguay                          | 3.52                   | 59.18           |
| Venezuela                        | 32.22                  | 255.09          |

```sql
-- Show per-capita GDP for the trillion dollar countries to the nearest $1000
SELECT name, ROUND(gdp/population, -3) as 'per-capita GDP' 
FROM world
WHERE gdp >= 1000000000000
```

| name           | per-capita GDP |
| -------------- | -------------- |
| Australia      | 55000          |
| Brazil         | 10000          |
| Canada         | 43000          |
| China          | 9000           |
| France         | 39000          |
| Germany        | 44000          |
| India          | 2000           |
| Indonesia      | 4000           |
| Italy          | 32000          |
| Japan          | 39000          |
| Mexico         | 9000           |
| Russia         | 10000          |
| South Korea    | 22000          |
| Spain          | 28000          |
| United Kingdom | 40000          |
| United States  | 59000          |


```sql
-- Show the name and capital where the name and the capital have the same number of characters
SELECT name, capital 
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```

| name       | capital    |
| ---------- | ---------- |
| Algeria    | Algiers    |
| Angola     | Luanda     |
| Armenia    | Yerevan    |
| Botswana   | Gaborone   |
| Cameroon   | Yaoundé    |
| Canada     | Ottowa     |
| Djibouti   | Djibouti   |
| Egypt      | Cairo      |
| Estonia    | Tallinn    |
| Fiji       | Suva       |
| Gambia     | Banjul     |
| Georgia    | Tbilisi    |
| Ghana      | Accra      |
| Greece     | Athens     |
| Luxembourg | Luxembourg |
| Mauritania | Nouakchott |
| Peru       | Lima       |
| Poland     | Warsaw     |
| Russia     | Moscow     |
| Rwanda     | Kigali     |
| San Marino | San Marino |
| Singapore  | Singapore  |
| Taiwan     | Taipei     |
| Turkey     | Ankara     |
| Zambia     | Lusaka     |

```sql
-- Show the name and the capital where the first letters of each match
-- Don't include countries where the name and the capital are the same word
SELECT name, capital 
FROM world 
where LEFT(name,1) = left(capital,1) AND name <> capital
```
| name                  | capital                   |
| --------------------- | ------------------------- |
| Algeria               | Algiers                   |
| Andorra               | Andorra la Vella          |
| Barbados              | Bridgetown                |
| Belize                | Belmopan                  |
| Brazil                | Brasília                  |
| Brunei                | Bandar Seri Begawan       |
| Burundi               | Bujumbura                 |
| Guatemala             | Guatemala City            |
| Guyana                | Georgetown                |
| Kuwait                | Kuwait City               |
| Maldives              | Malé                      |
| Marshall Islands      | Majuro                    |
| Mexico                | Mexico City               |
| Monaco                | Monaco-Ville              |
| Mozambique            | Maputo                    |
| Niger                 | Niamey                    |
| Panama                | Panama City               |
| Papua New Guinea      | Port Moresby              |
| Sao Tomé and Príncipe | São Tomé                  |
| South Korea           | Seoul                     |
| Sri Lanka             | Sri Jayawardenepura Kotte |
| Sweden                | Stockholm                 |
| Taiwan                | Taipei                    |
| Tunisia               | Tunis                     |

```sql
-- Find the country that has all the vowels and no spaces in its name
SELECT name 
FROM world
WHERE 
  name LIKE '%a%' AND 
  name LIKE '%e%' AND 
  name LIKE '%i%' AND 
  name LIKE '%o%' AND 
  name LIKE '%u%' AND 
  name NOT LIKE '% %'
```

| name       |
| ---------- |
| Mozambique |

**[⬆ back to top](#table-of-contents)**

## **SELECT from nobel**

nobel Table

| yr   | subject    | winner                      |
| ---- | ---------- | --------------------------- |
| 1960 | Chemistry  | Willard F. Libby            |
| 1960 | Literature | Saint-John Perse            |
| 1960 | Medicine   | Sir Frank Macfarlane Burnet |
| 1960 | Medicine   | Peter Madawar               |

```sql
-- Change the query shown so that it displays Nobel prizes for 1950
SELECT yr, subject, winner 
FROM nobel
WHERE yr = 1950
```

| yr   | subject    | winner            |
| ---- | ---------- | ----------------- |
| 1950 | Chemistry  | Kurt Alder        |
| 1950 | Chemistry  | Otto Diels        |
| 1950 | Literature | Bertrand Russell  |
| 1950 | Medicine   | Philip S. Hench   |
| 1950 | Medicine   | Edward C. Kendall |
| 1950 | Medicine   | Tadeus Reichstein |
| 1950 | Peace      | Ralph Bunche      |
| 1950 | Physics    | Cecil Powell      |

```sql
-- Show who won the 1962 prize for Literature
SELECT winner
FROM nobel
WHERE yr = 1960 AND subject = 'Physics'
```

| winner         |
| -------------- |
| John Steinbeck |

```sql
-- Show the year and subject that won 'Albert Einstein' his prize.
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

| yr   | subject |
| ---- | ------- |
| 1921 | Physics |


```sql
-- Give the name of the 'Peace' winners since the year 2000, including 2000.
SELECT winner
FROM nobel
WHERE 
  subject ='Peace' AND 
  yr >= 2000
```

| winner                                    |
| ----------------------------------------- |
| Tunisian National Dialogue Quartet        |
| Kailash Satyarthi                         |
| Malala Yousafzai                          |
| European Union                            |
| Ellen Johnson Sirleaf                     |
| Leymah Gbowee                             |
| Tawakel Karman                            |
| Liu Xiaobo                                |
| Barack Obama                              |
| Martti Ahtisaari                          |
| Intergovernmental Panel on Climate Change |
| Al Gore                                   |
| Grameen Bank                              |
| Muhammad Yunus                            |
| International Atomic Energy Agency        |
| Mohamed ElBaradei                         |
| Wangari Maathai                           |
| Shirin Ebadi                              |
| Jimmy Carter                              |
| United Nations                            |
| Kofi Annan                                |
| Kim Dae-jung                              |

```sql
-- Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive
SELECT * 
FROM nobel
WHERE 
  yr BETWEEN 1980 AND 1989 AND 
  subject='Literature'
```

| yr   | subject    | winner                 |
| ---- | ---------- | ---------------------- |
| 1989 | Literature | Camilo José Cela       |
| 1988 | Literature | Naguib Mahfouz         |
| 1987 | Literature | Joseph Brodsky         |
| 1986 | Literature | Wole Soyinka           |
| 1985 | Literature | Claude Simon           |
| 1984 | Literature | Jaroslav Seifert       |
| 1983 | Literature | William Golding        |
| 1982 | Literature | Gabriel García Márquez |
| 1981 | Literature | Elias Canetti          |
| 1980 | Literature | Czeslaw Milosz         |

```sql
-- Show all details of the presidential winners:
-- Theodore Roosevelt
-- Woodrow Wilson
-- Jimmy Carter
-- Barack Obama
SELECT * 
FROM nobel
WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter','Barack Obama')
```

| yr   | subject | winner             |
| ---- | ------- | ------------------ |
| 2009 | Peace   | Barack Obama       |
| 2002 | Peace   | Jimmy Carter       |
| 1919 | Peace   | Woodrow Wilson     |
| 1906 | Peace   | Theodore Roosevelt |

```sql
-- Show the winners with first name John  
SELECT winner 
FROM nobel
WHERE winner LIKE 'John %'
```

| winner            |
| ----------------- |
| John O'Keefe      |
| John B. Gurdon    |
| John C. Mather    |
| John L. Hall      |
| John B. Fenn      |
| John E. Sulston   |
| John Pople        |
| John Hume         |
| John E. Walker    |
| John C. Harsanyi  |
| John F. Nash Jr.  |
| John C. Polanyi   |
| John R. Vane      |
| John H. van Vleck |
| John Cornforth    |
| John R. Hicks     |
| John Bardeen      |
| John C. Kendrew   |
| John Steinbeck    |
| John Bardeen      |
| John F. Enders    |
| John Cockcroft    |
| John H. Northrop  |
| John R. Mott      |
| John Galsworthy   |
| John Macleod      |

```sql
-- Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984
SELECT *
FROM nobel
WHERE 
  (subject = 'Physics' AND yr = 1980) OR 
  (subject = 'Chemistry' AND yr = 1984)
```

| yr   | subject   | winner           |
| ---- | --------- | ---------------- |
| 1984 | Chemistry | Bruce Merrifield |
| 1980 | Physics   | James Cronin     |
| 1980 | Physics   | Val Fitch        |

```sql
-- Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine
SELECT * 
FROM nobel
WHERE 
  yr = 1980 AND 
  subject <>'Chemistry' AND 
  subject <>'Medicine'
```

| yr   | subject    | winner                |
| ---- | ---------- | --------------------- |
| 1980 | Economics  | Lawrence R. Klein     |
| 1980 | Literature | Czeslaw Milosz        |
| 1980 | Peace      | Adolfo Pérez Esquivel |
| 1980 | Physics    | James Cronin          |
| 1980 | Physics    | Val Fitch             |

```sql
-- Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)
SELECT *
FROM nobel
WHERE
  (yr < 1910 AND subject ='Medicine') OR 
  (yr >= 2004 AND subject ='Literature') 
```

| yr   | subject    | winner                       |
| ---- | ---------- | ---------------------------- |
| 2015 | Literature | Svetlana Alexievich          |
| 2014 | Literature | Patrick Modiano              |
| 2013 | Literature | Alice Munro                  |
| 2012 | Literature | Mo Yan                       |
| 2011 | Literature | Tomas Tranströmer            |
| 2010 | Literature | Mario Vargas Llosa           |
| 2009 | Literature | Herta Müller                 |
| 2008 | Literature | Jean-Marie Gustave Le Clézio |
| 2007 | Literature | Doris Lessing                |
| 2006 | Literature | Orhan Pamuk                  |
| 2005 | Literature | Harold Pinter                |
| 2004 | Literature | Elfriede Jelinek             |
| 1909 | Medicine   | Theodor Kocher               |
| 1908 | Medicine   | Paul Ehrlich                 |
| 1908 | Medicine   | Ilya Mechnikov               |
| 1907 | Medicine   | Alphonse Laveran             |
| 1906 | Medicine   | Camillo Golgi                |
| 1906 | Medicine   | Santiago Ramón y Cajal       |
| 1905 | Medicine   | Robert Koch                  |
| 1904 | Medicine   | Ivan Pavlov                  |
| 1903 | Medicine   | Niels Ryberg Finsen          |
| 1902 | Medicine   | Ronald Ross                  |
| 1901 | Medicine   | Emil von Behring             |

```sql
-- Find all details of the prize won by PETER GRÜNBERG
SELECT *
FROM nobel
WHERE winner ='PETER GRÜNBERG'
```

| yr   | subject | winner         |
| ---- | ------- | -------------- |
| 2007 | Physics | Peter Grünberg |

```sql
-- Find all details of the prize won by EUGENE O'NEILL
SELECT *
FROM nobel
WHERE winner ='EUGENE O\'NEILL'
```

| yr   | subject    | winner         |
| ---- | ---------- | -------------- |
| 1936 | Literature | Eugene O'Neill |

```sql
-- List the winners, year and subject where the winner starts with Sir
-- Show the the most recent first, then by name order
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'sir%'
ORDER BY yr DESC, winner
```

| winner                      | yr   | subject   |
| --------------------------- | ---- | --------- |
| Sir Martin J. Evans         | 2007 | Medicine  |
| Sir Peter Mansfield         | 2003 | Medicine  |
| Sir Paul Nurse              | 2001 | Medicine  |
| Sir Harold Kroto            | 1996 | Chemistry |
| Sir James W. Black          | 1988 | Medicine  |
| Sir Arthur Lewis            | 1979 | Economics |
| Sir Nevill F. Mott          | 1977 | Physics   |
| Sir Bernard Katz            | 1970 | Medicine  |
| Sir John Eccles             | 1963 | Medicine  |
| Sir Frank Macfarlane Burnet | 1960 | Medicine  |
| Sir Cyril Hinshelwood       | 1956 | Chemistry |
| Sir Robert Robinson         | 1947 | Chemistry |
| Sir Alexander Fleming       | 1945 | Medicine  |
| Sir Howard Florey           | 1945 | Medicine  |
| Sir Henry Dale              | 1936 | Medicine  |
| Sir Norman Angell           | 1933 | Peace     |
| Sir Charles Sherrington     | 1932 | Medicine  |
| Sir Venkata Raman           | 1930 | Physics   |
| Sir Frederick Hopkins       | 1929 | Medicine  |
| Sir Austen Chamberlain      | 1925 | Peace     |
| Sir William Ramsay          | 1904 | Chemistry |

```sql
-- The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1. Is a boolean value
-- subject IN ('Physics','Chemistry') => 'Physics': 1, 'Chemistry': 1, rest: 0
-- Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('Physics','Chemistry'), subject, winner
```

| winner              | subject    |
| ------------------- | ---------- |
| Richard Stone       | Economics  |
| Jaroslav Seifert    | Literature |
| César Milstein      | Medicine   |
| Georges J.F. Köhler | Medicine   |
| Niels K. Jerne      | Medicine   |
| Desmond Tutu        | Peace      |
| Bruce Merrifield    | Chemistry  |
| Carlo Rubbia        | Physics    |
| Simon van der Meer  | Physics    |

**[⬆ back to top](#table-of-contents)**

## **Using nested SELECT**

world Table

| name        | continent | area    | population | gdp          |
| ----------- | --------- | ------- | ---------- | ------------ |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

```sql
-- List each country in the same continent as 'Brazil'.
SELECT continent
FROM world
WHERE name = 'Brazil'

SELECT name
FROM world
WHERE continent = (SELECT continent FROM world WHERE name = 'Brazil')
```

| continent     |
| ------------- |
| South America |

| name                             |
| -------------------------------- |
| Argentina                        |
| Bolivia                          |
| Brazil                           |
| Chile                            |
| Colombia                         |
| Ecuador                          |
| Guyana                           |
| Paraguay                         |
| Peru                             |
| Saint Vincent and the Grenadines |
| Suriname                         |
| Uruguay                          |
| Venezuela                        |

```sql
-- List each country and its continent in the same continent as 'Brazil' or 'Mexico'.
SELECT continent
FROM world
WHERE name='Brazil' OR name='Mexico'

SELECT name, continent
FROM world
WHERE continent IN (SELECT continent FROM world WHERE name='Brazil' OR name='Mexico')
```

| continent     |
| ------------- |
| South America |
| North America |

| name                             | continent     |
| -------------------------------- | ------------- |
| Argentina                        | South America |
| Bolivia                          | South America |
| Brazil                           | South America |
| Chile                            | South America |
| Colombia                         | South America |
| Ecuador                          | South America |
| Guyana                           | South America |
| Paraguay                         | South America |
| Peru                             | South America |
| Saint Vincent and the Grenadines | South America |
| Suriname                         | South America |
| Uruguay                          | South America |
| Venezuela                        | South America |
| Belize                           | North America |
| Canada                           | North America |
| Costa Rica                       | North America |
| El Salvador                      | North America |
| Guatemala                        | North America |
| Honduras                         | North America |
| Mexico                           | North America |
| Nicaragua                        | North America |
| Panama                           | North America |
| Saint Kitts and Nevis            | North America |
| United States                    | North America |

```sql
-- Show the population of China as a multiple of the population of the United Kingdom
SELECT population
FROM world
WHERE name='United Kingdom'

SELECT population/(SELECT population FROM world WHERE name='United Kingdom') 
AS 'population of China/population of United Kingdom'
FROM world
WHERE name = 'China'
```

| population |
| ---------- |
| 66435550   |

| population of China/population of United Kingdom |
| ------------------------------------------------ |
| 21.1089                                          |

```sql
-- Show each country that has a population greater than the population of ALL countries in Europe.
SELECT population
FROM world
WHERE continent='Europe'

SELECT name
FROM world
WHERE population > ALL (SELECT population FROM world WHERE continent='Europe')
```

| name          |
| ------------- |
| Bangladesh    |
| Brazil        |
| China         |
| Egypt         |
| Ethiopia      |
| India         |
| Indonesia     |
| Iran          |
| Japan         |
| Mexico        |
| Nigeria       |
| Pakistan      |
| Philippines   |
| Russia        |
| Turkey        |
| United States |
| Vietnam       |

**[⬆ back to top](#table-of-contents)**

## **SELECT in SELECT**

world Table

| name        | continent | area    | population | gdp          |
| ----------- | --------- | ------- | ---------- | ------------ |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

**[⬆ back to top](#table-of-contents)**

### List each country name where the population is larger than that of 'Russia'.

```sql
-- List each country name where the population is larger than that of 'Russia'.
SELECT name 
FROM world
WHERE population > (SELECT population FROM world WHERE name='Russia')
```

| name          |
| ------------- |
| Bangladesh    |
| Brazil        |
| China         |
| India         |
| Indonesia     |
| Nigeria       |
| Pakistan      |
| United States |

**[⬆ back to top](#table-of-contents)**

### Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

```sql
-- Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
SELECT name 
FROM world
WHERE 
  continent = 'Europe' AND 
  gdp/population > (SELECT gdp/population FROM world WHERE name='United Kingdom') 
```

| name          |
| ------------- |
| Andorra       |
| Austria       |
| Belgium       |
| Denmark       |
| Finland       |
| Germany       |
| Iceland       |
| Ireland       |
| Liechtenstein |
| Luxembourg    |
| Monaco        |
| Netherlands   |
| Norway        |
| San Marino    |
| Sweden        |
| Switzerland   |

**[⬆ back to top](#table-of-contents)**

### List the name and continent of countries in the continents containing either Argentina or Australia.

```sql
-- List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
SELECT name, continent 
FROM world 
WHERE 
  continent = (SELECT continent FROM world WHERE name = 'Argentina') OR 
  continent = (SELECT continent FROM world WHERE name = 'Australia') 
ORDER by name
```

| name                             | continent     |
| -------------------------------- | ------------- |
| Argentina                        | South America |
| Australia                        | Oceania       |
| Bolivia                          | South America |
| Brazil                           | South America |
| Chile                            | South America |
| Colombia                         | South America |
| Ecuador                          | South America |
| Fiji                             | Oceania       |
| Guyana                           | South America |
| Kiribati                         | Oceania       |
| Marshall Islands                 | Oceania       |
| Micronesia, Federated States of  | Oceania       |
| Nauru                            | Oceania       |
| New Zealand                      | Oceania       |
| Palau                            | Oceania       |
| Papua New Guinea                 | Oceania       |
| Paraguay                         | South America |
| Peru                             | South America |
| Saint Vincent and the Grenadines | South America |
| Samoa                            | Oceania       |
| Solomon Islands                  | Oceania       |
| Suriname                         | South America |
| Tonga                            | Oceania       |
| Tuvalu                           | Oceania       |
| Uruguay                          | South America |
| Vanuatu                          | Oceania       |
| Venezuela                        | South America |

**[⬆ back to top](#table-of-contents)**

### Which country has a population that is more than Canada but less than Poland? 

```sql
-- Which country has a population that is more than Canada but less than Poland? 
-- Show the name and the population.
SELECT name, population 
FROM world 
WHERE 
  population > (SELECT population FROM world WHERE name = 'Canada') AND 
  population < (SELECT population FROM world WHERE name = 'Poland')
```

| name | population |
| ---- | ---------- |

**[⬆ back to top](#table-of-contents)**

### Show the name and the population as a percentage of the population of Germany for each country in Europe

```sql
-- Show the name and the population of each country in Europe. 
-- Show the population as a percentage of the population of Germany.
SELECT 
  name, 
  CONCAT(ROUND(population/(SELECT population FROM world WHERE name = 'Germany')*100,0), '%') AS percentage
FROM world 
WHERE continent = 'Europe' 
```

| name                   | percentage |
| ---------------------- | ---------- |
| Albania                | 3%         |
| Andorra                | 0%         |
| Austria                | 11%        |
| Belarus                | 11%        |
| Belgium                | 14%        |
| Bosnia and Herzegovina | 4%         |
| Bulgaria               | 8%         |
| Croatia                | 5%         |
| Czech Republic         | 13%        |
| Denmark                | 7%         |
| Estonia                | 2%         |
| Finland                | 7%         |
| France                 | 81%        |
| Germany                | 100%       |
| Greece                 | 13%        |
| Hungary                | 12%        |
| Iceland                | 0%         |
| Ireland                | 6%         |
| Italy                  | 72%        |
| Kazakhstan             | 22%        |
| Latvia                 | 2%         |
| Liechtenstein          | 0%         |
| Lithuania              | 3%         |
| Luxembourg             | 1%         |
| Malta                  | 1%         |
| Moldova                | 3%         |
| Monaco                 | 0%         |
| Montenegro             | 1%         |
| Netherlands            | 21%        |
| North Macedonia        | 2%         |
| Norway                 | 6%         |
| Poland                 | 46%        |
| Portugal               | 12%        |
| Romania                | 23%        |
| San Marino             | 0%         |
| Serbia                 | 8%         |
| Slovakia               | 7%         |
| Slovenia               | 3%         |
| Spain                  | 57%        |
| Sweden                 | 12%        |
| Switzerland            | 10%        |
| Ukraine                | 50%        |
| United Kingdom         | 80%        |
| Vatican City           | 0%         |

**[⬆ back to top](#table-of-contents)**

### Which countries have a GDP greater than every country in Europe?

```sql
-- Which countries have a GDP greater than every country in Europe?
SELECT name
FROM world
WHERE 
  gdp >= ALL(SELECT gdp FROM world WHERE continent = 'Europe' AND gdp > 0) AND 
  continent != 'Europe'
```

| name          |
| ------------- |
| China         |
| Japan         |
| United States |

**[⬆ back to top](#table-of-contents)**

### Find the largest country (by area) in each continent

```sql
-- Find the largest country (by area) in each continent
-- Show the continent, the name and the area.
SELECT continent, name, area 
FROM world x 
WHERE area >= ALL (SELECT area FROM world y WHERE y.continent=x.continent)
```

| continent     | name       | area     |
| ------------- | ---------- | -------- |
| Africa        | Algeria    | 2381741  |
| Oceania       | Australia  | 7692024  |
| South America | Brazil     | 8515767  |
| North America | Canada     | 9984670  |
| Asia          | China      | 9596961  |
| Caribbean     | Cuba       | 109884   |
| Europe        | Kazakhstan | 2724900  |
| Eurasia       | Russia     | 17125242 |

**[⬆ back to top](#table-of-contents)**

### List each continent and the name of the country that comes first alphabetically.

```sql
-- List each continent and the name of the country that comes first alphabetically.
SELECT continent, name
FROM world x
WHERE name <= ALL(SELECT name FROM world y WHERE y.continent = x.continent)
```

| continent     | name                |
| ------------- | ------------------- |
| Africa        | Algeria             |
| Asia          | Afghanistan         |
| Caribbean     | Antigua and Barbuda |
| Eurasia       | Armenia             |
| Europe        | Albania             |
| North America | Belize              |
| Oceania       | Australia           |
| South America | Argentina           |

**[⬆ back to top](#table-of-contents)**

### Find the continents where all countries have a population <= 25000000. 

```sql
-- Find the continents where all countries have a population <= 25000000. 
-- Then find the names of the countries associated with these continents. 
-- Show name, continent and population.
SELECT name, continent, population
FROM world x
WHERE 
  25000000 > ALL(SELECT population FROM world y WHERE x.continent = y.continent)
```

| name                | continent | population |
| ------------------- | --------- | ---------- |
| Antigua and Barbuda | Caribbean | 96453      |
| Bahamas             | Caribbean | 385340     |
| Barbados            | Caribbean | 287025     |
| Cuba                | Caribbean | 11209628   |
| Dominica            | Caribbean | 71808      |
| Dominican Republic  | Caribbean | 10358320   |
| Grenada             | Caribbean | 112003     |
| Haiti               | Caribbean | 11577779   |
| Jamaica             | Caribbean | 2726667    |
| Saint Lucia         | Caribbean | 178696     |
| Trinidad and Tobago | Caribbean | 1363985    |

**[⬆ back to top](#table-of-contents)**

### Some countries have populations more than three times that of any of their neighbours (in the same continent)

```sql
-- Some countries have populations more than three times that of any of their neighbours (in the same continent).
SELECT name, continent
FROM world x
WHERE 
  population > ALL(
    SELECT population*3 
    FROM world y 
    WHERE 
      x.continent = y.continent AND 
      y.population > 0 AND 
      y.name != x.name
    )
```

| name   | continent     |
| ------ | ------------- |
| Brazil | South America |
| Russia | Eurasia       |

**[⬆ back to top](#table-of-contents)**

## **SUM and COUNT**

world Table

| name        | continent | area    | population | gdp          |
| ----------- | --------- | ------- | ---------- | ------------ |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

**[⬆ back to top](#table-of-contents)**

### Total world population

```sql
-- Show the total population of the world.
SELECT SUM(population) AS 'total population'
FROM world
```

| total population |
| ---------------- |
| 7615648652       |

**[⬆ back to top](#table-of-contents)**

### List of continents

```sql
-- List all the continents - just once each.
SELECT DISTINCT(continent)
FROM world
```

| continent     |
| ------------- |
| Africa        |
| Asia          |
| Caribbean     |
| Eurasia       |
| Europe        |
| North America |
| Oceania       |
| South America |

**[⬆ back to top](#table-of-contents)**

### GDP of Africa

```sql
-- Give the total GDP of Africa
SELECT SUM(gdp) AS 'total GDP of Africa'
FROM world 
WHERE continent = 'Africa'
```

| total GDP of Africa |
| ------------------- |
| 1964824000000       |

**[⬆ back to top](#table-of-contents)**

### Count the big countries

```sql
-- How many countries have an area of at least 1000000
SELECT COUNT(area)
FROM world 
WHERE area >= 1000000
```

| COUNT(area) |
| ----------- |
| 29          |

**[⬆ back to top](#table-of-contents)**

### Baltic states population

```sql
-- What is the total population of ('Estonia', 'Latvia', 'Lithuania')
SELECT SUM(population) AS 'total population'
FROM world 
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```

| total population |
| ---------------- |
| 6028631          |

**[⬆ back to top](#table-of-contents)**

### Counting the countries of each continent

```sql
-- For each continent show the continent and number of countries.
SELECT continent, COUNT(name) AS number
FROM world 
GROUP BY continent
```

| continent     | number |
| ------------- | ------ |
| Africa        | 53     |
| Asia          | 47     |
| Caribbean     | 11     |
| Eurasia       | 2      |
| Europe        | 44     |
| North America | 11     |
| Oceania       | 14     |
| South America | 13     |

**[⬆ back to top](#table-of-contents)**

### Counting big countries in each continent

```sql
-- For each continent show the continent and number of countries with populations of at least 10 million.
SELECT continent, count(name)
FROM world 
WHERE population >= 10000000
GROUP BY continent
```

| continent     | number |
| ------------- | ------ |
| Africa        | 31     |
| Asia          | 26     |
| Caribbean     | 3      |
| Eurasia       | 1      |
| Europe        | 15     |
| North America | 4      |
| Oceania       | 1      |
| South America | 8      |

**[⬆ back to top](#table-of-contents)**

### Counting big continents

```sql
-- List the continents that have a total population of at least 100 million.
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000
```

| continent     |
| ------------- |
| Africa        |
| Asia          |
| Eurasia       |
| Europe        |
| North America |
| South America |

**[⬆ back to top](#table-of-contents)**

## **JOIN**

### Basic SQL Join Types

| customer_id | first_name | last_name  | email               | address                   | city            | state | zipcode |
| ----------- | ---------- | ---------- | ------------------- | ------------------------- | --------------- | ----- | ------- |
| 1           | George     | Washington | gwashington@usa.gov | 3200 Mt Vernon Hwy        | Mount Vernon    | VA    | 22121   |
| 2           | John       | Adams      | jadams@usa.gov      | 1250 Hancock St           | Quincy          | MA    | 02169   |
| 3           | Thomas     | Jefferson  | tjefferson@usa.gov  | 931 Thomas Jefferson Pkwy | Charlottesville | VA    | 22902   |
| 4           | James      | Madison    | jmadison@usa.gov    | 11350 Constitution Hwy    | Orange          | VA    | 22960   |
| 5           | James      | Monroe     | jmonroe@usa.gov     | 2050 James Monroe Parkway | Charlottesville | VA    | 22902   |

| order_id | order_date | amount  | customer_id |
| -------- | ---------- | ------- | ----------- |
| 1        | 07/04/1776 | $234.56 | 1           |
| 2        | 03/14/1760 | $78.50  | 3           |
| 3        | 05/23/1784 | $124.00 | 2           |
| 4        | 09/03/1790 | $65.50  | 3           |
| 5        | 07/21/1795 | $25.50  | 10          |
| 6        | 11/27/1787 | $14.40  | 9           |

```sql
-- Inner Join
select first_name, last_name, order_date, order_amount
from customers c
inner join orders o
on c.customer_id = o.customer_id
```

| first_name | last_name  | order_date | order_amount |
| ---------- | ---------- | ---------- | ------------ |
| George     | Washington | 07/04/1776 | $234.56      |
| John       | Adams      | 05/23/1784 | $124.00      |
| Thomas     | Jefferson  | 03/14/1760 | $78.50       |
| Thomas     | Jefferson  | 09/03/1790 | $65.50       |

```sql
-- Left Join
select first_name, last_name, order_date, order_amount
from customers c
left join orders o
on c.customer_id = o.customer_id
```

| first_name | last_name  | order_date | order_amount |
| ---------- | ---------- | ---------- | ------------ |
| George     | Washington | 07/04/1776 | $234.56      |
| John       | Adams      | 05/23/1784 | $124.00      |
| Thomas     | Jefferson  | 03/14/1760 | $78.50       |
| Thomas     | Jefferson  | 09/03/1790 | $65.50       |
| James      | Madison    | NULL       | NULL         |
| James      | Monroe     | NULL       | NULL         |

```sql
-- Right Join
select first_name, last_name, order_date, order_amount
from customers c
right join orders o
on c.customer_id = o.customer_id
```

| first_name | last_name  | order_date | order_amount |
| ---------- | ---------- | ---------- | ------------ |
| George     | Washington | 07/04/1776 | $234.56      |
| Thomas     | Jefferson  | 03/14/1760 | $78.50       |
| John       | Adams      | 05/23/1784 | $124.00      |
| Thomas     | Jefferson  | 09/03/1790 | $65.50       |
| NULL       | NULL       | 07/21/1795 | $25.50       |
| NULL       | NULL       | 11/27/1787 | $14.40       |

```sql
-- Full Join
select first_name, last_name, order_date, order_amount
from customers c
full join orders o
on c.customer_id = o.customer_id
```

| first_name | last_name  | order_date | order_amount |
| ---------- | ---------- | ---------- | ------------ |
| George     | Washington | 07/04/1776 | $234.56      |
| Thomas     | Jefferson  | 03/14/1760 | $78.50       |
| John       | Adams      | 05/23/1784 | $124.00      |
| Thomas     | Jefferson  | 09/03/1790 | $65.50       |
| NULL       | NULL       | 07/21/1795 | $25.50       |
| NULL       | NULL       | 11/27/1787 | $14.40       |
| James      | Madison    | NULL       | NULL         |
| James      | Monroe     | NULL       | NULL         |

**[⬆ back to top](#table-of-contents)**

## **More JOIN**

**[⬆ back to top](#table-of-contents)**

## **Using NULL**

**[⬆ back to top](#table-of-contents)**

## **Self JOIN**

**[⬆ back to top](#table-of-contents)**
select 	emp_name, dept_name
from employees
inner join departments
on employees.dept_id = departments.dept_id