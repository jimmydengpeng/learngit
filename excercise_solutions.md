# Chapter 03 - SQL
## 3.1
### a. Find the titles of courses in the Comp. Sci. department that have 3 credits.
``` sql
select title
from department natural join course
where dept_name = 'Comp. Sci.' and credits = 3;
```
> Robotics   
Image Processing  
Database System Concepts

<br>    

### b. Find the IDs of all students who were taught by an instructor named Einstein; make sure there are no duplicates in the result.
```sql
select takes.ID 
from takes, (select course_id as eid
    from instructor natural join teaches
    where name = 'Einstein')
where takes.course_id = eid;
```
```sql
select takes.id
from takes join teaches using (course_id)
where teaches.ID = (
    select id
    from instructor
    where name = 'Einstein'
)
```
> 44553

<br>   

### c. Find the highest salary of any instructor.
```sql
select max(salary)
from instructor
```
> 95000

<br>   

### d. Find all instructors earning the highest salary (there may be more than one with the same salary).
```sql
select id, name
from instructor
where salary = (select max(salary) from instructor)
```
> 22222,Einstein

<br>   

### e. Find the enrollment of each section that was offered in Autumn 2009.
```sql
select course_id, count(*)
from section natural join takes
where year = 2009
group by course_id
```
> BIO-101,1  
CS-101,6  
CS-190,2  
CS-347,2  
EE-181,1  
PHY-101,1  

<br>   

### f. Find the maximum enrollment, across all sections, in Autumn 2009.
```sql
select max(c)
from (
    select course_id, count(*) as c
        from section natural join takes
        where year = 2009 and semester = 'Fall'
        group by course_id
)
```
> 6

<br>   

### g. Find the sections that had the maximum enrollment in Autumn 2009.
```sql
select course_id, course.title, max(c)
from (
    select course_id, count(*) as c
        from section natural join takes
        where year = 2009 and semester = 'Fall'
        group by course_id
) natural join course
```
> CS-101,Intro. to Computer Science,6
<br>   
