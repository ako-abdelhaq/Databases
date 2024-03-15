
# SQL Social-Network Query Exercises Extras Answers

You find below my answers to the SQL Social-Network Query Exercises extras. 
The database can be found [here][1]. 
To see the schema and data click [here][2]. 

Please report any issues.

## Q1

For every  situation where student A likes student B, but student B likes a different student C, return the names and grades of A, B, and C.

```sql
select distinct h1.name , h1.grade , h2.name , h2.grade , h3.name , h3.grade 
from Highschooler h1 , Highschooler h2 , Highschooler h3 , Likes
where (h1.ID , h2.ID) in Likes and  (h2.ID , h3.ID) in Likes 
		and h3.ID <> h1.ID;
```

## Q2

Find  those  students for whom all of their friends are in different grades from themselves. Return the students' names and grades.

```sql
select h.name , h.grade
from Highschooler h
where not exists ( select f.ID 
				   from Highschooler f
				   where ( h.ID , f.ID ) in Friend and h.grade = f.grade );
```

## Q3


What  is  the average number of friends per student? (Your result should be just one number.)

```sql
select avg( friends )
from (  select count(*) as friends
		from Friend
		group by ID2 );
```

## Q4

Find  the  number of students who are either friends with Cassandra or are friends of friends of Cassandra. Do not count Cassandra, even though technically she is a friend of a friend.

```sql
select count (distinct h1.ID)
from Highschooler h1 , Highschooler h2 , Highschooler h3 , Likes
where h2.name = 'Cassandra' and (h1.ID , h2.ID) in Friend and h2.ID <> h1.ID 
		or ( (h1.ID , h3.ID ) in Friend 
				and h2.name = 'Cassandra'
			 	and ( h3.ID , h2.ID ) in Friend 
				and h1.ID <> h2.ID );
```

## Q5

Find  the  name and grade of the student(s) with the greatest number of friends.
```sql
select name , grade
from Highschooler
where ID in ( select ID1 
			  from ( select ID1 , count(*) as friends
					 from Friend
					 group by ID1
				    ) 
			  where friends = ( select max( friends )
							  	from (  select ID1 , count(*) as friends
									 	from Friend
									 	group by ID1
									 ) 
							  )
			 );
```



[1]: sql-schemas/rating.sql
[2]: http://cs.stanford.edu/people/widom/