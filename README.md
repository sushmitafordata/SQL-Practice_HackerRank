# SQL-Practice_HackerRank

#### BASIC - SELECT

1.Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.
```
select *
from city
where countrycode="USA" and population >100000
```

2.Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

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
