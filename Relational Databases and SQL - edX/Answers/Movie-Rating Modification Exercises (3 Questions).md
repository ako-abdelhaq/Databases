
# SQL Movie-Rating Modification Exercises Answers

You find below my answers to the SQL Movie-Rating Modification Exercises. 
The database can be found [here][1]. 
To see the schema and data click [here][2]. 

Please report any issues.

## Q1

Add the reviewer Roger Ebert to  your  database, with an rID of 209.

```sql
insert into Reviewer
values ( 209 , 'Roger Ebert' );
```

## Q2

For all  movies  that have an average rating of 4 stars or higher, add 25 to the release year. (Update the existing tuples; don't insert new tuples.)

```sql
update Movie
set year = year + 25
where mID in ( select mID 
			   from Rating
			   group by mID 
			   having avg(stars) >= 4 )
```

## Q3


Remove all  ratings  where the movie's year is before 1970 or after 2000, and the rating is fewer than 4 stars.

```sql
delete from Rating
where mID in ( select mID 
			   from Movie 
			   where year < 1970 or year > 2000 ) 
	  and stars < 4;
```



[1]: sql-schemas/rating.sql
[2]: http://cs.stanford.edu/people/widom/