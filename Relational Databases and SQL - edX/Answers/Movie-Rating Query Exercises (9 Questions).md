
# SQL Movie-Rating Query Exercises Answers

You find below my answers to the SQL Movie Rating Query exercises. 
The database can be found [here][1]. 
To see the schema and data click [here][2]. 

Please report any issues.

## Q1

Find the titles of all movies directed by Steven Spielberg.

```sql
select title
from Movie
where director = 'Steven Spielberg';
```

## Q2

Find all  years  that have a movie that received a rating of 4 or 5, and sort them in increasing order.

```sql
select distinct year
from Movie natural join Rating
where stars >= 4
order by year;
```

## Q3

Find  the titles of all movies that have no ratings.
```sql
select title 
from Movie
where mID in ( select distinct mID
from Movie
except
select mID from Rating );
```

## Q4

Some  reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.

```sql
select distinct name
from Reviewer natural join Rating
where ratingDate is null;
```

## Q5

Write a query to return the ratings data in a more readable format: reviewer name, movie title, stars, and ratingDate. Also, sort the data, first by reviewer name, then by movie title, and lastly by number of stars.

```sql
select name , title , stars , ratingDate
from Movie natural join ( Reviewer natural join Rating )
order by name , title , stars;
```

## Q6

For all cases where the same reviewer rated the same movie twice and gave it a higher rating the second time, return the reviewer's name and the title of the movie.

```sql
select distinct name , title
from Movie natural join Reviewer
where rID in ( select r1.rID 
				from Rating r1 , Rating r2
				where r1.rID = r2.rID and r1.mID = r2.mID 
					and r1.stars < r2.stars 
					and r1.ratingDate < r2.ratingDate )
		and mID in ( select r1.mID 
					from Rating r1 , Rating r2
					where r1.rID = r2.rID and r1.mID = r2.mID 
					and r1.stars < r2.stars 
					and r1.ratingDate < r2.ratingDate );
```

## Q7

For each movie that has at least one rating, find the highest number of stars that movie received. Return the movie title and number of stars. Sort by movie title.

```sql
select title , max( stars )
from Movie natural join Rating
group by title
order by title;
```

## Q8

For each movie, return the title and the 'rating spread', that is, the difference between highest and lowest ratings given to that movie. Sort by rating spread from highest to lowest, then by movie title.

```sql
select title , max(stars) - min(stars) as spread
from Movie natural join Rating
group by title
order by spread desc , title;
```

## Q9

Find the difference between the average rating of movies released before 1980 and the average rating of movies released after 1980. (Make sure to calculate the average rating for each movie, then the average of those averages for movies before 1980 and movies after. Don't just calculate the overall average rating before and after 1980.)

```sql
select ROUND( ( select avg(a1) as avg1 
			   from ( select avg( stars ) as a1 
					 	from Rating natural join Movie 
					 	where year < 1980 
					 	group by mID ) ) 
			 - 
			  ( select avg(a2) as avg2 
			   from ( select avg( stars ) as a2 
					 	from Rating natural join Movie 
					 	where year > 1980 
					 	group by mID ) ) 
			 ,16 );
```

[1]: sql-schemas/rating.sql
[2]: http://cs.stanford.edu/people/widom/