
# SQL Social-Network Query Exercises Answers

You find below my answers to the SQL Social-Network Query Exercises. 
The database can be found [here][1]. 
To see the schema and data click [here][2]. 

Please report any issues.

## Q1

Find  the  names of all  students  who are friends with someone named Gabriel.

```sql
select name
from Highschooler 
where ID in ( select ID1 
              from Friend
			  where ID2 in ( select ID 
							  from Highschooler
							  where name = 'Gabriel') )
```

## Q2

For  every student who likes someone 2 or more grades younger than themselves, return that student's name and grade, and the name and grade of the student they like.

```sql
select distinct h2.name , h2.grade , h1.name , h1.grade
from Highschooler h1 , Highschooler h2 , Likes
where h1.ID <> h2.ID and h1.grade + 2 <= h2.grade 
		and ( (h2.ID , h1.ID) in Likes or (h1.ID , h2.ID) in Likes);
```

## Q3


For  every  pair of students who both like each other, return the name and grade of both students. Include each pair only once, with the two names in alphabetical order.

```sql
select distinct min(h2.name,h1.name) , h1.grade , max(h2.name,h1.name) , h2.grade
from Highschooler h1 , Highschooler h2 , Likes
where h1.ID < h2.ID 
	and (h2.ID , h1.ID) in Likes 
	 and (h1.ID , h2.ID) in Likes
```

## Q4

Find all students who do not appear in the Likes table (as a student who likes or is liked) and return their names and grades. Sort by grade, then by name within each grade.

```sql
select distinct name , grade
from Highschooler 
where not exists ( select ID1 
				   from Likes 
				   where ( ID1 , ID ) in Likes)
	and  not exists ( select ID2 
					  from Likes 
					  where ( ID , ID2 ) in Likes)
```

## Q5

For  every  situation where student A likes student B, but we have no information about whom B likes (that is, B does not appear as an ID1 in the Likes table), return A and B's names and grades.

```sql
select distinct h1.name , h1.grade , h2.name , h2.grade
from Highschooler h1 , Highschooler h2 , Likes
where (h1.ID , h2.ID) in Likes and not exists ( select ID2 
												from Likes 
										  		where ( h2.ID , ID2 ) in Likes )
```

## Q6

Find names and grades of students who only have friends in the same grade. Return the result sorted by grade, then by name within each grade.

```sql
select h1.name , h1.grade
from Highschooler h1
where not exists ( select * 
				   from Highschooler h2
				   where ( h1.ID , h2.ID ) in Friend and h1.grade <> h2.grade)
order by 2 , 1;
```

## Q7

For  each  student A who likes a student B where the two are not friends, find if they have a friend C in common (who can introduce them!). For all such trios, return the name and grade of A, B, and C.

```sql
select distinct h1.name , h1.grade , h2.name , h2.grade , h3.name , h3.grade 
from Highschooler h1 , Highschooler h2 , Highschooler h3 , Likes
where (h1.ID , h2.ID) in Likes and ( (h1.ID , h2.ID) not in ( select * from Friend ) ) 
		and h3.ID in ( select ID 
					   from Highschooler
					   where (h1.ID , ID) in Friend and (h2.ID , ID) in Friend )
```

## Q8

Find  the  difference between the number of students in the school and the number of different first names.

```sql
select count(*)
from Highschooler h1 , Highschooler h2
where h1.ID < h2.ID and h1.name = h2.name
```

## Q9

Find  the  name and grade of all students who are liked by more than one other student.

```sql
select name , grade
from Highschooler
where ID in ( select ID2 
			 from Likes
			 group by ID2
			 having count(*) > 1 
			)
```

[1]: sql-schemas/rating.sql
[2]: http://cs.stanford.edu/people/widom/