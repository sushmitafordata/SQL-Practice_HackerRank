# SQL-Practice_HackerRank

#### BASIC - SELECT

1.Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.
```
select *
from city
where countrycode="USA" and population >100000
```