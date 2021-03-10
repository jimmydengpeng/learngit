## Chapter 3: SQL
### 3.1
- a
``` sql
select title
from department natural join course
where dept_name = 'Comp. Sci.' and credits = 3;
```
- b
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
- c
```sql
select max(salary)
from instructor
```
- d
```sql
select id, name
from instructor
where salary = (select max(salary) from instructor)
```
- e
```sql
select course_id, count(*)
from section natural join takes
where year = 2009
group by course_id
```
- f
```sql
select max(c)
from (
	select course_id, count(*) as c
		from section natural join takes
		where year = 2009 and semester = 'Fall'
		group by course_id
)
```
- g
```sql
select course_id, course.title, max(c)
from (
	select course_id, count(*) as c
		from section natural join takes
		where year = 2009 and semester = 'Fall'
		group by course_id
) natural join course
```