
# SQL Movie-Rating Query Exercises Extras Answers

You find below my answers to the SQL Movie Rating Query exercises extras. 
The database can be found [here][1]. 
To see the schema and data click [here][2]. 

Please report any issues.

## Q1

Find  the names of all reviewers who rated  Gone with the Wind.

```sql
select name
from Reviewer
where rID in ( select rID 
			   from Movie natural join Rating 
			   where title = 'Gone with the Wind' );
```

## Q2

For  any rating where the reviewer is the same as the director of the movie, return the reviewer name, movie title, and number of stars.

```sql
select distinct name , title , stars
from Reviewer natural join ( Movie natural join Rating )
where name = director
```

## Q3


Return  all reviewer names and movie names together in a single list, alphabetized. (Sorting by the first name of the reviewer and first word in the title is fine; no need for special processing on last names or removing "The".)

```sql
select * from(
		select name from Reviewer
		union
		select title from Movie
	) as name
order by name;
```

## Q4

Find  the titles of all movies not reviewed by Chris Jackson.
```sql
select title
from Movie
where mID not in ( select mID 
				  from Rating natural join Reviewer
				  where name = 'Chris Jackson' )
```

## Q5

For all pairs of reviewers such that both reviewers gave a rating to the same movie, return the names of both reviewers. Eliminate duplicates, don't pair reviewers with themselves, and include each pair only once. For each pair, return the names in the pair in alphabetical order.

```sql
select distinct min(r1.name , r2.name) as name , max(r1.name,r2.name) 
from ( Rating natural join Reviewer ) r1 , ( Rating natural join Reviewer ) r2
where r1.rID < r2.rID and r1.mID = r2.mID 
order by name
```

## Q6

For each rating that is the lowest (fewest stars) currently in the database, return the reviewer name, movie title, and number of stars.

```sql
select name , title , stars
from Reviewer natural join ( Movie natural join Rating )
where stars = ( select min(stars) from Rating )
```

## Q7

List movie titles and average ratings, from highest-rated to lowest-rated. If two or more movies have the same average rating, list them in alphabetical order.

```sql
select title , avg(stars) as avg
from Rating natural join Movie
group by title
order by avg desc , title;
```

## Q8

Find the names of all reviewers who have contributed three or more ratings. (As an extra challenge, try writing the query without HAVING or without COUNT.)
```sql
select name 
from ( select name , count(rID) as reviews
		from Reviewer natural join Rating
		group by rID
	  )
where reviews > 2;
```

## Q9

Some directors directed more than one movie. For all such directors, return the titles of all movies directed by them, along with the director name. Sort by director name, then movie title. (As an extra challenge, try writing the query both with and without COUNT.)

```sql
select r1.title as title , r1.director as director
from Movie r1 , Movie r2
where r1.director = r2.director and r1.mID <> r2.mID
order by director , title;
```

[1]: sql-schemas/rating.sql
[2]: http://cs.stanford.edu/people/widom/