
# SQL Social-Network Modification Exercises Answers

You find below my answers to the SQL Social-Network Modification Exercises. 
The database can be found [here][1]. 
To see the schema and data click [here][2]. 

Please report any issues.

## Q1

It's time  for  the seniors to graduate. Remove all 12th graders from Highschooler.

```sql
delete from Highschooler
where grade = 12
```

## Q2

If two  students  A and B are friends, and A likes B but not vice-versa, remove the Likes tuple.

```sql
delete from Likes
where ( ID1 , ID2 ) in ( select ID1 , ID2 
						 from Likes
						 where (ID1 , ID2) in friend 
						 	and ( ID1 , ID2 ) in Likes
						 	and ( ID2 , ID1 ) not in Likes )
```

## Q3


For all cases where A is friends with B, and B is friends with C, add a new friendship for the pair A and C. Do not add duplicate friendships, friendships that already exist, or friendships with oneself. (This one is a bit challenging; congratulations if you get it right.)

```sql
insert into Friend
	select distinct h1.ID , h3.ID
	from Highschooler h1 , Highschooler h2 , Highschooler h3 , Friend
	where (h1.ID , h2.ID) in Friend and h2.ID <> h1.ID 
		and ( (h2.ID , h3.ID ) in Friend and h2.ID <> h3.ID 
				and ( h1.ID , h3.ID ) not in Friend 
				and h1.ID <> h3.ID 
			)
	 ;
```



[1]: sql-schemas/rating.sql
[2]: http://cs.stanford.edu/people/widom/