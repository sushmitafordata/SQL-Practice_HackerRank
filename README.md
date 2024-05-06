# SQL-Practice_HackerRank

## SELECT

**1.Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.**
```
select *
from city
where countrycode="USA" and population >100000
```

**2.Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.**

```
(select city,length(city) as len_c
from station
order by len_c desc,city
limit 1)
union
(select city,length(city) as len_c
from station
order by len_c ,city
limit 1)
```


**3.Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.**

```
select DISTINCT(city)
from station
where city LIKE "a%" OR  city LIKE"e%" OR city LIKE"i%" OR city LIKE "o%" OR city LIKE "u%";

-- Alt Approach--

select DISTINCT(city)
from station
where SUBSTR(city,1,1) in ('a','e','i','o','u')

```

**4.Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.**
```
select DISTINCT city
from station
where SUBSTR(city,-1,1) in ("a","e","i","o","u");
```

**5.Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.**
```
select distinct city
from station
where SUBSTR(city,1,1) in ('a','e','i','o','u')
AND
SUBSTR(city,-1,1) in ('a','e','i','o','u')
```
**6.Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.**
```
select distinct city
from station
where substr(city,1,1) NOT in ('a','e','i','o','u');
```

**7.Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.**
```
select distinct city 
from station
where substr(city,-1,1) not in ("a","e","i","o","u");

```
**8.Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.**
```
select distinct city
from station
where substr(city,1,1)  not in ("a","e","i","o","u")
OR
substr(city,-1,1)  not in ("a","e","i","o","u");
```

## AGGREGATION

**9.Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.**

```
select name 
from students
where marks >75
order by substr(name,-3,3),id

```
**10.Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id.**

```select name 
from Employee
where salary >2000 and months <10
order by employee_id asc;
```
**11.Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than . Round your answer to  decimal places.**
```
select round(LONG_W,4) 
from station
where LAT_N <137.2345
order by LAT_N desc
limit 1;
```
**12. Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. Round your answer to  decimal places**.

```
select round(LONG_W,4)
from station
where LAT_N >38.7780
order by LAT_N
limit 1;
```
