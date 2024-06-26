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
**Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's  key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.
Write a query calculating the amount of error (i.e.:  average monthly salaries), and round it up to the next integer.**

```
select
ceil(avg(salary)- round(avg(replace(salary,0,""))))
from employees

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



**1.Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:**

**Equilateral: It's a triangle with  sides of equal length.
Isosceles: It's a triangle with  sides of equal length.
Scalene: It's a triangle with  sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle.**

```
SELECT CASE
    WHEN (a + b > c AND a + c > b AND b + c > a) THEN
        CASE
            WHEN (a = b AND b = c) THEN 'Equilateral'
            WHEN (a = b OR b = c OR c = a) THEN 'Isosceles'
            ELSE 'Scalene'
        END
    ELSE 'Not A Triangle'
END AS triangle_type
FROM triangles;
```

**Generate the following two result sets:**

**Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:**

**There are a total of [occupation_count] [occupation]s.
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.**

```
SELECT CONCAT(NAME,'(',LEFT(OCCUPATION,1),')')
FROM OCCUPATIONS 
ORDER BY NAME ASC; 
SELECT CONCAT("There are a total of"," ",COUNT(OCCUPATION)," ",LOWER(OCCUPATION),'s.') 
FROM OCCUPATIONS 
GROUP BY OCCUPATION 
ORDER BY COUNT(OCCUPATION) ASC;

```

**We define an employee's total earnings to be their monthly  worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as  space-separated integers.**

```
select concat(max(months*salary),' ',count(*))
from employee
group by months*salary desc
limit 1;
```

## JOIN
**Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.**

```
SELECT country.continent, FLOOR(AVG(city.population)) 
FROM city 
JOIN country 
ON city.countryCode = country.code 
GROUP BY country.continent;
```
**You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.
Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.
Write a query to help Eve.**

```
SELECT 
CASE
  WHEN Grade >= 8 THEN Name
  ELSE NULL
END AS Name, Grade, Marks 
FROM Students INNER JOIN Grades 
ON Students.Marks BETWEEN Grades.Min_Mark AND Grades.Max_Mark 
ORDER BY Grade DESC, Name ASC, Marks ASC;
```
