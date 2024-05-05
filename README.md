# SQL-Practice_HackerRank

### SELECT

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
