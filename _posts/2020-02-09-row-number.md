---
layout: post
title: My introduction to window functions
---
*Last Monday, I started working @ Opinary (Berlin) as a Data Scientist. Wednesday, I was introduced
to MySQL / BigQuery window functions. They're likely to be one of the most useful (and one of
my favourite) functions from now on. Let me very quickly describe what window functions are.*

Imagine you have a database that looks like this:

|employees   |
|-------------------    |
|name, age, salary, department |
|Brian, 24, 1000, Sales <br>Jonathan, 32, 2800, Engineering<br>Melissa, 40, 2500, Engineering<br>John, 25, 3000, Engineering<br>Lucy, 30, 2800, Sales<br> James, 28, 1500, Marketing|

and you're asked to calculate which are the best paid employees per department. To me, this called
to GROUP BY deparment find the MAXimum salary and JOIN the resulting table back to the original one.
In MySQL this corresponds to:

```
SELECT name, age, salary, department, max_department_salary = salary as
is_best_paid_department_employee FROM employees JOIN (SELECT MAX(salary) as max_department_salary
FROM employees GROUP BY deparment) USING(department)
```

This is all good and fine and would result in something like this:

|query result|
|-------------------    |
|name, age, salary, department, is_best_paid_department_employee |
|Brian, 24, 1000, Sales, False <br>Jonathan, 32, 2800, Engineering, False <br>Melissa, 40, 2500, Engineering, False <br> John, 25, 3000, Engineering, True<br>Lucy, 30, 2800, Sales, True<br> James, 28, 1500, Marketing, True|

Now, imagine ask your colleague asks you this (artificial) follow-up question: "Oh, can you calculate
the second best paid employees?". You think "Well, I could remove best paid employees and repeat the query again.
It's not super nice, but it should work". Your invested colleague continues and asks:
"Actually, can you tell me how each employee ranks in their department?". That to me, sounded very
complex... until I heard about window functions.

Window functions perform a calculation on a group of related rows. The simplest one: ROW_NUMBER().
This function simply assigns a row number to every row in the table or to a subset of them. We can,
for example, assign row numbers to subgroups defined by a column like in a GROUP_BY using
the PARTITION BY clause. The rows belonging to a group can also be sorted according to some 
criteria and then assigned a row number. In our case, we could do:

```
SELECT name, age, salary, department, ROW_NUMBER() OVER (PARTITION BY deparment ORDER BY salary DESC)
as nth_best_paid_department_employee FROM employees
```

which would return:

|query result|
|-------------------    |
|name, age, salary, department, nth_best_paid_department_employee |
|Brian, 24, 1000, Sales, 2<br>Jonathan, 32, 2800, Engineering, 2<br>Melissa, 40, 2500, Engineering, 3<br>John, 25, 3000, Engineering, 1<br>Lucy, 30, 2800, Sales, 1<br> James, 28, 1500, Marketing, 1|

ROW_NUMBER is a non-aggregate window function as it assigns an individual value to the
rows that have been grouped (_partitioned_) as oppossed to aggregate ones using GROUP BY that are
used to calculate summary statistics (max, min, count, etc) over the different groups.

## EXTRA: What if several employees earned the same maximum amount?
Well, in this case, ROW_NUMBER would assign number 1 to an arbitrary employee and subsequent numbers
to the rest. However, we can do better than this using another window function called RANK. 
RANK will assign the same number to employees with the same salary. For example, if
our top paid employees earn [3000, 3000, 2500, 2500, 2300], RANK will return [1, 1, 3, 3, 4]. DENSE_RANK,
a variation of this window function, will return [1, 1, 2, 2, 3].
